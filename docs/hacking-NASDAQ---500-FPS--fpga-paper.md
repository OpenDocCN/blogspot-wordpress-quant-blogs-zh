<!--yml

类别：未分类

日期：2024-05-13 00:01:50

-->

# hacking NASDAQ @ 500 FPS: fpga 论文

> 来源：[`hackingnasdaq.blogspot.com/2012/10/fpga-paper.html#0001-01-01`](http://hackingnasdaq.blogspot.com/2012/10/fpga-paper.html#0001-01-01)

今天碰到了这篇广告^H^H^H^H^H 《由 IEEE 审查的》论文。

它写得很好，内容很全面，但包含一些非常糟糕的假设。让我们一一解析

摘要：

"该应用程序以固定的端到端延迟 1 微秒维持 10Gb/s 以太网线速率 - 比可比较的软件实现低了两个数量级。"

他们在说用脑残策略的软件延迟是 100 微秒？这完全是废话，是的，如果你写烂代码，你的端到端延迟将是 100 微秒，再加上 25 微秒的抖动。如果你使用标准硬件编写紧凑的代码并且知道你在做什么...绝对可以轻松在 10 微秒以下的端到端延迟问题。

下一点：

"初始的数据处理阶段使用流中的冗余信息替换由于数据包丢失而暂时丢失的任何信息，以便重构交易所订单簿的必要部分。"

这是纯魔术，不知道他们在这里谈论什么。当市场数据包丢失时，如何能够在少于 1 微秒内在 FPGA 的 RTL 上重新构建其标识/价格/买入与卖出/数量/操作。承认如果给予约 100 毫秒或更多时间，并且在数据流中存在显著的延迟，e.g. 你丢失了一个新的报价 X，但收到了取消报价 X 的消息时，也许能够很好地猜测数据包中存在的内容... 也许他们在谈论使用 *咳咳*市场数据恢复通道。

下一点：

"美国交易所中交易的所有 8000 种证券的价格均可容纳在 FPGA 芯片上的内存中。表的大小可扩展以支持更多所需的符号。"

这很棒，但是什么鬼？猜想他们在谈论 8000 * 4 字节（32 位固定点价格）* 2（买入/卖出）* 信号存储最佳买入/卖出的价格。这在赛灵思 V5 240T 的块 RAM 内(注意：块 RAM 是 FPGA 芯片上的内存，不要与外部内存（比如 DDR/QDR/SRAM）混淆)很容易就能够存储。

很好，但是...他们怎么计算 BBO 呢？你需要存储整个订单簿，至少需要在外部存储器中存储工作集因为工作集至少为 1GB。

为什么要存储整个订单簿？

1) 当你收到报价取消消息时，交易所很少会在取消消息中包含价格/数量/买入与卖出/标识。通常只有订单号和/或取消的数量，因此需要保留价格/数量/买入与卖出/标识/订单号等信息才能正确处理，如处理 Y 个报价取消消息后此订单的当前开放数量。

2) 当一个报价被删除时，需要从订单簿中将其移除，然后遍历订单簿以找到最佳价格 - 读取需要在内存中保留订单簿。关键在于智能地以及何时遍历以找到最佳价格，如对大部分排序的列表进行排序可能非常快。

3) .... 但今天在这上面浪费了太多时间。

……所以，你是在说，我们可以在 fpga 中存储 8000 个买入/卖出价格，供 rtl 编码的算法使用？嗯……

这是一篇很好的、写得很技术的论文，也许是关于这个主题最好的论文之一，但是忽略了一些更重要的细节……就像所有关于这个主题的学术论文一样……也就是说，只需坐着忍受那 30%的账户回撤 3 个月，而盈利是漂亮的。

/抱怨
