<!--yml

类别：未分类

date: 2024-05-18 04:58:46

-->

# Magmasystems 博客：Colin 正在构建一个 CEP 应用程序

> 来源：[`magmasystems.blogspot.com/2008/09/colin-is-building-cep-app.html#0001-01-01`](http://magmasystems.blogspot.com/2008/09/colin-is-building-cep-app.html#0001-01-01)

Colin Clark 开始撰写关于 OMICRON 5000 的博客，这是一个

CEP

-基于的订单路由器/流动性查找器，他想要构建。我不确定 Colin 是否只是在博客上概述系统，或者他是否

去

开始编写这个东西。但是，我会密切关注他的即将到来的冒险，因为 Colin 暗示他将在开发过程的每个步骤中通知我们。

我不知道 Colin 将选择哪种技术平台……Windows 或 Linux，C# 或 C++ 或 Java。如果 Colin 对这项新努力非常公开，那么我可能会期待一些供应商为他提供一些免费软件，因为这将对

CEP

最终选择的供应商。

Colin 的评估将在我们进行初步评估一年后进行，我很想看看他将如何选择

CEP

引擎。Colin 是一个人公司。*如果* Colin 能够获得一些

CEP

软件，他将无法像我们一样享受同样的奢侈——4 个月用于研究——以进行长时间的评估。

让我们看看一个公司能做什么，以启动进入

CEP

.

Colin 将如何获取他的手？

CEP

用于评估的软件？Coral8 可以免费下载，并且他们的开发者版本非常容易上手。你可以下载

Aleri

，但根据我的记忆，它附带一个 30 天的许可证。Progress

Apama

不会让我下载他们的软件，除非要求我进行演示。

Streambase

向我们提供了他们的软件，所以我不知道他们的评估过程。

Esper

完全免费（至少，他们的非高可用性版本是）。我想知道保罗·文森特是否会送给 Colin 一份 Business Events 玩。

一旦 Colin 选择了

CEP

引擎，他需要花费多少资金才能获得该软件的生产许可证？

Esper

是免费。其他软件需要最低支出 60,000 美元，不包括年度维护费用。你可以随意使用你从 Coral8 下载的版本，但在不购买许可证的情况下无法将其部署到生产应用程序中。

Colin 表示 OMICRON 需要一个数据库。我假设 MySQL 在 Sun 收购后仍然免费。你需要找到一个

CEP

拥有 MySQL 适配器的引擎。

OMICRON 需要一个 FIX 引擎。我所知道的唯一免费的一个是

QuickFix

。Colin 将为他的

CEP

引擎？

OMICRON 需要市场数据。

OpenTick

是免费使用的，你只需要支付交易所费用。最糟糕的情况是，你可以编写一个服务，从雅虎财经那里抓取数据，但我相信这不会满足 Colin（尽管它在早期开发阶段很有用）。

最终，Colin 需要一个图形用户界面 (GUI)。如果 Colin 使用 C#/.NET，Visual Studio 附带了许多控件，而且你还可以在诸如

CodeProject

。我假设 OMICRON 需要的只是一个简单的网格，也许有些单元格需要实时更新。

看来如果一个开发者选择使用 Esper，他可以完全免费地使用开源软件。如果你愿意，也许可以使用大学开发的 CEP 引擎系统。

我会密切关注 Colin 的博客，并对他的每一个动作发表意见……

©2008 Marc Adler - 版权所有。

这里的所有观点都是个人的，与我的雇主无关。
