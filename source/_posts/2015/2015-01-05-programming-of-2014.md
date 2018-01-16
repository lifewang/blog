---
title: 2014 年度小结（技术方面）
permalink: 1976
tags:
  - Node.js
  - 单元测试
  - 软件工程
  - 年度小结
date: 2015-01-05
---

2014 年的第一个项目是一个有关比特币交易的系统，规模并不大。

这是我除了 Hello World 之外的第一个 Node.js 项目，也是我第一次写 CoffeeScript. 简单地看了一遍「CoffeeScript 小书」，又随便搜了搜对 CoffeeScript 的评价，大家说得最多的是「CoffeeScript 嘛，哪有什么语法，想怎么写就怎么写就行了」，说起来倒还真是如此，差不多只花了两个小时就学会了 CoffeeScript, 而且之后几乎没在这上面遇到什么坑。

说起 CoffeeScript, 似乎在 2012 年中旬，whtsky 牛就开始学习了，并且在博客上发了两篇文章，虽然 CoffeeScript 很简单，但这也可见 whtsky 总是站在潮流浪尖。

虽然之前一直对比特币很是关注，但对比特币的交易规则其实还是一知半解，其实比特币交易平台的工作模型和股票是相似的——说起来在此之前我也不知道股票是如何工作的。因为对这个项目业务逻辑的知识了解不够充分，所以这个项目我差不多是只写了个开头，就由别人完全接手了。

- - - -

第二个项目是也是有关比特币的，一个 Web 系统，也是 Node.js.

因为这时搬到了苏州，有很多的时间和小明交流，所以总算是对股票的工作方式，以及相似的比特币交易平台的工作方式，有了一个比较深入的了解。

当一个 Web 系统的规模稍大一些，比如有几十个 API, 以及几个比较大块的业务逻辑；再对这个系统进行重构就非常困难了，但碰巧我又总是在重构——这有主观原因也有客观原因，客观原因就是毕竟我初学 Node.js, 还在探索所谓的「最佳实践」，免不了要走一些弯路。于是在这个系统主体已经完工的时候，我开始着手引入自动测试。

说起自动测试，在此之前，我无数次地听到这个词。我知道这是一种先进的开发技术，但不知道究竟如何应用，也不知道用好了之后会有怎样的效果。在 LightPHP 上我做过一些探索，但感觉大部分模块因为有复杂的依赖关系，不容易编写单元测试；而为简单的模块编写单元测试又没有带来实际的正面影响。理想的情况下，应当将程序划分为模块，然后对每个模块或者说单元进行测试。但实际上大多数情况下，我还是没能彻底地剥离掉模块之间的依赖关系，所以更多的时候我在使用「自动测试」这个词，而不是「单元测试」。

所以，还是老问题，剥离模块之间的依赖关系令我非常头痛。虽然在这个项目上，后来还是做到了为绝大部分功能编写测试，但是用了很多不够优雅、不够健壮的实现方案，导致测试非常容易出问题，而且出了问题之后往往要进行大幅的修改才能解决，且测试代码之间也有错综复杂的依赖关系。

- - - -

然后依然是一个有关比特币的交易系统，依然 Node.js.

这是一个自动交易系统，整个系统每时每刻都在进行大量的计算，基本上占用了服务器的几乎所有资源。这个项目的代码量并不大，但是逻辑密集，计算量大，对性能有一定要求 —— 事实上这差不多是我做过的唯一对性能敏感的项目，因为大多数项目的用户量实在太少了，根本谈不上优化性能。

为了能让算法逻辑更清晰，也为了找出改善性能的关键点，这个项目前前后后重构了很多次。在最后一次重构后，似乎效果还不如之前，不过因为比特币的价格一路在跌，这个项目被暂时搁置了，最后的一个版本开始在无人看管的状态下继续吃 CPU. 但是这不影响比特币继续一路下跌，终于在最近，这个项目被彻底关掉了——说起来比特币差不多是 2014 年度最差的投资品了。

这个项目使用了 MongoDB 作为数据库，程序差不多是在虐待数据库 —— 我没有花太多时间来对数据库进行优化，连索引也是随便想当然建的，然后程序每秒钟都在写入和读取数据，以及一些没有被很好地优化的聚合查询。不过 MongoDB 在这半年间完全没有出过问题，让我对 MongoDB 好感倍增；说起来 RP 主机上的 MySQL 曾经出过无端丢数据的情况，再加上毕竟 MySQL 的作者已经不建议我们使用 MySQL 了，顿时觉得 MySQL 的前途一片灰暗。

- - - -

之后开始我们（指 [番茄土豆团队](http://hackplan.com/), 下同）开始着手重写之前 PHP 版本的 [番茄土豆](https://pomotodo.com). 因为之前在设计上考虑不充分，在用户量增加了之后，出现了一些性能问题，为了系统性地解决性能和其他的一些问题，索性不如直接用 Node.js 和 MongoDB 进行重写，而不是在原来的 PHP 版本上再修修补补。做出这个决定也是因为这时候我们大概用了半年 Node.js, 相比于 PHP, 我们觉得基本上只有优势，而没有发现有什么不如 PHP 的地方，于是希望将原有的 PHP 项目都改为 Node.js.

这次重写主要是其他人完成的，我只是稍微参与了一下，写了其中几个小的功能点。这是我第一次使用 Mongoose, 之前我认为既然 MongoDB 的特点是无模式，那么何必非要用一个 ORM 重新定义模式呢；后来我又稍稍改变了一点想法，确实 MongoDB 的 API 提供的是一种较为底层的数据库操作，还是需要一些辅助的功能来更好地完成业务逻辑，例如字段的检查器、在文档上定义实例方法等。

Mongoose 差不多是 Node.js 社区最主流的 MongoDB ORM, 选择它是一个没有悬念的事情。但用了一阵 Mongoose 之后我发现，虽然 Mongoose 设计了一个美丽的图景，但在细节上坑实在太多了。比如它虽然提供了在文档间定义引用关系和嵌入关系的方法，但这个功能非常弱；另一方面因为它用了一些比较 hack 的方式来实现对字段的验证，这导致又没有办法自由地修改从数据库中取出的文档，例如自己来实现引用关系，这给向视图传递数据造成了一些困难。

总之，在我使用 Mongoose 的过程中，总是有一种自己重新造一个轮子的冲动，但我又没有把握设计得更好，需要很努力地克制这种冲动 —— 好吧，其实我连给这个轮子的名字都想好了。

在 Node.js 版基本完成后，如何将新版本部署上线成了一个很大的问题，这个问题困扰了我们几个月的时间。番茄土豆在 2014 年初也上线了一个重写的版本，但那次的情况要简单得多，一个晚上就基本搞定了。而这次因为除了 Web 版之外还有几个平台的客户端，需要保证这些客户端所使用的 API 依然可用，这就要求新版本的上线过程必须是持续的、平滑的，新旧版本需要共存一段时间，目前我们还在逐步完成有关新版本上线的工作。

- - - -

我们给番茄土豆设计了一个「周报」的功能，会在每个周末向用户的邮箱发送一周的工作报告，这个工作由我负责，但这差不多是我 2014 年度完成得最不好的一个项目，前前后后花费了很多时间，但还是错误百出。

说起来也简单，无非是每周运行一次：从数据库查到数据、生成统计数据、渲染邮件、发送邮件，但每个步骤都出了很多问题。首先要保证这个任务每周运行一次就花了一些功夫，因为番茄土豆的用户来自不同的时区，所以需要在当地时间每周日早上来发送这封邮件，这就将「每周一次」变成了「每周 24 次，每次完成一部分」。而邮件一旦发出又不能撤回，试错有很大的代价 —— 在这个项目上我出现了太多次严重的失误。

因为这是我们第一个与邮件相关的工作，因此之后大部分与邮件相关的工作也归我了。我围绕着邮件写了一些一般化的库，比如 [pomo-mailer](https://github.com/HackPlan/pomo-mailer) 和 [pomo-sender](https://github.com/HackPlan/pomo-sender). 前者用于渲染涉及多语言的邮件，后者是一个考虑了时区和定时任务的邮件队列。

在实现邮件队列上，我遇到了一些有关 Node.js 异步流程控制的坑。在 PHP 和 Node.js 中，都不需要我们人工地创建和管理线程，因此之前从 C++ 上学习到的有关多线程编程的知识也快忘光了 — —或者说那些知识其实根本没实践过。直到年末看了 [JavaScript 异步编程](http://www.amazon.cn/gp/product/B00CYM0Z8Y/ref=as_li_ss_tl?ie=UTF8&camp=536&creative=3132&creativeASIN=B00CYM0Z8Y&linkCode=as2&tag=jysperm07-23) 这本书之后才基本掌握了如何在 Node.js 中优雅地控制异步流程。

- - - -

[RootPanel](https://github.com/jysperm/RootPanel) 是贯穿我 2014 整年的一个项目，也贯穿我学习 Node.js 的整个过程。

在之前写 PHP 的时候，当需要写前端 JavaScript 时总是非常苦恼，因为 JavaScript 语言的设计并不全然合理，浏览器间又有不兼容的拓展，再加上市面上全是些不靠谱的 [21 天学通 JavaScript](http://www.amazon.cn/gp/product/B00HRC6AVC/ref=as_li_ss_tl?ie=UTF8&camp=536&creative=3132&creativeASIN=B00HRC6AVC&linkCode=as2&tag=jysperm07-23) 教程。所以在一开始使用 Node.js 的时候我也对 JavaScript 比较抗拒，加上 CoffeeScript 屏蔽了 JavaScript 语言的一些细节，所以在最开始的一段时间，我对 JavaScript 的了解其实很少。例如原型系统、真假值表什么的都是后来才系统地了解。

RootPanel 3 被我定义为「一个插件化的 PaaS 开发框架」，实现彻底地插件化是最重要的一点。2013 年末的时候我已经开始尝试用 PHP 实现 RP3 了，但非常困难，主要是因为 PHP 毕竟还是传统的面向对象架构，正统的方式是通过类的继承、定义接口来实现插件化，这就导致大量的代码是在维护这种「模式」而不是专注于业务逻辑。JavaScript 就好像无模式的 MongoDB 一样，PHP 中的类、对象、数组、函数，在 JavaScript 中都是 object, 可以自由地添加和读取属性，以实现在运行时拓展功能。当然 JavaScript 的灵活性也导致了我作为一个 Node.js 新手，一开始花了很多时间去探索什么才是好的设计模式，浪费了很多时间，尤其是浪费了很多时间在重构 RootPanel 上。

在 2014 年 8 月，因为 us1 被反复 DDoS 直到下线。我不得不加快了 RP3 的开发，在之后的三个月里，快速地发布了几个版本，还节外生枝地发布了一个 GreenShadow. 在之后，尤其最近两个月，RP3 的进度明显慢了下来，主要原因是我对插件系统的设计依然不理想，还在继续探索更好的实现方式；目前 RootPanel 的版本号是 0.8, 希望在新的一年里我能将插件化的实现方式确定下来，发布 1.0 版。

- - - -

在 2014 下半年，我断断续续地看完了 [SQL 反模式](http://www.amazon.cn/gp/product/B005N4L03E/ref=as_li_tf_tl?ie=UTF8&camp=536&creative=3200&creativeASIN=B005N4L03E&linkCode=as2&tag=jysperm07-23), 这本书中列举了一些好的和不好的数据库设计模式。说起来我的 SQL 基础非常不扎实，基本上也就会个增删查改，从未系统性地学习过 SQL. 我突然开始反思，是否是因为我只用到了 MySQL 众多功能中很小的一部分，所以才觉得关系性较弱、无模式的 MongoDB 更好用呢。于是我开始尝试系统地学习 SQL, 但似乎 SQL 本来就不是一个系统的语言，有大量「取决于实现」的细节。所以我其实也只是先补习了一下之前了解很少的子查询、GROUP BY, 以及 JOIN.

这时，我们希望将番茄土豆中的订单和支付系统独立出来，用 Node.js 重写，我决定在这个项目中使用 MySQL.

这个订单系统是我第一次在一开始就引入单元测试的项目。因为我们一直都是前后端独立开发，所以在此之前，我都是通过 Postman 在测试我的程序。因此经常发生这样的情况：在开发完成一个功能后，测试没有问题，但之后因为改动其他部分而产生了问题，这种情况往往只有到前端开发用到这个接口的时候才会发现，因为我们团队都是远程工作，经常发生这样的事情会对工作效率有一些负面的影响。而在重构之后这个问题更加严重，往往要重新测试所有接口来确认重构没有对其造成影响。

而如果从一开始就引入单元测试，开发就变得容易得多，开发的大部分时间就是在看单元测试的结果而已，一旦单元测试显示通过，那么你就知道程序至少在按照你单元测试中写清的规则在运行。有人认为编写单元测试需要花费额外的时间，进而觉得很不值得，其实不然，开发一个程序终究是需要测试的，单元测试会将原本需要人工测试的步骤自动化，以便可以随时完整地重新运行所有测试。只要探索出了正确的方法，编写单元测试并不会比人工测试花费更多的时间，而且单元测试会有一项额外的好处：测试的步骤被存档了下来，而且会进入源代码的版本控制中。

当然，为了能够编写单元测试，是需要在设计项目结构上花一些功夫的。前辈们在这一点上的经验总结起来就是三个字母 —— MVC. 之前我一直错误地在 Controller 中包含了太多的逻辑，比如在 Controller 中实现大部分的错误处理。其实这通常也不会有太大问题，但一旦引入了单元测试，这种架构就暴露出了问题。在 Web API 中往往一个接口包含了一组逻辑，如果在 Controller 中包含这些逻辑就会出现一些重复，这些重复的逻辑没办法被抽象成一个函数。更严重的是因为在单元测试中需要构造一些特定的环境，如果通过调用 Web API 的方式来实现会非常繁琐，因为 Web API 往往是被保护在用户认证、权限认证之后的。所以更正确的方式是尽可能在 Model 中实现大部分的逻辑，以便被划分成更细粒度的单元，被单元测试直接使用。

Node.js 上主流的 MySQL ORM 应该是 Sequelize, 不过我在这个项目中本着「步子不要迈太大」的原则，并没有使用 ORM, 也没有使用 MySQL 的外键和事务，这些功能估计要在新的一年里去探索了。

- - - -

我们团队的前端项目一直在使用 AngularJS, 如果我还在写 PHP 的话，那这应该和我关系不大。不过既然已经掌握了 JavaScript, 就不如尝试一下。于是买了一本 [JavaScript Web Applications](http://www.amazon.cn/gp/product/B0082226FU/ref=as_li_ss_tl?ie=UTF8&camp=536&creative=3132&creativeASIN=B0082226FU&linkCode=as2&tag=jysperm07-23) 学习如何在前端实现 MVC. 这本书简单地介绍了 Backbone 这个框架，我发现相比于 AngularJS 我更喜欢 Backbone 这种侵入式弱，定制型强的轻量级框架。于是我读了一遍 Backbone 仅有 2000 余行的实现，并决定在新的一年里用 Backbone 来重构 RP3 的前端。

- - - -

2014 年的最后一个项目也是一个 Node.js 的 Web 系统。

这个项目也是从一开始就引入了单元测试。我发现我之前为 Web 系统编写的单元测试存在一个问题，即究竟应该以什么为「单元」进行测试。之前通常是以每个 API 接口为一个单元，测试这个 API 接口在各种情况下的工作情况。但当程序的逻辑复杂起来以后，为了测试一个 API 接口在某种环境下的工作情况，需要花费大量的代码来准备这个环境。于是一个更好的方式就是以「行为」为单位，一种行为包含了一组 API 请求，它们往往需要通用的环境，因此更适合被放在同一个单元中。