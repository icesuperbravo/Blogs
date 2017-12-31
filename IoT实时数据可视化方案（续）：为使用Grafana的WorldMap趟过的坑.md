## 万万没想到，我这一世英名葬送在了地图坑里
继上次搭建完框架得到了个粗糙的demo以后，我天真的以为我离真理的距离简直就只有一步之遥了。
## 睁大双眼，认真审题（这屎一样的文档）
Grafana和InfluxDB的文档大概是我有生以来看到过写的最一片混乱的文档的文档之一了，之前那篇博客就已经吐槽了N遍。
请大家继续欣赏WorldMap Panel的[documentation](https://github.com/grafana/worldmap-panel)。 说实话我一口气看了三遍竟然都没看懂这文档在说个啥。该强调的重点不强调，不该强调的倒是像老奶奶的裹脚布，又长又臭；比如数据分类明明是以code和geohash为区分，不知道为什么文档作妖按什么table data, time series data和json分。恕在下是真的没看懂。  
扫视N遍后发现最重要的话隐藏在不经意的角落：   
> There are currently two ways to connect data with points on a map. Either by matching a tag or series name to a **country code/state code** (e.g. SE for Sweden, TX for Texas) or by using **geohashes** to map against geographic coordinates.
对于code： 可以使用grafana预先定义的code， 也可以自定义一些code并用json/jsonp方式导入;  
对于geohash: 主要是为了支持elasticsearch， 但是对于influxdb， 可以人工添加geohash的tag，并将数据看作是表格读取geohash tag中的内容； 
## 问题所在
一个悲伤的事实是： influxdb不支持对geohash格式，而我的数据源产生的数据也不包括geohash或者country/state code。geohash实在是一种太高级的地理数据格式了，作为一个朴素的IoT设备，通常的地理数据是通过GPS采集到的经纬度信息 e.g. (latitude, longtitude);  

## 可能的解决方案： 
为了hack这个让我如鲠在喉，不痛不痒的娘嬉皮问题，我绞尽脑汁在google各种搜刮信息，最后得到以下几种可能的解决方法：
1. 在原始数据中添加对应经纬度信息的country code或geo hash等信息；
2. Telegraf plug-in development---->need to develop a small plug-in with Golang；
3. Kapacitor---->need to develop a small plug-in with Golang, need to customize script to add geohash function；
4. 使用[node-influx](https://github.com/node-influx/node-influx)和[node-geohash](https://github.com/sunng87/node-geohash)node.js，处理添加geohash tag再存入influxdb；  
ref[1]: https://community.influxdata.com/t/mapping-influx-data-to-maps/341/2
5. use Node-Red service to add geohash encode/decode functionality.

首先最容易想到的方法就是对我的原始数据做处理。要不就是在json数据包里额外添加一些code属性，要不就加上geohash信息。简单粗暴快捷！可是加上它们本身就很不容易，因为从经纬度到这些人类可读的信息需要经过一些计算得到，而这些计算是否能在IoT设备本身计算得到呢？这点我并不确定。其次，我所使用的模拟器设备并不支持geohash数据的模拟。因此解决方法中的1被我否掉了，还是要保持json数据的高傲和纯洁；  
## 解决方案详细配置及步骤
### 配置Node-Red
prerequisite: **node.js**  
tips:用了一个插件叫做chocolately, 从此Windows也拥有了软件包管理工具，命令行安装package不是梦！
打开 windows cmd 并输入： 
`choco install nodejs-lts`
* 安装Node-Red：   
`C:\WINDOWS\system32>npm install -g --unsafe-perm node-red`
*  安装至关重要的geohash node：   
`用户app路径\npm\node_modules\node-red>npm install node-red-node-geohash`
* 运行node-red：
`用户app路径\npm\node_modules\node-red>node-red`
* cmd提示成功信息
![](red-node-success.PNG)
* 用浏览器打开途中高亮地址，进入node-red的用户界面---新世界大门打开，噔噔！
![](UIlayout.PNG)

### 思考一个问题
既然已经确认使用Node-Red的geohash-node作为解决方案，那么这个时候要思考一个问题：
**是在数据存入数据库之前增加geohash的属性还是之后?**

### 在Red-Node上创建data flow
location-preprocessor:    
```
//The main purpose of this snippet is to extract the location info from msg.payload and then put it to msg.location to get the calculated geohash. 
var message=JSON.parse(msg.payload);
if(message[0].location!==null)
{
  msg.location={
      "lat":message[0].location.lat.toString(), 
      "lon":message[0].location.lon.toString(),
      "precision":"8"
  };
//msg.location=message;
}
return msg;
```
location-afterprocessor:  
```
//The main purpose for this snippet is to put the geohash property into msg.payload which is then transferred by mqtt-broker via certain topic
if(msg.location.geohash!==null)
{
   var message=JSON.parse(msg.payload);
   message[0].geohash=msg.location.geohash;
   msg.payload=JSON.stringify(message);
   msg.topic="sensors/wrap_geohash";
}
return msg;
```
### 检查数据库内的数据格式是否正确
到这里，数据应该安然无恙地被telegraf简单处理后存入数据库。这时对数据库进行简单的操作检查数据是否如自己预期地被写入了指定数据库。
![](correct-dbformat.jpg)

### 配置grafana



