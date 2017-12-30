## 睁大双眼，认真审视这屎一样的文档
写的一片混乱的文档，数据分类明明是以code和geohash未区分。不知道为什么后续作妖按什么table data, time series data和json分。恕在下是真的没看懂。  
扫视N遍后发现最重要的话隐藏在不经意的角落：   
> There are currently two ways to connect data with points on a map. Either by matching a tag or series name to a country code/state code (e.g. SE for Sweden, TX for Texas) or by using geohashes to map against geographic coordinates.
## 可以解决的方法： 
1. Backend Design: calculate geohash according to sensor data pair (long, la) before pushing data to influxdb
2. Modify my sensor json format
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
