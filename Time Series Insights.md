>AZURE TIME SERIES INSIGHTS IS A FULLY MANAGED ANALYTICS, STORAGE, AND VISUALIZATION SERVICE THAT MAKES IT SIMPLE TO EXPLORE AND ANALYZE BILLIONS OF IOT EVENTS SIMULTANEOUSLY. IT GIVES YOU A GLOBAL VIEW OF YOUR DATA, LETTING YOU QUICKLY VALIDATE YOUR IOT SOLUTION AND AVOID COSTLY DOWNTIME TO MISSION-CRITICAL DEVICES BY HELPING YOU DISCOVER HIDDEN TRENDS, SPOT ANOMALIES, AND CONDUCT ROOT-CAUSE ANALYSES IN NEAR REAL-TIME.
1. Concepts: 
**Azure TSI=database+query system+visualization layer**  
* Benefits:
1. Reducing the number of services, and therefore costs(cost effective) – thanks to replacing Stream Analytics and databases which we no longer needed;
2. Simplicity(Full-managed, highly integrated and an out-of-the-box solution) – the whole logic of data aggregation is prepared in one tool; 
**3. Real-time analytics – there is a live data preview via line graph and a heat map**( But it is not a real-time visualiszaition). And also there exists a lantency on TSI to update new data, which will be within 60s.
4. Flexibility – the solution is accessible via APIs. You can customize your visualization on the top of TSI.
5. Big data scalable, extremely suitable for when the number of devices exceeded several hundred thousand. Even POWER BI doesn't have the ability to do this.





* perfect for monitoring trends of your IoT devices using line charts or heat maps. 
* Azure Time Series Insights only supports the IoT Hub and Event Hub as direct sources. 

* For data aggregation and visualization:
The caveat/downside is:  both of them work along the time axis. We do not have the ability to create our custom metrics or edit data either.
![Architecture before Azure TSI implementation](https://predica.pl/wp-content/uploads/2017/07/Original-architecture.png)  
Figure 1. Architecture before Azure TSI implementation.
![Architecture after Azure TSI implementation.](https://predica.pl/wp-content/uploads/2017/07/Changed-architecture.png)  
Figure 2. Architecture after Azure TSI implementation.

reference: 
1. https://predica.pl/blog/azure-time-series-insights-for-iot-devices/
