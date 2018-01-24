### REST API vs HTTP API vs GraphQL
一句话概括REST： 用HTTP动词， 用URL定位资源
HTTP API则可以不受限与REST的构建规则而使用HTTP协议通讯；
GraphQL作为未来基友可能取代REST的API技术，是以数据为驱动的（具体还不了解其原理）

### 浏览器内核
**浏览器内核的本质＝渲染引擎＋JS解析引擎**  
但现在的所谈论的浏览器内核一般多指**渲染引擎**。
各大浏览器使用的渲染内核：
* IE： Trident
* Edge: EdgeHTML
* Safari: Webkit
* Chrome: ~~之前使用Webkit~~, 现在转投Blink怀抱
* Firefox: Gecko
* Opera： ~~之前使用自主研发的Presto~~, 现已投入Blink的怀抱

现在风头正盛的渲染引擎必属Blink了（Google出品必属精品），国内一众浏览器例如： QQ，360, UC等均使用了Blink引擎做页面渲染；    
而作为JS解析引擎，V8（Google出品必属精品）是一款强大的JS引擎，它极大地提高了javascript在浏览器端的运算速度；  
**因此Chrome好用的原因，主要来自于其背后强大的引擎系统： Blink+V8；**  
依此类推，可以列举出：  
Safari内核： Webkit+Niitro  
IE内核； Trident+Chakra  

### Node.js和npm的关系和区别
Node.js既不是后端框架，也不是javascript库。它封装了google的V8 Javascript引擎。能将javascript解析成机器语言，其性能和速度据说可以媲美C语言这种底层语言（不太确定）。因此Node.js更多地是被看做一种js的运行环境（runtime）， 它使得javascript的运用场景和应用范围更加广泛，使用javascript做全栈开发变得可能。   
npm是node环境中的包管理工具，会随着node.js的下载安装而同时安装。 使用npm工具从npm服务器中下载第三方代码或插件，能加速开发进程。 node社区的活跃使得npm服务器上的资源异常丰富，JS成为网站开发的宠儿，因此各种JS相关的资源都活跃在npm中。 因此，npm上的资源不再仅限于node相关(这意味着各种前端相关的资源同样也能在npm上找到？）。  
顺带聊一下webpack,grunt,gulp这样的工具。  
如果后端不使用，是否能使用这样的自动化工具呢？   
答案是肯定的，虽然这些工具都是基于node编写的，但这些工具都是做预编译的工具，目的是为了得到理想的源码。 





