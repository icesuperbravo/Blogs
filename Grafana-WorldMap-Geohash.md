## 睁大双眼，认真审题（这屎一样的文档）
写的一片混乱的文档，数据分类明明是以code和geohash未区分。不知道为什么后续作妖按什么table data, time series data和json分。恕在下是真的没看懂。  
扫视N遍后发现最重要的话隐藏在不经意的角落：   
> There are currently two ways to connect data with points on a map. Either by matching a tag or series name to a **country code/state code** (e.g. SE for Sweden, TX for Texas) or by using **geohashes** to map against geographic coordinates.
对于code： 可以使用grafana预先定义的code， 也可以自定义一些code并用json/jsonp方式导入;  
对于geohash: 主要是为了支持elasticsearch， 但是对于influxdb， 可以人工添加geohash的tag，并将数据看作是表格读取geohash tag中的内容； 
## 问题所在
一个悲伤的事实是： influxdb不支持geohash(哭！)而我的数据源产生的数据也不包括geohash。geohash实在是一种太高级的地理数据格式了，作为一个朴素的IoT设备，通常的地理数据是通过GPS采集到的经纬度信息 e.g. (latitude, longtitude);  
为了能够使用这高大上的地图，那我势必就需要对我的原始数据做处理咯。要不就是在json数据包里额外添加一些辅助code，要不就加上geohash信息。可是加上它们本身就很不容易，因为从经纬度到这些人类可读的信息需要经过一些计算得到，而这些计算是否能在IoT设备本身计算得到呢？这点我并不确定。其次，我所使用的模拟器设备并不支持geohash数据的模拟。因此解决方法中的1被我否掉了，还是要保持json数据的高傲和纯洁；  
## 可能可以解决的方法： 
1. 在原始数据中添加对应经纬度信息的country code或geo hash等信息；
2. 使用node-influx和node-geohash pull data，处理添加geohash tag再存入influxdb；
3. Telegraf plug-in development---->need to develop a small plug-in with Golang
4. Kapacitor---->need to develop a small plug-in with Golang, need to customize script to add geohash function
5. use Node-Red service to add geohash encode/decode functionality;

### 安装Node-Red
presiquite: node.js
tips:用了一个插件叫做chocolately, 从此Windows也拥有了软件包管理，命令行安装package不是梦！
在cmd输入： 
`choco install nodejs-lts`

```
npm install node-red-node-geohash
npm install  node-red-contrib-influxdb
```
