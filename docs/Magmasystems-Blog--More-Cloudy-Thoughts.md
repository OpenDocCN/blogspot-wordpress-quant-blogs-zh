<!--yml

类别：未分类

日期：2024-05-18 05:03:00

-->

# Magmasystems 博客：更多关于云计算的思考

> 来源：[`magmasystems.blogspot.com/2008/04/more-cloudy-thoughts.html#0001-01-01`](http://magmasystems.blogspot.com/2008/04/more-cloudy-thoughts.html#0001-01-01)

看来我在描述事件云的想法时的笨拙引发了一些 Greg 和 Hans 之间的争论。我将尝试澄清我对事件云的思考，看看是否更有意义。

在我的帖子中我不想透露我们任何“秘方”，所以我会尝试将我的思考从股票交易领域映射到另一个我不熟悉的领域……建筑安全领域。（提前向所有阅读这篇文章的侦探们道歉。我的用例可能会诽谤你们尊敬的研究领域。）

假设我们正在为我们的 MegaBank 编写一个企业级的 CEP 应用程序，以监视我们的安全系统，以便那些爱打探的 StanLehGoldBar Inc 员工不要闯入我们的建筑物并窃取我们的秘密。

我们要区分以下

**原子事件**

以及

**派生事件**

。一个派生事件是在监视一个或多个原子事件时检测到有趣的事情时产生的。

一个原子事件可能根据用例存储在我们的 CEP 引擎中。一个派生事件将肯定由我们的 CEP 系统保存。由于派生事件代表了一个“有趣”的条件，我们可能想要对派生事件进行报告和分析。我们可能还想对派生事件进行一些复杂的搜索。在我心中，持久化的原子和派生事件形成了我们的事件云。

两个或更多的派生事件可以组合成一个新的事件。一个派生事件可以与一个原子事件结合成一个新的事件。让我来解释一下。

我们通过 CEP 系统处理很多原子事件。每个穿过 MegaBank 大门的人都会产生一个

**人员进入建筑物**

原子事件。（这相当于市场数据事件。）我们有 MegaBank 所有员工的静态数据库，当在

**人员进入建筑物**

事件中的人不在我们的员工数据库中，CEP 系统会产生一个

**非员工进入**

派生事件。这个派生事件将存储在我们的复杂事件处理引擎中。

我们还有其他派生

**人员离开建筑物**

事件在有人离开建筑物时产生。这个事件是由以下产生的

（让我们幻想一下，假设我们对进入建筑物的人进行视网膜扫描。让我们发挥一点想象力，说我们有 StanLehGoldBar Inc 所有员工的视网膜扫描）

假设我们在

**非员工进入**

事件和 StanLehGoldBar 员工的静态来源之间进行连接。我们可以产生一个

**建筑物内有竞争对手**

派生事件。这个派生事件也将保存到 CEP 引擎中。

我们监控我们建筑的所有大门。无论何时有人穿过股票交易大厅的门，我们都会生成一个

**TradingFloorEntered**

原子事件。如果有人在天下午 6 点后第一次穿过交易大厅的门，我们可能会认为这个行为是可疑活动，并且我们想要生成一个

**PossibleIntruderOnTradingFloor**

派生事件。

现在，一些聪明的安保人员是我们 CEP 系统的用户，他想创建一个新的派生事件。他想看看我们是否有竞争对手在夜间徘徊在我们的交易大厅。所以，安保人员进入我们的 CEP GUI，创建了一个新的、自定义的派生事件，称为 CompetitorOnTradingFloorAfterHours，如果满足以下条件之一就会生成：

**CompetitorInBuilding**

派生事件 2）没有“取消”

**PersonLeftBuilding**

事件，3）与

**PossibleIntruderOnTradingFloor**

事件。各种事件“漂浮”在我们的事件云中，这使得轻松创建新的派生事件成为可能。

安保人员可能还想对我们的事件云进行查询，看看竞争对手在夜间入侵交易大厅之前是否“踩点”。安保人员可能想看看在过去一个月里那个特定的竞争对手访问 MegaBank 的次数。他可能还想看看竞争对手在正常营业时间内访问交易大厅的次数。这听起来像是你会用数据仓库而不是 CEP 引擎做的查询。

因此，我们需要在 CEP 引擎中以有效的方式表示事件云。我们需要能够在 CEP 引擎运行时动态地创建新的派生事件。我们需要能够对事件云进行即兴分析，以提高我们的情境意识。我们需要能够创建新的有趣的视觉化效果，让用户窥视云中的情况。

有趣的东西，对吧？

Tim Bass 列出了可以用于事件分析的技术列表。这些技术包括：

+   基于规则的推理

+   贝叶斯信念网络（贝叶斯网络）

+   Dempster-Shafer 方法

+   适应性神经网络

+   聚类分析

+   状态向量估计

我必须承认，我之前并没有深入研究这些领域。然而，我们刚刚雇佣了一个有生物信息学背景的人，我们希望他能在睡梦中完成这些工作。谁会想到，在 MegaBank 工作，我会接触到如此有趣的研究领域呢？

©2008 Marc Adler - 版权所有
