<!--yml

分类：未分类

日期：2024-05-18 05:42:03

-->

# 微服务辩论 | 交易桌面故事

> 来源：[`mdavey.wordpress.com/2015/06/05/the-great-micro-services-debate/#0001-01-01`](https://mdavey.wordpress.com/2015/06/05/the-great-micro-services-debate/#0001-01-01)

## 微服务辩论

少数人关注了正在许多公司中进行的关于微服务的伟大辩论。微服务，像许多其他架构选项一样，只是工具箱中的另一个工具。没有一种单一的解决方案能解决所有问题:) 马丁·福勒（Martin Fowler）在他的[文章](http://martinfowler.com/bliki/MonolithFirst.html)中提出了关于微服务架构的最新观点。萨姆·纽曼（Sam Newman）在[一篇博客](http://samnewman.io/blog/2015/04/07/microservices-for-greenfield/)中提供了一个关于棕地/绿地微服务的很好的案例研究。我认为萨姆文章中的一个重要收获是，对问题的领域知识对于服务的划分至关重要。

> 尽管他们对持续集成领域的领域知识非常了解，但他们为托管 CI 解决方案提出的服务边界初稿并不完全正确。这导致了变更成本和拥有成本很高。在为这个问题奋斗了几个月后，团队决定将服务合并回一个大型应用程序。后来，当应用程序的功能集稳定了一些，团队对领域的理解更加坚定时，找到那些稳定的边界变得更容易了。

整洁的代码（Clean Code）[博客](http://blog.cleancoder.com/uncle-bob/2014/09/19/MicroServicesAndJars.html)在服务领域也提供了合理的建议：

> 不要仅仅因为微服务听起来很酷就仓促进入。首先使用插件架构将系统划分为 jar。如果这还不够，那么在战略点上考虑引入服务边界。

作者：mdavey，发布于 2015 年 6 月 5 日。

发布在[语言](https://mdavey.wordpress.com/category/languages/)分类下
