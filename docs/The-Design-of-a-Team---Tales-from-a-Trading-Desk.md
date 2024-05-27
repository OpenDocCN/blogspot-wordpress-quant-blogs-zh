<!--yml

分类：未分类

日期：2024-05-18 06:03:20

-->

# 团队设计 | 交易桌上的故事

> 来源：[`mdavey.wordpress.com/2013/08/07/agile-the-design-of-a-team/#0001-01-01`](https://mdavey.wordpress.com/2013/08/07/agile-the-design-of-a-team/#0001-01-01)

这有点像随机游走，基于交流、阅读和处理团队学习心得的时间跨度。

David [Hanna](http://dave-hanna.net/) 提供了一句非常棒的引语，值得反复阅读以确保你完全理解它：

> **所有的组织都是为了得到他们得到的结果而完美设计的。**

为了取得成果而进行团队打击可能不是解决方案，尽管当组织想要的结果不理想时，这种“管理”风格经常会使用。现在想想上面引用的内容。也许组织构建了这样一个团队，使团队本质上被设置为失败？

这引导了当考虑到“管理”时的 Paul [Drucker](http://en.wikipedia.org/wiki/Peter_Drucker)。Drucker 先生为管理者提供了 5 个基本[任务](http://guides.wsj.com/management/developing-a-leadership-style/what-do-managers-do/)。成功提供了一个很好的[视角](http://www.success.com/articles/1115-peter-drucker-the-father-of-management-theory)来观察 Drucker 先生的管理理论，同样[商业周刊](http://www.businessweek.com/stories/2005-11-27/the-man-who-invented-management)也做过类似的工作。Drucker 先生的一些经典[评论](http://sourcesofinsight.com/lessons-learned-from-peter-drucker/)：

+   我们所说的管理的大部分内容都是让人们对完成工作变得困难。

+   沟通中最重要的事情是听到没有被说的内容

+   工作的生产力不是工人的责任，而是管理者的责任。

最近，Chris [Parsons](http://chrismdp.com/) 在今年早些时候的苏格兰 Ruby 会议上提供了一场见解深刻的[演讲](http://chrismdp.com/2013/05/leading-software-teams-well/)，题目为“[如何](http://vimeo.com/66884238)领导软件[团队](http://chrismdp.com/tag/team/)得好”。这场演讲非常值得一听，特别是因为它重申了一些古老的观点，不幸的是，这些观点在今天经常因为糟糕的领导和管理而迷失。几个关键点：

+   管理结构经常会妨碍工作。

+   领导力**不是**管理。像装配线那样的管理在软件工程中已经是过时的了——你不能控制人！

+   任务[委派](http://chrismdp.com/2012/09/task-assignment-is-a-team-anti-pattern/) 😦 如果说有什么是敏捷的反模式，那这就是一个。

+   职位名称——我一直觉得职位[名称](http://chrismdp.com/2012/09/job-titles-team-anti-pattern/)会在团队中产生隔阂心态，导致[团队](http://chrismdp.com/2011/04/the-team-is-the-atomic-unit/)的微软 Excel 资源流动 😦  在招聘之前进行试用绝对是可能的最好方法——妥协的招聘将会在你和你的公司身上造成严重的金钱损失

+   停止在团队内部指指点点！

+   提升你的替代者！

这使我转向了 BDD（行为驱动开发），以及我对那些声称遵循 BDD 但实际上只是遵循一般“测试”的人的疑问。这个问题通过访问敏捷联盟网站，并查看其[BDD](http://guide.agilealliance.org/guide/bdd.html)页面，可以得到更好的澄清。该页面在我看来，提供了一些关于“使用迹象”的优秀观点。具体来说，思考一下遵循与你今天使用的“测试”相比的后果，以及从故事（带有验收标准/测试）到代码可能的断裂：

+   使用[BDD](http://www.manning.com/smart/)的团队应该能够提供大量的“功能文档”，以用户故事的形式，辅以可执行的场景或示例。

+   与其说“类的单元测试”，不如说使用 BDD 的实践者或团队更喜欢谈论“类的行为规格”。这反映了此类规格更大的关注点：它们的名称预期更具表达力，并且，当与给定-当- then 格式的描述一起完成时，它们将作为技术文档服务。

这又让我想起了另一个反模式——Cucumber 是一个测试工具。如果你持有这种观点，那么考虑阅读这篇[帖子](http://chrismdp.com/2013/06/rack-usermanual/)，以及这篇[文章](http://chrismdp.com/2012/09/cucumber-isnt-a-testing-tool/)。Dan North 提供了更多的 BDD 示例[在这里](http://dannorth.net/whats-in-a-story/)，具体是关于故事是“项目干系人、业务分析师、测试人员和开发人员之间的[对话](http://chrismdp.com/2012/09/cucumber-isnt-a-testing-tool/)”的结果。对我来说，一个带有验收测试（AT）的良构故事，生成代码和“测试”，如果不利用 Given-When-Then AT 的工作，似乎就像一个损坏的流水线——如果 AT 在编码之前利用 DSL 的话，情况会更糟。

~ mdavey 于 2013 年 8 月 7 日。

发布在[敏捷](https://mdavey.wordpress.com/category/agile/)
