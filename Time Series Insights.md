(｡･∀･)ﾉﾞ嗨，盆友们，这次我胡汉三又回来啦！这次我们要讨论的另一款功能强大的可视化工具是与Power BI师出同门的Time Series Insights(微软爸爸的怀抱).  
俗话说的好，相亲前要先看简历！那么Time Series Insights简历会是什么样呢？他为什么能从众多追求竞争者中脱颖而出？是长相出众？还是个性独特？我们要从TSI的概念开始聊起！
### 1. Concept
根据Time Series Insights官方文档所述： 
According to Time Series Insights' official documentation:
>AZURE TIME SERIES INSIGHTS IS A **FULLY MANAGED ANALYTICS, STORAGE, AND VISUALIZATION SERVICE** THAT MAKES IT SIMPLE TO EXPLORE AND ANALYZE **BILLIONS OF IOT EVENTS SIMULTANEOUSLY**. IT GIVES YOU A GLOBAL VIEW OF YOUR DATA, LETTING YOU QUICKLY VALIDATE YOUR IOT SOLUTION AND AVOID COSTLY DOWNTIME TO MISSION-CRITICAL DEVICES BY HELPING YOU DISCOVER **HIDDEN TRENDS, SPOT ANOMALIES, AND CONDUCT ROOT-CAUSE ANALYSES IN NEAR REAL-TIME**.  

在这段言简意赅的浓缩概括中，几个闪亮的关键词引起了我的特别注意：  
（There are a few glittering keywords which really catch my attention when I read this paragrah: ） 
1. **FULLY MANAGED ANALYTICS, STORAGE, AND VISUALIZATION SERVICE**  
换言之， **Azure TSI=SQL Database+Query System(powerful analysis)+Visualization Layer**.   
另外， 'Fully Managed' 可能暗示着TSI提供的解决方案是开箱即用的，无需工程师进行复杂的架构和调配的。从上述我们给出的公式也可以看出TSI是多种工具融合一体的产品，因此推测可能会非常易部署和上手(Also, 'Fully Managed' indicates that Time Series Insights is probably an out-of-the-box solution with no complex architecture and easy configuration. From the above formula that we gave, it can also be inferred that TSI is an handy and easy-to-deploy product)。
2. **BILLIONS OF IoT EVENTS SIMULTANEOUSLY**    
TSI支持同时对上千万IoT时间数据的可视化，以全局视角来展示数据，'extremely suitable for when the number of devices exceeded several hundred thousand. Even POWER BI doesn't have the ability to do this（特别适用于当IoT设备数量超过十万的情景。此时Power BI可能都没有这样的能力做到这一点）.'  
3. **HIDDEN TRENDS, SPOT ANOMALIES, AND CONDUCT ROOT-CAUSE ANALYSES IN NEAR REAL-TIME**  
TSI能帮助用户发现数据潜在趋势，侦测设备异常且具备根源分析能力，而这一切的操作实现几乎都在实时。

* TSI所解决的用户痛点：
![challenges](https://github.com/icesuperbravo/Blogs/blob/master/time-series-insights/azure3.PNG?raw=true)

这张截图来自微软首席项目经理OP Ravi在Microsoft Build 2017中针对TSI的产品展示。  
它阐述了在IoT数据可视化领域，现今客户的普遍痛点：    
* 数据总是被储存本地，无法在云端共享;
* 工程师或数据分析师没有时间做可视化前的数据处理准备;  
* 很难去可视化IoT大量级数据（比如当数据的数量超过10万以上）；
* 可视化的工具能够公司被不同层级不同岗位的人员使用，易用易上手。

根据微软的另一产品经理Andrew Shannon在IoTSWC 2017会议中所描述，TSI原本只是一款Microsoft公司内部使用的产品，而正是因为他们发现其他公司也有着和微软同样的痛点，他们决定将这款产品商业化，并放入Azure生态环境。
* 一张图对TSI的总结
![core scenarios](https://github.com/icesuperbravo/Blogs/blob/master/time-series-insights/azure2.PNG?raw=true)
TSI在这些核心场景中能展现其在市场中独特优势： 
* IoT时间序列数据的可视化和分析；
* 针对多设备，多工厂的不同数据的统一视窗
* IoT方案的验证和检测
* 根源问题分析和异常侦测
* 支持REST API, 自由灵活地在TSI上层开发您自己的APP

综上所述，TSI不同于一般的终端可视化软件，以展示数据仪表盘为主， 它是一款针对海量IoT设备数据的统一化**可视和分析软件**。它由多种工具集成，开箱即用，操作简便友好，对非专业工程师人员同样适用。
### 2. Architecture
![TSI Architecture](https://github.com/icesuperbravo/Blogs/blob/master/time-series-insights/azure1.PNG?raw=true)

作为Azure生态圈中一款IoT产品，TSI的架构自然以来于Azure中其他产品所组成。事件数据从不同遥感设备上传入到Azure IoT Hub或Azure Event Hub中。 通过简单的设置即可将数据储存在TSI自带的SQL数据库，数据将以时间为主索引进行排列整理，最终通过TSI Explorer图形化展示。
* 使用TSI后架构发生的变化(Comparison between 'before TSI' and 'after TSI')  
![Architecture before Azure TSI implementation](https://predica.pl/wp-content/uploads/2017/07/Original-architecture.png)  
Comparison A. Architecture before Azure TSI implementation.
![Architecture after Azure TSI implementation.](https://predica.pl/wp-content/uploads/2017/07/Changed-architecture.png)  
Comparison B. Architecture after Azure TSI implementation.  
可以看到，在使用TSI后，架构设计中减少了产品使用的数量。并且省去了在存入数据库前对数据的预先流处理的环节。而TSI能完美地代替Stream Analytics,利用这些未经处理的原始数据自动生成可用的Schema供用户分析选择。**这样一来不仅简化的了产品架构的复杂程度，也节省了一定的人力和金钱成本**。

### 3. Using Time Series Insights to expore your data
* 配置过程  
TSI配置过程较为简单，注意使用TSI的前提条件为： 
1. Azure可用的账户;
2. 数据流经IoT Hub或Event Hub.
由于无复杂的构架，具体配置过程可参见[微软官方手册](https://docs.microsoft.com/en-us/azure/time-series-insights/time-series-insights-get-started)。  
其他相关配置操作请参见上述链接中左方导航栏的How-to Guide。

* 产品界面
TSI explorer为一款云端基于web的可视化及分析工具，其主要界面如下图所示： 


* 

* 实时图形刷新频率<=60s  
The data update interval is usually within 60 seconds. And it only automatically refresh the line graph of the belowing query sector. 
![auto-refresh](https://github.com/icesuperbravo/Blogs/blob/master/time-series-insights/time-series-insights.PNG?raw=true)
当要搜索的时间区域确定后，主界面所展示的line graph和heatmap是不会随时间自动刷新的。但搜索区域的索引line graph是会以约1分钟/次的频率刷新的，不过条件是将界面右上角的autofresh功能打开。
### 4. Conclusion

#### Benefits:
1. Reducing the number of services, and therefore costs(cost effective) – thanks to replacing Stream Analytics and databases which we no longer needed;
2. Simplicity(Full-managed, highly integrated and an out-of-the-box solution) – the whole logic of data aggregation is prepared in one tool; 
3. Free Schema
**4. Real-time analytics – there is a live data preview via line graph and a heat map**
4. Flexibility – the solution is accessible via APIs. You can customize your visualization on the top of TSI.
5. Big data scalable, extremely suitable for when the number of devices exceeded several hundred thousand. Even POWER BI doesn't have the ability to do this.
#### Caveats:
1. Azure Eco-Envrionement----only accept source from IoT Hub and Event Hub
2. Only Line Graph and Heatmap, no customization or any edit;

### [Appendix]Reference: 
1. https://predica.pl/blog/azure-time-series-insights-for-iot-devices/
2. https://www.youtube.com/watch?v=uH4Eim6HqgY
3. https://www.youtube.com/watch?v=BgJrhfpjdWs
