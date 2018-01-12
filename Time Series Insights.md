>AZURE TIME SERIES INSIGHTS IS A FULLY MANAGED ANALYTICS, STORAGE, AND VISUALIZATION SERVICE THAT MAKES IT SIMPLE TO EXPLORE AND ANALYZE BILLIONS OF IOT EVENTS SIMULTANEOUSLY. IT GIVES YOU A GLOBAL VIEW OF YOUR DATA, LETTING YOU QUICKLY VALIDATE YOUR IOT SOLUTION AND AVOID COSTLY DOWNTIME TO MISSION-CRITICAL DEVICES BY HELPING YOU DISCOVER HIDDEN TRENDS, SPOT ANOMALIES, AND CONDUCT ROOT-CAUSE ANALYSES IN NEAR REAL-TIME.
* perfect for monitoring trends of your IoT devices using line charts or heat maps. 
* Azure Time Series Insights only supports the IoT Hub and Event Hub as direct sources. 
* Using Scenerios: 
However, this became problematic in terms of performance and cost generation when the number of devices exceeded several hundred thousand.
* Benefits:
1. Reducing the number of services, and therefore costs – thanks to replacing Stream Analytics and databases which we no longer needed
2. Simplicity – the whole logic of data aggregation is prepared in one tool  
**3. Real-time analytics – there is a live data preview via line graph and a heat map**
4. Flexibility – the solution is accessible via APIs
* For data aggregation and visualization:
The caveat/downside is:  both of them work along the time axis. We do not have the ability to create our custom metrics or edit data either.
![Architecture before Azure TSI implementation](https://predica.pl/wp-content/uploads/2017/07/Original-architecture.png)
Figure 1. Architecture before Azure TSI implementation.
![Architecture after Azure TSI implementation.](https://predica.pl/wp-content/uploads/2017/07/Changed-architecture.png)
Figure 2. Architecture after Azure TSI implementation.

reference: 
1. https://predica.pl/blog/azure-time-series-insights-for-iot-devices/
