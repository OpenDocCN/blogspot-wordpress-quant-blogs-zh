<!--yml

类别：未分类

日期：2024-05-12 19:52:09

-->

# MTS & 报价状态引擎 | 编码市场

> 来源：[`etrading.wordpress.com/2006/06/28/mts-quote-state-engines/#0001-01-01`](https://etrading.wordpress.com/2006/06/28/mts-quote-state-engines/#0001-01-01)

## MTS & 报价状态引擎

### 2006 年 6 月 28 日

[有限状态机](http://en.wikipedia.org/wiki/Finite_state_machine)是我们用在交易系统中管理报价和 RFQ 状态的标准编程技术。考虑在 MTS 上的报价状态管理。MTS 特别有趣，因为 MTS 将市场制造商的报价视为“提案”，这些是坚定的、可交易的报价。这与其他纯粹由报价驱动的市场，如彭博和 TradeWeb，非常不同，在这些 ECN 上，我们发送的报价是指导性的，而不是可交易的。在这些 ECN 上，只有当客户点击指导性报价并发起 RFQ 时，我们才会向个别客户发送一个可交易的价格。

由于对于 MTS，我们的报价是坚定的，或者可以交易，我们开发者必须非常重视我们系统发送的报价。如果我们把陈旧的报价留在市场上，我们的交易员会损失金钱。当这种情况发生时，他们会非常不高兴。确切为什么报价会变陈旧，这会让我们进入讨论固定收益定价引擎的架构和设计，以及期货、基准债券、债券和掉期之间的价格关系。我们还可以讨论 MTS 的交易报价模型以及相关的排队机制。这些都是另外一天的问题，所以我们假设在一个快速变动的市场中，我们必须每秒重新计算几次债券价格，并将结果报价发布到 MTS。

我们的系统是一个自动报价系统：它自动化了在一打 ECN 上报价债券的过程。当然，我们的交易员控制着我们的自动报价系统，就像飞行员控制飞机上的自动驾驶系统一样。报价状态引擎确保自动报价系统以安全和可预测的方式响应交易员对其控制装置的操作。交易员可用的控制装置是价差、买入和卖出数量，以及报价是开启还是关闭。现在让我们通过一些关于债券报价的状态和转换的例子来进行说明…

+   状态

    +   死亡：我们没有报价债券。

    +   待处理价格：交易员已经开启报价，但我们还没有从定价引擎那里得到最新的价格跳动。

    +   待处理市场开启：报价是开启的，我们有一个最新的中间价格，并应用了一个价差，将结果的买入和卖出价格及数量发送到 MTS，从而开启了一个报价交易，但 MTS 尚未关闭报价交易。

    +   直播：MTS 已经关闭了报价交易，向我们示意该提案已活在市场上，因此可以交易。

    +   待处理市场关闭：交易员已经关闭了报价，我们已经启动了报价关闭交易，但 MTS 尚未确认报价关闭交易已关闭。

+   转换

    +   BankOn：我们已经登录到 MTS。

    +   TraderOn: 报价按交易员分组。拥有这个报价的分组交易员已经登录

    +   Price: 定价引擎传来了一个新的中间价格

    +   Trade: 市场接受者触发了我们的提议。我们可能想要关闭报价几秒钟，让交易员在重新开启之前考虑这笔交易

    +   TraderOff: 交易员已经关闭了他的报价组

    +   BankOff: 我们已经从 MTS 上登出

正确获取状态和转换意味着我们避免了在陈旧价格上交易。例如…

+   使用陈旧的中间价格开启报价，然后随后在错误的价格上交易

+   在之前的报价交易关闭之前尝试发送一个新的报价。如果这个报价的中间价格再次变动，我们将在发往外部的队列中有一个陈旧的报价，而后面则是一个更新更新鲜的报价

当然，上述所有内容都是过于简化的，我还省略了像 MTS 的通道机制和 OpenServer 这样的各种问题，但你应该明白了…
