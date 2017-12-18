# 为什么写这篇博客？
网络上关于windows系统下搭建从数据源到前端可视化工具Grafana的解决方案甚少，且适合我自己本身开发所需情况的方案就更加少了。 在翻阅大量官方文档，github issues以及英文博客后，终于得到了可运行的demo。把相关详细的配置过程记录下来，方便以后学习或工作复用并造福于有相似需求的朋友。

# 服务构架
IoT Simulator(publisher)----> MQTT broker---->Telegraf(subscriber)---->InfluxDB---->Hosted Grafana(Cloud)
# 产品服务介绍
## MQTT
### 什么是MQTT协议？
MQTT为MQ Telemetry Transport的缩写，该协议定义了在机器对机器或物联网环境下的通信规则。它采用发布/订阅的模式传输数据，设计思想是在尽力保证一定程度的数据可达性及稳定性的同时，减少对网络带宽和设备资源的依赖。MQTT协议简洁且轻量，适用于低带宽，高延迟或不稳定的网络环境中的设备，同时也适用于带宽和电源受限的移动应用.

Ref:http://mqtt.org/faq 
### 为什么使用MQTT协议？
在使用Power BI作为可视化方案时，曾成功使用REST API直接将数据源通过HTTP推送到POWER BI所提供的endpoint。因此在架构这套服务之初，我并没有打算使用MQTT作为数据传输协议。但经过一番研究后，在我的案例当中，发现使用HTTP协议有以下局限性：  

1. 在Telegraf的input plugins中，和HTTP相关的插件有两个：一个是HTTP JSON，另一个是HTTP Listener（HTTP Response由于不符合个体案例没有做研究）； HTTP JSON主要通过向拥有数据的HTTP URLs发送请求，并从对应响应中的json中获取数据。由于我的IoT设备仅仅是一个模拟的数据发送器且并没有为其部署本地服务器或云端服务器，因此无法分配到URL地址和端口，同时另一个考虑是希望减少在部署服务器上花费的成本，更好的集中在可视化工具上的研究上。 因此这个插件并不适合我的情况；HTTP Listener主要监听HTTP POST上的消息。Telegraf可以作为代理服务器来处理原本通过InfluxDB HTTP API 上 /write 写入的数据。听起来这个似乎深得我心，没有多余的学习成本---与使用POWER　BI时情景类似，可以将数据直接推入InfluxDB的API终端，然后设置Telegraf作为代理在写入数据库之前对数据流做process或aggregation的工作，使得数据变得更加具有可读性（meaningful）。简单粗暴快捷。唯一也是致命的缺点是如果使用HTTP Listener将仅支持[InfluxDB line protocol format](https://docs.influxdata.com/telegraf/v1.5/concepts/data_formats_input/) 作为数据写入格式。这就使得数据源的格式大大受限，数据输入格式解析的功能也相当于无法使用了，那么使用telegraf的意义就变得不那么大（对数据流进行格式解析和聚合）；

2. 我使用的IoT Simulator对MQTT协议有较为全面的支持，无需二次开发接口；

Ref:https://docs.influxdata.com/telegraf/v1.5/plugins/inputs/
### 配置中使用的MQTT
* 如何安装MQTT Broker: 参见[这里](http://www.steves-internet-guide.com/install-mosquitto-broker/)，以及[这里](https://sivatechworld.wordpress.com/2015/06/11/step-by-step-installing-and-configuring-mosquitto-with-windows-7/)

* Publish/Subscribe:The MQTT protocol is based on the principle of publishing messages and subscribing to topics, or "pub/sub". Multiple clients connect to a broker and subscribe to topics that they are interested in. Clients also connect to the broker and publish messages to topics. Many clients may subscribe to the same topics and do with the information as they please. The broker and MQTT act as a simple, common interface for everything to connect to. This means that you if you have clients that dump subscribed messages to a database, to Twitter, Cosm or even a simple text file, then it becomes very simple to add new sensors or other data input to a database, Twitter or so on.

MQTT client1(sub)--->MQTT broker<----MQTT Client2(pub)  
                   (message center)                            
                          ^  
                          |  
                    MQTT client2(pub)  

* Topic setting: 话题可以被划分层级，用/来表示具体层级结构。 例如： sensors/COMPUTER_NAME/temperature/HARDDRIVE_NAME
two wildcards: # and +  
"+" for a single level of hierarchy，+/+/+/HARDDRIVE_NAME表示了包含上述例子的一个父集  
"#" for all remaining levels of hierarchy，sensors/COMPUTER_NAME/temperature/# 表示了包含上述例子的一个父集  
* Quality of Service: **Higher levels of QoS are more reliable, but involve higher latency and have higher bandwidth requirements.**  
0: The broker/client will deliver the message once, with no confirmation.  
1: The broker/client will deliver the message at least once, with confirmation required.  
2: The broker/client will deliver the message exactly once by using a four step handshake.  
Downgrade for QoS  
Ref: https://mosquitto.org/man/mqtt-7.html  
##InfluxDB HTTP API和Hosted Grafana HTTPS 通讯的冲突问题
Influx DB默认采用HTTP协议进行Client和Server端的通信，而云端的Grafana服务则强制采用HTTPS确保数据传输的安全性。 众所周知，HTTPS协议是HTTP协议的安全版本，其安全性能的实现主要依靠在Transport Layer之上增加的TLS/SSL层实现文本及数据的加密。HTTPS与HTTP一个重要的区别在于HTTPS增加了对身份的验证功能，因此第三方无法伪造服务端或客户端身份，由此引入了证书认证来确保功能的实现。
为了配合云端服务所使用的HTTPS协议，因此我将InfluxDB的接口也进行了相关配置，使得API利用TLS层使用HTTPS协议进行数据的传输。　


### 心得
1. 作为开源产品Grafana和InfluxDB,两者的documentation和error hint做的都不是特别好，在开发过程中，我花了大量时间理解文档内容和错误提示。如果能在这两个方面多花功夫；
