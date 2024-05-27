→yml

类别：未分类

date: 2024-05-18 05:35:16

→

# 软件成本曲线与情境驱动测试（CDT）| 交易桌上的故事

> 来源：[`mdavey.wordpress.com/2016/03/16/software-cost-curve/#0001-01-01`](https://mdavey.wordpress.com/2016/03/16/software-cost-curve/#0001-01-01)

## 软件成本曲线与情境驱动测试（CDT）

缺陷成本([defects](http://swreflections.blogspot.co.uk/2013/09/the-real-cost-of-change-in-software.html))是大多数团队不担心的事情。大多数团队主要关心的是构建软件，接受测试周期中会发现的缺陷，以及在生产中会发生缺陷。不幸的是，这是 21 世纪对软件的一种天真看法。

[考察敏捷变更成本曲线](http://www.agilemodeling.com/essays/costOfChange.htm)对这个话题提供了一些思考。图 3 特别值得关注。现在支付还是以后支付缺陷成本，以后支付的成本会更高。不幸的是，大多数利益相关者/产品所有者只想要功能，只想要功能，并且不理解或不在乎软件工程师以及成本，直到通常为时已晚 😦

特别是图 3 中“通过传统验收测试发现的 Requirements 缺陷”的成本。

这使我们想到了软件工程界（至少在测试领域）最新的热潮，即情境驱动测试([CDT](http://context-driven-testing.com/))。

Rally 有一篇关于[CDT](http://www.developsense.com/blog/2016/01/a-context-driven-approach-to-automation-in-testing/)和[敏捷](https://www.rallydev.com/blog/engineering/context-driven-testing-agile-teams)团队的帖子，提供了一些有趣的数据点：

+   “理解我们在测试什么是我们产品质量的基石。”——无法反驳这一点:)

+   “测试人员的职责是提问：为什么、什么、在哪里、如何、如果等等。他们需要在每个阶段提出问题，但尤其在编码开始之前，而不是在过程后期”–我认为这个数据点特别关键。我总是担心那些只从以他们的简历为中心的视角/自尊心讨论测试，忽视了成为团队一员的需求，利用他们的测试技能作为协作过程的一部分，交付高质量的软件。因此，“每个阶段”和“尤其在编码开始之前”与我对软件工程的认识非常契合。:)

+   “业务价值”–无需多言:)

+   “目的不是发现任何缺陷，而是发现重要的缺陷” 同意:)

+   作为一名测试人员，很容易被产品中可能不是那么重要的区域的缺陷所分心。”——不幸的是，这是真的，我称这为“偏离轨道”。

这让我想到了[CDT](http://context-driven-testing.com/)，以及七项基本原则：

+   “人们在一起工作是任何项目背景中最重要的部分”——100%同意。这就是为什么测试人员和其他项目团队成员需要像团队一样协作，以交付伟大的软件。进入故事的发现讨论，停止接受代码，停止认为游戏是发现缺陷。测试通常会在敏捷团队中突出显示其他问题。寻找根本原因，并在代码编写和测试之前协作修复流程。

+   “良好的软件测试是一个具有挑战性的智力过程。”——这个原则感觉像是测试人员试图验证他们与开发人员的智力能力。在这样一个团队中，每个人都是平等的，每个人都协作交付一个令团队自豪的软件产品，这不应该是有必要的。

我们可以大概结束过去几年中发展起来的 Check != Test [讨论](http://www.satisfice.com/blog/archives/856)。尽管如此，我们还需要考虑在整个故事生命周期中检查和测试的概念（敏捷）。否则，缺陷将继续上升。通常生成验收标准讨论的故事发现和详细说明也需要在 CDT 的背景下考虑。CDT 不能仅仅是管道末端的孤岛，测试人员坐在新的 CDT 光鲜世界里。

最后一点，很多 CDT [文章](http://www.satisfice.com/articles/cdt-automation.pdf)并没有涉及到 CDT（检查≠测试）是如何与看板或 Scrum（敏捷）团队一起工作的。

~ 由 mdavey 于 2016 年 3 月 16 日发表。

发布在[敏捷](https://mdavey.wordpress.com/category/agile/)、[未分类](https://mdavey.wordpress.com/category/uncategorized/)
