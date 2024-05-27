<!--yml

分类：未分类

date: 2024-05-18 05:02:52

-->

# Magmasystems Blog: 抽象化 CEP 引擎

> 数据来源：[`magmasystems.blogspot.com/2008/04/abstracting-cep-engine.html#0001-01-01`](http://magmasystems.blogspot.com/2008/04/abstracting-cep-engine.html#0001-01-01)

昨天我收到了两条评论，以下是我的回答：

1)

*你购买了一个不支持事件云的 CEP 引擎吗？*

我们认为 Coral8 支持事件云，但我们正在寻找实现它的最佳模式。Mark 是

CTO

的 Coral8，不太同意“事件云”这个术语。他发布的

[这里](http://www.coral8.com/blogs/blog-entry/unclouding-and-streamlining-your-thinking-about-cep-use-cases)

突出他的论点。根据 Mark 的说法，“事件云”可以表示为多个事件流，

某事

的支持。

2)

*如何在您的系统中抽象化 CEP 引擎？*

首先，为什么。我们希望隔离自己，不受任何与

CEP

引擎，无论是产品本身还是公司方面。在这种经济环境下，我们担心其中一些规模较小的

CEP

企业可能会受到压力。那些有风险投资支持的企业可能会发现他们的

VC's

感到担忧，认为我们正在重蹈 2002 年至 2003 年那些不光彩的时代的覆辙。那些私人融资的公司可能会发现支持者希望转移到其他领域。众所周知，大多数公司都在削减或推迟软件采购，受到影响的第一批是小型利基公司。

我们还希望有一定的灵活性，以防

CEP

引擎本身并不像宣传的那样工作。Coral8 给了我们很大的支持，但我们还没有对它施加压力。我们知道其他评估过 Coral8 的公司，他们已经

foudn

一些缺点，这些问题 Coral8 工作人员已经解决。然而，完全有可能我们需要考虑另一种

CEP

引擎在 Coral8 跌跌撞撞时应该使用。

现在，关于如何...

我们没有使用 Coral8 的本地输入和输出适配器。我们甚至不使用 Coral8 的

PollFromDatabase

和

ReadFromDatabase

适配器。我们有一个输入服务器，用于读取静态和实时数据，

marshall

把数据从 Coral8

元组

。在另一边，我们有一个输出服务器，它接收由其他系统生成的派生事件

元组

from Coral8，

marshalls

并将它们转换为通用格式，执行各种警报和可视化操作。

从我们评估其他

CEP

供应商，我们的输入和输出服务器层处理

Aleri

和

Streambase

。换句话说，我们有自己的适配器！从 Coral8 更改到

Streambase

或

Aleri

涉及对我们类似 Spring 的配置文件进行简单编辑。

此外，我们有能力将工作外包给其他引擎，例如

KDB

+. 我们可以读取其他系统生成的派生事件（只要它们在我们的通用格式中）并将它们放入

CEP

引擎的"事件云"。

在我们的架构中，我们引入了额外的跃点，以便抽象化

CEP

引擎。但是，我们并不太担心，因为我们处理的是分析和小号，而不是交易。

©2008 马克·阿德勒 - 版权所有
