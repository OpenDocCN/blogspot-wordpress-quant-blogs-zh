<!--yml

类别：未分类

日期：2024-05-18 05:23:04

-->

# Magmasystems Blog: 指数和定制信用违约互换

> 来源：[`magmasystems.blogspot.com/2005/11/index-and-bespoken-tranches.html#0001-01-01`](http://magmasystems.blogspot.com/2005/11/index-and-bespoken-tranches.html#0001-01-01)

在我们正在构建的信用衍生品交易系统中，我们需要添加对各种结构化产品的支持。其中两种产品是指数和定制分层。我们最终需要实施的其他工具包括 NTDs、CDOs 和 CDO

2.

我们都知道信用违约互换（CDS）是什么，对吧？这是某人为一家公司购买的一种保险形式。一方（保险的购买者）定期向另一方（保险的出售者）支付保险费，以获得一个基础证券（债券或其他信用工具）的保险。如果基础证券发生“信用事件”（例如：公司破产、错过利息支付，或 CEO 带着他的秘书逃到百慕大），保险的出售者必须向购买者支付一定数额的钱，这被称为“恢复率”。CDS 有一些参数，例如

**优先级**

（在公司破产时首先获得赔偿的人）， the

**期限**

（购买者需要支付保险费的时间长度），以及

**名义金额**

（基础证券的价值）。

有关于 CDS 的指数。我们可以创建我们自己的指数，比如所有美国汽车制造商的债券。或者，我们可以使用交易所制造的指数。

CDS 指数非常受欢迎，以至于有

[CDS 指数](http://djindexes.com/mdsidx/index.cfm?event=cdx)

在道琼斯指数上。交易最广泛的 CDS 指数是

[北美投资级指数](http://finance.yahoo.com/q?s=%5EDJCDXNI)

证券。它占交易 CDX 体积的 80%以上。

所以，现在我们知道什么是 CDS 指数。接下来是分层......

一个

**分层**

是一定程度的风险。根据 Investopedia 的说法：

**分层是一个经常用来描述特定类别的** [**债券**](http://www.investopedia.com/terms/t/tranches.asp#) **的术语，在发行中每个分层对** [**投资者**](http://www.investopedia.com/terms/t/tranches.asp#) **提供不同程度的风险。例如，一个 CMO 提供的分隔 MBS 投资组合可能包括一年、两年、五年和 20 年到期的抵押贷款（分层）。**

对于上面提到的指数，有 5 个分层。The

***股权**

分层覆盖信用工具的第一个 3%的损失。The

***中级**

分层覆盖从 3-7%。The two

***高级**

分层分别覆盖 7-10%和 10-15%。The

***超级高级**

分层覆盖最后 15-30%的损失。

**指数分层**

是为活跃交易者设计的。一个

**定制分层**

这是根据投资者的愿望组装的。它通常是长期投资的产物。

©2005 Marc Adler - 保留所有权利
