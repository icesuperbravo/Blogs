### 1. Concept
According to Time Series Insights' official documentation: 
>AZURE TIME SERIES INSIGHTS IS A **FULLY MANAGED ANALYTICS, STORAGE, AND VISUALIZATION SERVICE** THAT MAKES IT SIMPLE TO EXPLORE AND ANALYZE **BILLIONS OF IOT EVENTS SIMULTANEOUSLY**. IT GIVES YOU A GLOBAL VIEW OF YOUR DATA, LETTING YOU QUICKLY VALIDATE YOUR IOT SOLUTION AND AVOID COSTLY DOWNTIME TO MISSION-CRITICAL DEVICES BY HELPING YOU DISCOVER **HIDDEN TRENDS, SPOT ANOMALIES, AND CONDUCT ROOT-CAUSE ANALYSES IN NEAR REAL-TIME**.

There are a few glittering 
**Azure TSI=database+query system(powerful real-time analysis)+visualization layer**  
![challenges](https://github.com/icesuperbravo/Blogs/blob/master/time-series-insights/azure3.PNG?raw=true)
![core scenarios](https://github.com/icesuperbravo/Blogs/blob/master/time-series-insights/azure2.PNG?raw=true)
* Benefits:
1. Reducing the number of services, and therefore costs(cost effective) – thanks to replacing Stream Analytics and databases which we no longer needed;
2. Simplicity(Full-managed, highly integrated and an out-of-the-box solution) – the whole logic of data aggregation is prepared in one tool; 
**3. Real-time analytics – there is a live data preview via line graph and a heat map**( But it is not a real-time visualiszaition). And also there exists a lantency on TSI to update new data, which will be within 60s.
4. Flexibility – the solution is accessible via APIs. You can customize your visualization on the top of TSI.
5. Big data scalable, extremely suitable for when the number of devices exceeded several hundred thousand. Even POWER BI doesn't have the ability to do this.

### 2. Architecture
![TSI Architecture](https://github.com/icesuperbravo/Blogs/blob/master/time-series-insights/azure1.PNG?raw=true)

* Comparison between 'before TSI' and 'after TSI'
![Architecture before Azure TSI implementation](https://predica.pl/wp-content/uploads/2017/07/Original-architecture.png)  
Figure 1. Architecture before Azure TSI implementation.
![Architecture after Azure TSI implementation.](https://predica.pl/wp-content/uploads/2017/07/Changed-architecture.png)  
Figure 2. Architecture after Azure TSI implementation.

* It monitors trends of your IoT devices ONLY using line charts or heat maps. 
* Azure Time Series Insights only supports the IoT Hub and Event Hub as direct sources. 
* For data aggregation and visualization: both of them work along the time axis. We do not have the ability to create our custom metrics or edit data either.

### 3. Using Time Series Insights to expore your data
* 图形刷新频率
The data update interval is usually within 60 seconds. And it only automatically refresh the line graph of the belowing query sector. 
![auto-refresh](https://github.com/icesuperbravo/Blogs/blob/master/time-series-insights/time-series-insights.PNG?raw=true)
当要搜索的时间区域确定后，主界面所展示的line graph和heatmap是不会随时间自动刷新的。但搜索区域的索引line graph是会以约1分钟/次的频率刷新的，不过条件是将界面右上角的autofresh功能打开。

### Reference: 
1. https://predica.pl/blog/azure-time-series-insights-for-iot-devices/
