### Intro: 开篇先聊五毛钱天
**大爱无疆之感天泣地：为微软爸爸正名！就是今天了！**   
IoT实时数据可视化方案系列写（憋）到今天，终于来到了Power BI和Azure的领域。 聊起这两个赫赫有名的儿子，不得不提一提它们多金帅气的爸爸： Microsoft。 
虽然微软爸爸一直以十分体面精英的形象示人，一头金色飘逸的秀发迷倒众生，西装笔挺谈吐好不儒雅， 生意的版图也愈发宽广和稳固，大有一朝帝国吞吐山河的气势。但 人言可畏，众口难调。开源和独立开发圈子里总频频传出微软爸爸其实是个地中海秃头且是个暴发户的消息，名声并不显赫（是很不显赫- -）地位也偶遭鄙视（是时常遭嫌弃- -）。连我也有时候也怀疑（不是怀疑，简直就是快要相信），微软爸爸究竟是去植了发还是带着假发套，是不是金絮其外，败絮其中。  
但就在这时，突然有一天，我交到了一个身在企业级服务的好基友，此人却对微软爸爸无比崇拜，眼冒桃心。 这让我对微软爸爸的真实身份产生了强烈的好奇和兴趣。这时我拿出了在豆瓣天涯微博混迹时积累多年的追番/帖/热搜/扒皮的强大华丽堪比卓伟的狗仔技能树，对微软爸爸做了一番地毯式搜索。 然而结果令人惊艳！重磅消息重磅消息： 微软爸爸虽然那一头金发是染的！但人家不秃头，毛发健康且发色独具光泽，在企业级IT服务（特别时大体量级的企业级服务）方面有着卓越而突出的贡献和地位。  
被我误会多年秃头的微软爸爸，今天我要用大爱来感化你！用尊严来捍卫你！用我的实际行动支持你！我要带着你的两个儿子为你打call！今天的你在我眼里是zhui帅的！  
### 1. Azure生态圈和Power BI服务简介
确实从个人观点出发，在企业级服务和解决方案上，微软的表现比开源和独立开发上令人亮眼太多。而Power BI和Azure则分别在这个领域里各自扮演着他们极其重要的战略角色，承担起他们的服务职责。  
Azure开发生态圈作为企业级服务体系中的影响巨大，奠定基础的一环，为企业级开发方案提供了涵盖IaaS, Paas及SaaS不同层面的架构开发相关产品及服务；  
IaaS(Infrastructure as a Service)层包括了负载均衡（Load Balance），自动伸缩（auto-scaling），虚拟机（Virtual Machine）等基础设施服务；   
PaaS(Platform as a Service)拥有云服务（Cloud Service），移动服务（Mobile Service），网页应用部署（Website Deployment）等平台服务；  
SaaS（Service as a Service）则涵盖了如数据库（SQL， HDinsights...），IoT(Stream Analytics, IoT Hub, Event Hub)方面和数据分析可视化（Time Series Insights， Power BI）等不同领域的软件服务。
![Azure Dashboard](https://github.com/icesuperbravo/Blogs/blob/master/Power%20BI/azure.PNG?raw=true)
Power BI作为SaaS服务中的一项，是一套强大的商业智能分析及数据可视化工具， 能快速地将复杂的原始数据组织成直观有效的数据图表使得数据分析师或工程师能根据图表展示出的数据逻辑及趋势迅速进行决策，有效避免未来开发成本的增加，降低运作风险；    
而之所以说Power BI是一套服务，在于Power BI旗下产品又可细分为Power BI Desktop, Power BI Cloud, Power BI Mobile三种对不同平台所支持的服务。这三种产品在功能性上有较大的差异，但在使用上又保持着千丝万缕的联系。  
Power BI Desktop功能主要集中在创建功能强大的查询语句，数据模型和具有强交互性的数据报表；且可以将已完成的工作发布到Power BI Cloud进行云端共享或创建仪表盘（Power BI Desktop lets you build advanced queries, models, and reports that visualize data. With Power BI Desktop, you can build data models, create reports, and share your work by publishing to the Power BI service.）  
Power BI Cloud则集中于解决云端数据可视化方案，提供了仪表盘，数据警报，分享，流数据等诸多功能，同时兼容Desktop版本部分数据报表的功能；**而我们要讨论的实时数据可视化方案依靠于Power BI Cloud提供的流数据方案**。  
Power BI Mobile则主要解决移动设备上对已建立的数据报表和仪表盘的查看阅览问题, 显然移动端对编辑报表和仪表盘的限制目前还是较大的。  
将Power BI体系中的这几个工具组合起来使用，产生的功效是十分强大的。既能对非时间序列的数据集进行多角度展示，又能满足当下时代对实时数据可视化的强烈需求。   
使用Azure和Power BI能搭建一个完整的云端部署的可视化数据方案，让数据不在孤立于某个本地数据库或服务器中，在大数据时代下数据能够在云端有效共享，在终端设备多维展示，并能被实时分析，为推动公司方案决策，减少成本损失助力。
![Power BI Cloud Solution Architecture](https://github.com/icesuperbravo/Blogs/blob/master/Power%20BI/concept.PNG?raw=true)

### 2. 聊聊一个系列开篇就应该回答的问题：我们为什么需要实时数据可视化的方案？ 
在工业互联网时代到来的今天，大批的传统机械制造行业如石油，生产等都面临着严峻的生产设备和资产管理的数字转型（digital tranformation）。大部分工厂均为自己的设备配备了多维度的传感设备或遥感设备从而对自己的生产进程和设备健康进行监控和管理，而这些设备每天都将产生大量结构复杂且不易人类阅读的机器数据。这些机器数据将会被储存在不同的本地数据库中。大量的数据被孤立在本地不仅占用大量存储资源且无法为企业产生经济效益。为了解决这一痛点，首先这些数据需要被共享，以保证数据分析的正确性和利用最大化；其次数据应该能被实时流式处理，处理后的数据可以根据需要舍弃或保存；最后数据应该被统一的平台进行终端可视化，使得这些数据能快速被人类理解，分析以及基于数据进行预测。
信息化社会的迅猛发展早早就造就了一系列强大的传统数据分析和商业智能分析工具的诞生，这些软件大多采用ETL（Extract, Transform, Load）的传统方法从数据库加载数据到工具中再供用户进行操纵；由于受数据库读取和写入性能的限制，就算是在最完美的情况下，完成整个数据获取的过程也需要一分钟。 而工业级传感设备一般在每秒就能产生将近百万条的机器数据，数据频繁在数据库的更新要求分析工具连续地对数据库发出读请求，这样会造成数据库巨大的读写业务压力。因此大部分的传统数据分析工具（例如Tableau, Qlik）对实时数据可视化的支持非常不好，或者说甚至没有。 
![Traditional Method](https://github.com/icesuperbravo/Blogs/blob/master/Power%20BI/traditional-analytics.PNG?raw=true)
从理论分析来看，对数据响应而进行有效决策（actionable time-critical decision）的最佳黄金时间往往发生在秒级别（近乎实时）。 因此，这推动了我们获取一种让分析工具能更快更好获得数据的处理方法。   
![The diminishing value of data](https://github.com/icesuperbravo/Blogs/blob/master/Power%20BI/diminishing%20value%20of%20data.PNG?raw=true)
流式数据处理因而应运而生。这种处理方法能让数据处理表现几乎保持在实时。如果将数据比喻成水流，从数据源头流向数据终端，在这期间，我们在流经的某点建立起一座水进化处理工厂（即流式处理工具），对水流进行预先设置好的处理，在流经过程中完成整个处理过程，并提取聚合出我们对水流成分的感兴趣的一些信息，这样便能大大提高对数据处理的效率。而经过处理后的水流仍可以流向其终点，并使用传统的方法存入数据库供历史分析。  
![Streaming Method](https://github.com/icesuperbravo/Blogs/blob/master/Power%20BI/streaming-method.PNG?raw=true)  

[1]. Real-Time Event Processing with Microsoft Azure Stream Analytics;

### 3. 用Power BI构建实时数据可视化仪表板 
#### 3.1 Power BI接受的两种数据流入方法
Power BI作为商业智能分析工具的先驱和行业有利竞争者，似乎是敏锐地捕捉到这样的商机和市场需求，顺势推出了实时数据可视化的仪表盘，并且为了响应流式数据处理在IoT领域的强大需求，又推出了Azure Stream Analytics这一产品。使用Stream Analytics后能将数据无缝无延迟的推送到Power BI终端进行近乎实时的可视分析。而另一个使用该产品的好处是Stream Analytics能对数据进行预处理比如解析，聚合等，使得终端设备能够应对以各种形式组织的数据结构，大大增加了整个数据输入的横向可延展性（horizontal scalability）。  
另一种较之稍逊的方法是使用Power BI REST API直接将流数据推入Power BI中。这样做的缺点是，数据无法被预处理因此则要求产生数据的应用或数据库有能力将数据组织成Power BI能够识别的简单结构。否则Power BI将因无法识别数据而报错。  
还有一种叫做PubNub的方法局限性较大，在此不做讨论。
#### 3.2 基于云部署的三种Power BI实时数据可视化架构方案

***
3.2.1. 全云部署方案
![full-cloud](https://github.com/icesuperbravo/Blogs/blob/master/Power%20BI/fullcloud.PNG?raw=true)

性能指标：  
执行能力：4颗星；  
可伸缩性：4颗星；  
开发成本：2颗星；  
流数据处理能力：3颗星；  
在该情景下，我们首先将保存在本地数据库中的数据全部复制到Azure SQL数据库中。然后利用Azure虚拟机服务，云端部署应用，该应用主要业务逻辑为连续每秒向SQL数据库中拉取新数据并转换为JSON格式，以便连接的Event/IoT Hub进行后续处理。最后，我们使用Azure Stream Analytics服务读取IoT/Event Hub中的事件消息并将消息中的数据塑造成可用于分析的形态。所有这些的处理发生在实时或近乎实时，如果我们能将数据拉取的过程控制在每秒。  
这套方案将几乎全部依赖于微软的Azure服务。方案最大的特色是快速部署和低配置成本，这使得该方法具有高延展性和可移植性。通过仅仅几个步骤，就能使整个服务在几个小时内挂起运行。而所有你需要做的仅仅是将你的原始数据轻松嵌入Azure环境，Azure则会将数据自动实时“传播”到你的Power BI仪表盘。  
该方法的主要局限在于：
* 较高的运营成本；大量地使用了Azure内的服务产品，若每月24小时不间断运行该套方案，基本的每月成本将从100美元至上千美元不等；
* 由于存在将数据不间断复制进入云端数据库的操作过程，云端数据库可能存在较大的业务压力。而对每秒从数据库拉取新数据这一方法的实操性我暂保持怀疑态度；
***
3.2.2.Azure Event／IoT Hub +Azure Stream Analytics
![iot-stream](https://github.com/icesuperbravo/Blogs/blob/master/Power%20BI/eventhub+streamanalytics.PNG?raw=true)

性能指标:  
执行能力：4颗星；  
可伸缩性：1颗星；  
开发成本：3颗星；  
流数据处理能力：3颗星；  
一般而言，产生数据的终端通常是你使用的App。如果App本身有能力和外部网络进行通讯且你能够一定程度上控制App的行为，那么你就可能通过编码将数据直接推送至IoT/Event Hub，从而使得数据能够在云端共享。 
该方案明显的优点在于： 
* 削减了该方案对Azure云资源的依赖，因此使得运营成本也大大下降；  
* 这种方案由于直接将数据源接入Event/IoT Hub，使得从方案1中从数据源本地数据库存取数据到云数据库，然后再从云数据库中按每秒的速度拉取数据到Event/IoT Hub整个繁琐过程中产生的时间延迟完全消失了，因此可以看作是真正实时解决方案；  
而该方案主要的劣势集中在对数据的控制方面： 
如果想要对数据源做任何的修改控制，都需要在产生数据的应用或程序中添加逻辑业务，这大大限制了其对数据控制的灵活性；
***
3.2.3 Power BI REST API 
![rest-api](https://github.com/icesuperbravo/Blogs/blob/master/Power%20BI/restapi.PNG?raw=true)

性能指标:  
执行能力：2颗星；  
可伸缩性：1颗星；  
开发成本：4颗星；  
流数据处理能力：1颗星；  
最后，Power BI提供了REST API接口供用户控制和管理流式数据集。它允许用户将数据直接推送到Power BI并在此基础上建立可视化模块。不过你可能需要将你的应用在Azure Active Directory上注册以获得口令，然后用它来认证你流式数据的输入来源。  
在此方法中，明显优势表现在：  
* Power BI REST API使得运行成本显著降低，只涉及Power BI服务本身所产生的费用；
* 其开发成本也将大大降低，这得益于REST API的广泛流行。  
而该方案可预见的限制在于：   
* 必须在推入API之前将数据进行预处理，而数据产生中断通常并不是建立处理流数据逻辑的理想位置；
* 通过实践开发经验表明，Power BI目前对产品版本的持续更新可能影响到数据源连接，维护成本大大增加；
***
#### 3.3 小结：   
在这三种方案中，我亲自实验了第2种和第3种， 第一种方案由于成本和时间延迟方面的已知限制故而在选择之初就舍弃了。   
**在2，3的比较中，在我的案例中， 显而方案2的性价比都要优于方案3**。  
首先从成本方面考虑， 虽然方案3的成本仅仅包含使用Power BI Cloud产品所产生的费用，但由于Azure是公司产品开发的主要平台，因此使用部分Azure云资源完全是可负担且易得的；  
其次从实时性方面考虑，两种方案基本都能保持数据新鲜度和及时性，打成平手；  
最后从传播数据的可控性来说，方案2完败方案3； 由于Azure Stream Analytics的存在，其对从数据源流出数据的控制力还是十分强大的，你可以用SQL Query甚至自定义javascript snippet对流数据做一定的处理， 而方案3基本对数据控制是毫无能力的；  
[2]. [Build Real-Time Dashboard in Power BI](https://www.agilebi.com.au/blog/build-real-time-dashboard-power-bi) 
### 3. 玩转Power BI可视化
