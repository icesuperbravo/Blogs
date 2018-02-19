### Intro: 开篇先聊五毛钱天
**大爱无疆之感天泣地：为微软爸爸正名！就是今天了！**   
IoT实时数据可视化方案系列写（憋）到今天，终于来到了Power BI和Azure的领域。 聊起这两个赫赫有名的儿子，不得不提一提它们多金帅气的爸爸： Microsoft。

![hansome microsoft](https://media.giphy.com/media/WnmuS2R8x7ZwQ/giphy.gif)  
虽然微软爸爸一直以十分体面精英的形象示人，一头金色飘逸的秀发迷倒众生，西装笔挺谈吐好不儒雅， 生意的版图也愈发宽广和稳固，大有一朝帝国吞吐山河的气势。但 人言可畏，众口难调。开源和独立开发圈子里总频频传出微软爸爸其实是个地中海秃头且是个暴发户的消息，名声并不显赫（是很不显赫- -）地位也偶遭鄙视（是时常遭嫌弃- -）。连我也有时候也怀疑（不是怀疑，简直就是快要相信），微软爸爸究竟是去植了发还是带着假发套，是不是金絮其外，败絮其中。  
但就在这时，突然有一天，我交到了一个身在企业级服务的好基友，此人却对微软爸爸无比崇拜，眼冒桃心。 这让我对微软爸爸的真实身份产生了强烈的好奇和兴趣。这时我拿出了在豆瓣天涯微博混迹时积累多年的追番/帖/热搜/扒皮的强大华丽堪比卓伟的狗仔技能树，对微软爸爸做了一番地毯式搜索。 然而结果令人惊艳！重磅消息重磅消息： 微软爸爸虽然那一头金发是染的！但人家不秃头，毛发健康且发色独具光泽，在企业级IT服务（特别时大体量级的企业级服务）方面有着卓越而突出的贡献和地位。  
被我误会多年秃头的微软爸爸，今天我要用大爱来感化你！用尊严来捍卫你！用我的实际行动支持你！我要带着你的两个儿子为你打call！今天的你在我眼里是zhui帅的！ 

![on call](https://media.giphy.com/media/VgIums4vgV4iY/giphy.gif)
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

### 2. 聊聊这个系列开篇就应该回答的问题：我们为什么需要实时数据可视化的方案？ 
在工业互联网时代到来的今天，大批的传统机械制造行业如石油，生产等都面临着严峻的生产设备和资产管理的数字转型（digital tranformation）。大部分工厂均为自己的设备配备了多维度的传感设备或遥感设备从而对自己的生产进程和设备健康进行监控和管理，而这些设备每天都将产生大量结构复杂且不易人类阅读的机器数据。这些机器数据将会被储存在不同的本地数据库中。大量的数据被孤立在本地不仅占用大量存储资源且无法为企业产生经济效益。为了解决这一痛点，首先这些数据需要被共享，以保证数据分析的正确性和利用最大化；其次数据应该能被实时流式处理，处理后的数据可以根据需要舍弃或保存；最后数据应该被统一的平台进行终端可视化，使得这些数据能快速被人类理解，分析以及基于数据进行预测。
信息化社会的迅猛发展早早就造就了一系列强大的传统数据分析和商业智能分析工具的诞生，这些软件大多采用ETL（Extract, Transform, Load）的传统方法从数据库加载数据到工具中再供用户进行操纵；由于受数据库读取和写入性能的限制，就算是在最完美的情况下，完成整个数据获取的过程也停留在分钟级别。 而工业级传感设备一般在每秒就能产生将近百万条的机器数据，数据频繁在数据库的更新要求分析工具连续地对数据库发出读请求，这样会造成数据库巨大的读写业务压力。因此大部分的传统数据分析工具（例如Tableau, Qlik）对实时数据可视化的支持非常不好，或者说甚至没有。 
![Traditional Method](https://github.com/icesuperbravo/Blogs/blob/master/Power%20BI/traditional-analytics.PNG?raw=true)
从理论分析来看，对数据响应而进行有效决策（actionable time-critical decision）的最佳黄金时间往往发生在秒级别（近乎实时）。 因此，这推动了我们获取一种让分析工具能更快更好获得数据的处理方法。   
![The diminishing value of data](https://github.com/icesuperbravo/Blogs/blob/master/Power%20BI/diminishing%20value%20of%20data.PNG?raw=true)
流式数据处理因而应运而生。这种处理方法能让数据处理表现几乎保持在实时。如果将数据比喻成水流，从数据源头流向数据终端，在这期间，我们在流经的某点建立起一座水进化处理工厂（即流式处理工具），对水流进行预先设置好的处理，在流经过程中完成整个处理过程，并提取聚合出我们对水流成分的感兴趣的一些信息，这样便能大大提高对数据处理的效率。而经过处理后的水流仍可以流向其终点，并使用传统的方法存入数据库供历史分析。  
![Streaming Method](https://github.com/icesuperbravo/Blogs/blob/master/Power%20BI/streaming-method.PNG?raw=true)  

[1]. Real-Time Event Processing with Microsoft Azure Stream Analytics;

### 3. 用Power BI构建实时数据可视化仪表板 
#### 3.1 Power BI接受的两种数据流入方法
Power BI作为商业智能分析工具的先驱和行业有利竞争者，似乎是敏锐地捕捉到这样的商机和市场需求，顺势推出了实时数据可视化的仪表盘，并且为了响应流式数据处理在IoT领域的强大需求，Azure又推出了Stream Analytics这一产品。使用Stream Analytics后能将数据无缝无延迟的推送到Power BI终端进行近乎实时的可视分析。而另一个使用该产品的好处是Stream Analytics能对数据进行预处理比如解析，聚合等，使得终端设备能够应对以各种形式组织的数据结构，大大增加了整个数据输入的横向可延展性（horizontal scalability）。  
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
在这三种方案中，我亲自实验了第二种和第三种， 由于第一种方案成本和时间延迟方面的明显已知限制故而在选择之初就舍弃了。   
**而在方案2，3的比较中， 从公司需求和资源方面的角度考虑，方案2的性价比要优于方案3**。  
首先从成本方面考虑， 虽然方案3的成本仅仅包含使用Power BI Cloud产品所产生的费用，但由于Azure是公司产品开发的主要平台，因此使用部分Azure云资源完全是可负担且易得的；  
其次从实时性方面考虑，两种方案基本都能保持数据新鲜度和及时性，打成平手；  
最后从传播数据的可控性来说，方案2完败方案3； 由于Azure Stream Analytics的存在，其对从数据源流出数据的控制力还是十分强大的，你可以用SQL Query甚至自定义javascript snippet对流数据做一定的处理， 而方案3基本对数据控制是毫无能力的；  
因此以下章节的所有的可视化效果将均来自于方案2的架构，以后不再赘述；  
[2]. [Build Real-Time Dashboard in Power BI](https://www.agilebi.com.au/blog/build-real-time-dashboard-power-bi) 

### 4. 玩转Power BI实时可视化
现在我们已经有了一个稳定的数据流和一个完整的云端架构体系, 接下来就到了各位的表演时间了！利用Power BI创建仪表盘和报表的操作十分简单直接，在搭建好环境后，自己摸索一下，几乎就可以上手了。    
因此，我就根据自身的需求使用Power BI Cloud创建了一个供测试的实时监控仪表盘demo。  
![I am a demo](https://github.com/icesuperbravo/Blogs/blob/master/Power%20BI/all_dashboard.gif?raw=true)  
不得不说还是Power BI数据流动的动态效果和整个界面简洁的设计感真是让人赏心悦目！接下来我们就来聊一聊Power BI在实时可视化这一领域究竟有哪一些独特之处！ 
* Power BI实时可视化特色1： 为流数据集而定制的流畅动画效果显示（Smooth Animation Effect for Streaming Dataset）    
我敢说，在做了无数可视化产品调研后，Power BI依旧是那个唯一拥有如此**流畅**的数据流动效果的产品。  
![Smooth Animation](https://github.com/icesuperbravo/Blogs/blob/master/Power%20BI/smooth_animation.gif?raw=true)  
这种丝滑的视觉体验主要表现在线性图中， 可以看到x时间轴会随着当前时间而移动，Power BI会根据每个时间点录入的数据产生平滑的曲线，并以一种连续流畅的动画效果呈现出来。这是市面上很多宣称自己是实时可视化的产品都无法达到的效果。   
* Power BI实时可视化特色2： Current + Old Data Access = Push + Streaming Dataset（Push and Streaming Dataset for Live Dashboard）   
根据Power BI的官方文档描述，能达到特色1中这样近乎完美的动态效果主要得益于Power BI内部的Redis Cache。而我们称这种可以近乎实时展示的数据集为Streaming。在Streaming Dataset中，流入的数据将被暂时保存在Power BI内嵌的Redis Cache中，仅对存入的数据进行缓存而不涉及ETL过程。Cache采用先进先出（FIFO）的策略，永远只保留最新流入的前20000行数据记录。 这是为什么这种数据集能保证数据到达**几乎无延迟显示即实时显示**的重要原因。  
但正是因为这种完美的实时效果，这种技术也存在很大的局限性： 首先，这种技术只能保留最新的前20000行数据也意味着在Streaming数据集为基础上建立的可视化组件最大的时间窗口大概为1小时，因此对历史数据的支持性极差；另一方面，Power BI目前针对Streaming Dataset仅仅提高极小范围的可视化组件的选择： Line Chart，Stacked Bar Chart,Stacked ColumnChart, Gauge, Card，且这些图表上供可自定义的操作十分有限，几乎只能更改图标标题和一些辅助文字。  
![Streaming_Limit](https://github.com/icesuperbravo/Blogs/blob/master/Power%20BI/streaming_dataset.gif?raw=true)   

我们在前面的章节介绍过这张图，对于分析决策而言，尽管实时数据更有价值且更有助于进行有效决策，但是如果能将历史数据和实时数据进行结合使用，则能发挥更大的利用价值。 因此为了让Power BI同样支持对流数据的历史数据分析，Power BI还提供了一种名为Push的数据集。   
![The diminishing value of data](https://github.com/icesuperbravo/Blogs/blob/master/Power%20BI/diminishing%20value%20of%20data.PNG?raw=true)  
Push数据集不同于Streaming使用Redis Cache来缓存数据；为了保证所有数据的永久保存，它使用了SQL数据库作为储存工具。 因此在数据延迟方面将会体验到3-5s的滞后（time lag）。在不过分追求完全实时且对历史数据可得性有需求的情况下，使用Push数据集会是个不错的选择。  
**当然，最完美的方法是同时使用Push和Streaming两种数据集，在要求精准实时展示的数据上使用Streaming Dataset，而对这种需求不强烈而对历史数据有要求的数据使用Push Dataset。**
* Power BI实时可视化特色3： 报表和仪表盘分离，各自承担不同角色
![Report vs Dashboard](https://github.com/icesuperbravo/Blogs/blob/master/Power%20BI/report_dashboard.PNG?raw=true)
而提到这两种不同的数据不得不提到另外两个在Power BI中难舍难分的概念： 仪表盘和报表。很多人在使用Power BI之初会经常搞混这两个工具。主要原因是它们同样作为各种可视化组件展示的地方，但提供的功能却有许多的不同之处。在刚刚接触Power BI Cloud这一工具时，我经常会一脸懵逼地混淆他们， 不理解为什么Power BI非要做出两个如此相似却又如此不同的工具。但当我的论文进行到一半时，我开始能渐渐理解做这两个功能的初衷。 不过不得不说，因为这两个工具的存在，也增加了Power BI工具使用的复杂程度。**如果站在产品经理的角度来说，这样非常模糊的功能分区是对用户十分不友好的。**  
那么现在来说说，报表和仪表盘究竟有哪些不同。报表（Report），一般针对于静态数据来源的可视化组件展示，它的特点在于不仅能对数据进行基本的可视化展示，还能完全支持**对每个组件更深入的交互式操作以便用户进一步的数据分析**。这些分析包括使用过滤器对数据做基本的筛选可视，查看图表中包含的原始数据等等。  
对于实时可视化的支持方面，报表支持流数据中的Push Dataset作为数据源建立图表, 这样一来用户就可以针对历史数据做更多更深层次的分析挖掘潜在的数据特征。但报表中建立的基于Push的可视化组件都无法自动刷新，而只能采取手动刷新的形式获得新的数据。如果想要让这些可视化图表对每次存入的新数据自动刷新，必须要将报表中的图形以pin的方式添加到仪表盘中。  
![Pin](https://github.com/icesuperbravo/Blogs/blob/master/Power%20BI/pin.gif?raw=true)
而仪表板的主要功能分区在于完整的展示数据可视化图形以及构建一个基于云的可分享的数据展示地，这也意味着添加到仪表板的图形组件大多都无法支持更深入的交互操作，仅供展示。每个仪表盘都可以在权限管理控制下进行分享，或干脆将整个仪表盘发布，使所有人都能通过特定的URL来访问。  
同样对于实时可视化的支持而言，仪表盘支持同时来此Push和Streaming数据集流入的数据。对于Streaming数据集，除了在特色2中受到的诸多可视化类型和自定义方面的限制，同样不支持深入的交互式操作。而Push数据集本身在报表中是支持交互操作的，*但如果将基于Push数据集的在报表中的图形pin到了仪表盘，那么在仪表盘的那个图形就不再支持交互式分析了即只提供纯实时数据展示的功能（且默认了每次实时刷新数据延迟3-5s)。*   
**因此对于实时可视化来说，在Power BI Cloud中如果想要有交互和分析的支持就选择用报表，如果仅仅作为数据展示的地方那么久一定用仪表盘，不存在一个工具是可以既能展示实时数据变化又能提供更多针对图表交互分析的**。有些情况下，可能会因为仪表盘中对实时数据展示的图表种类过于有限，而希望使用报表中种类丰富的可视图形，那么就一定要记得将报表中的图形经pin方法放到仪表盘中去，不过这种方法的使用前提是： 要接受一定程度数据的延迟。  
听起来这一系列操作是不是就足够复杂了呢？除此之外，使用Power BI的同学们还要牢记一点，**仅仅只有Power BI Cloud这个服务是支持流数据可视化的**，也就是说Mobile和Desktop系列都不会支持实时数据的可视化。而其主要原因还是从功能性出发来分析：Mobile主要支持浏览，可以从移动端查看实时数据仪表盘，但不承担编辑工作；而Desktop主要是对报表的编辑和浏览做支持，自然而然也不会让用户对实时数据这一方面有过多的期待。  
这些历史原因让实时数据可视化这样的一个功能在Power BI的体系中变得异常尴尬，似乎不论在Power BI哪个平台的产品中，实时数据都很难找到一个包容友好，对历史数据和实时展示功能完全支持的环境。这种情况的产生主要原因是Power BI从创始之初就将自己定位成一款*商业智能分析可视化软件*而并非一个*IoT数据实时可视化分析软件*，因此大多数功能都针对传统的静态数据而设计。但因今年物联网技术的迅猛发展，产生的大量机器数据被展示和分析的需求被无限扩大。Power BI团队这才后续做了这样一个功能使得Power BI同样能支持实时数据的可视化。但由于Power BI产品功能模块的设计早已成型，这才使得流数据可视化的位置在Power BI中显得无比尴尬。  
另外还有一点需要做说明的是：对于每一个数据集（Dataset）只能建立一个针对该数据集的报表，Power BI不允许在一张报表上混合来自不同Dataset的数据；而仪表盘则与之相反，允许将来自不同报表或流数据的可视化图形相互混合。当单击由某个报表的pin来的图形组件时，Power BI将导航至该报表以便用户更深入的探索数据。  

### 5.总结
父老乡亲们！！叔叔阿姨们！！爷爷奶奶们！！当我写到总结两个字的时候，我内心充满了无限的激动！  
![happy_ending](https://media.giphy.com/media/3ohs4k9pD1lpKWB6ec/giphy.gif)  
![happy_ending2](https://media.giphy.com/media/xTiN0CNHgoRf1Ha7CM/giphy.gif)  
对于Power BI，我总是抱着又爱又恨的态度。一方面，整个产品的设计界面，交互报表和实时数据流动性的展示真的做的很好；而另一方面，实时数据可视分析的功能始终无法媲美专业的IoT实时数据可视分析工具（尽管市面上能找到的专业工具也相当有限）。加之Power BI各种平台和各种数据源对功能的支持不尽相同，让使用Power BI的过程变得特别长，因为在构建图表之前，你总要大量的翻阅文档以支撑最后可以达到的实际效果。  
Power BI社区目前已拥有24.9k的发帖量，总的来说保持着高度活跃的氛围；与此同时Power BI的技术团队对产品的更新迭代也一直在进行之中并保持着频繁的版本更新速度。随着实时信息在信息社会的分量越来越重，使用可视化工具的用户对这样的需求越来越强烈，我有理由相信，Power BI未来对实时数据可视或分析的能力也会越来越强。也许到某一天，微软甚至会将这一功能从Power BI中分离出来而单独做一款这样的工具。而目前在这个领域，还没有特别成熟的工具能够占据主要的市场份额。对微软，我充满了一个工程师对新工具无限的期待和未来的展望（希望微软爸爸看到这里能给我打红包）。   
好了，该有的赞美都有了，该吐槽的也都吐槽完毕了。希望这会是一篇对Power BI合格的作业。如果能帮助到任何人，我会感到十分的开心和荣幸。（如果微软爸爸能看到，我会开心到灰起来吧！）
