<!--yml

分类：未分类

日期：2024-05-12 19:25:49

-->

# 量化交易：通用投资组合

> 来源：[链接](http://epchan.blogspot.com/2007/01/universal-portfolios.html#0001-01-01)

让我描述一个投资组合优化方案，长期来看，这个方案应该能保证超越组合中表现最好的股票。

在我们开始之前，让我们同意我们每天都会重新平衡我们的投资组合，以便每只股票都有固定的资本百分比分配，就像你最喜欢的金融顾问会建议你的那样。这意味着如果你持有 IBM 和 MSFT，而 IBM 在一天后上涨而 MSFT 下跌，你应该卖掉一些 IBM 并用这些资本购买更多的 MSFT。这种投资组合有一个技术术语：它们被称为“常青平衡投资组合”。同时注意到这与凯利准则的相似性，我在

我写过：[链接](http://epchan.blogspot.com/2006/10/how-much-leverage-should-you-use.html)

之前：凯利准则要求你保持恒定的杠杆，这就像在现金（债务）和股票之间保持固定的百分比分配。

那么固定百分比分配应该是多少呢？这个方案就在这里变得有趣。假设我们从一个平等的资本分配开始，因为缺乏更好的选择。一天结束时，你的投资组合有一定的净价值。但然后你可以计算如果你开始用不同的分配会有怎样的净价值。确实，我们可以运行这个模拟：尝试所有可能的初始分配，并计算结果投资组合的假设净价值。用这些假设的净价值作为权重（在它们被所有净价值的总和标准化之后），并计算加权平均百分比分配。最后，采用这个加权平均分配作为新的期望分配，并相应地重新平衡投资组合。所以实际上这个“固定”的百分比分配根本不是固定的：它每天都会调整，但可能调整不多。每天重复这个过程，总是通过模拟从第一天开始的各种初始分配来计算新的加权分配。

这种投资组合优化方案可以证明，在足够长的时间内，其净价值会超过仅仅持有最好的股票。如果这听起来像是一个奇迹，部分原因是因为这是一个信息论的巧妙结果，部分原因是因为实际上有一些限制，这些限制限制了它的实际应用。证明它有效（至少在理论上）相当技术化，我留给感兴趣的读者查阅原文

论文：[链接](http://itg.stanford.edu/~cover/papers/universal_portfolios.pdf)

由斯坦福大学的著名信息论者 Thomas Cover 教授发表。他为使用这种方案重新平衡/优化的投资组合创造了术语“普遍投资组合”。如果不理解数学直觉，这种方案可能对那些相信股票长期趋势行为的人有吸引力，因为如果一只股票过去表现非常好，我们最终会在长期内分配更多的资本给它。它也可能吸引那些相信短期均值回归行为的人，因为短期内，我们根据大约恒定的分配对股票头寸进行每日再平衡。然而，这种似乎证实了股票价格的趋势或均值回归特征的确认是幻觉的——这种方案即使股票价格完全是随机的也应该有效！我们如何设法即使在随机价格序列中也能挤出收益？记住我们之前已经做了相反的事情（参见我之前的

[文章](http://epchan.blogspot.com/2006/11/correction-maximizing-compounded-rate.html)

):即使价格序列表现出几何随机游走，我们还是设法亏了钱。因此，我们也能利用类似的信息论技巧赚钱，这并不令人惊讶。

现在谈谈警告。每次信息论者开始说“长期来看，…”，你会最好地建议问：多久？在我的几何随机游走中

[示例](http://epchan.blogspot.com/2006/11/correction-maximizing-compounded-rate.html)

在每期的回报波动率（标准差）为 1%的情况下，我们发现复合回报率每个周期痛苦地低至-0.005%。在普遍投资组合方案中，超越组合中最佳股票的表现同样取决于股票的波动性：波动性越高，超越表现越快。让我用由两个 ETF（RTH 和 OIH）组成的投资组合运行一个模拟。如果我们从 2001 年 5 月 17 日至 2006 年 12 月 29 日运行普遍投资组合方案，我发现累计回报是 32%（未计交易成本）。与仅仅购买并持有最佳 ETF（即这里的 OIH）相比：累计回报是 54%。普遍投资组合输了。这意味着理论是错误的吗？其实不是：RTH 和 OIH 的波动性可能只是太低。这就是普遍投资组合方案的第一个实际警告：如果波动性低，它可能需要太长时间才能实现其好处。

我们如何找到波动性足够高的 ETF 来实现普遍投资组合的超越表现？实际上，我们可以通过提高 RTH 和 OIH 的杠杆来简单地人为提高它们的波动性。那么假设我们将它们的杠杆都提高 2 倍。这意味着它们每日回报和波动性都翻倍。现在最佳 ETF（仍然是这里的 OIH）的回报是 23%（为什么它低于未杠杆的情况？记住我之前的公式中的 m-s²/2）。

[文章](http://epchan.blogspot.com/2006/11/correction-maximizing-compounded-rate.html)

。）然而，通用投资组合的回报率为 45%。所以现在通用投资组合获胜了。但这是一种战略性胜利：如果你考虑到 10 个基点的交易成本，通用投资组合的实际回报率只有 4%。这是通用投资组合的第二个警告：由于需要频繁重新平衡，交易成本往往侵蚀了所有的超额回报。

现在还有一个最后的警告。读者可能要问，为什么我不选择两只股票来阐述这个方案，而不是选择两只 ETF？大多数股票的波动性不是比 ETF 大得多，因此更适合这个方案吗？确实，大多数学术论文，包括 Cover 教授的原论文，都使用一对股票作为示例。但如果我们这样做，我们就有引入生存偏差的风险。自然地，如果你事先知道这两只股票都不会破产，通用投资组合方案可能看起来很棒。但如果你运行一个模拟，其中一只股票某天突然破产（这往往是一件相当数学上不连续的事情），通用投资组合方案很可能一开始就不会优于只持有非破产股票。使用 ETF 消除了这个问题。但然后 ETF 的波动性要小得多。

所以考虑到所有这些警告，通用投资组合真的实用吗？Cover 教授似乎是这样认为的。这就是他启动了对冲基金来证明这一点。
