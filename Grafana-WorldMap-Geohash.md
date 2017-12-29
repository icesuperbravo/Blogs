## 可以解决的方法： 
1. Backend Design: calculate geohash according to sensor data pair (long, la) before pushing data to influxdb
2. Modify my sensor json format
3. Telegraf plug-in development
4. Kapacitor???
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
