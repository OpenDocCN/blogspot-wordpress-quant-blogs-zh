<!--yml

分类：未分类

日期：2024-05-18 14:03:48

-->

# 使用概率密度作为适应性机制 – 量子金融家

> 来源：[`quantumfinancier.wordpress.com/2010/05/14/using-probability-density-as-an-adaptive-mechanism/#0001-01-01`](https://quantumfinancier.wordpress.com/2010/05/14/using-probability-density-as-an-adaptive-mechanism/#0001-01-01)

我现在将暂停一下《时间机器》系列，当我进一步研究并准备未来的文章时。今天我将跟进我关于回报分布的文章，展示一种简单的方法将其包含在适应性策略中。

博客圈里已经有很多讨论，认为具有固定参数的策略不如适应性策略。例如我能想到的最简单的每日 MR 策略可能是 RSI 2 50/50，但这个策略并不总是有效，我当然也不期望它会永远有效。此外，RSI 的最有利回顾参数也会随时间变化。这就是回报分布有用的地方。从这里，我们可以导出概率密度函数，并利用它来创建一个适应性机制。

关于概率密度函数稍微有一点背景；从维基百科上来说：“连续随机变量的密度是一个描述这个随机变量在观察空间中给定点发生相对可能性的函数。”用简单的话来说；就是某个特定事件发生的概率。我建议使用你最喜欢的统计软件来这样做，除非你想长时间做积分！

对于这个测试，我取了 SPY 数据，计算了不同回顾期（2 到 30）的 RSI 值，然后查看了每个策略的结果。对于一个滚动周期为 1 年半，我查看了每个策略的回报概率密度，特别关注回报大于零的概率（这可以改为更高的阈值，只是想保持基础）。然后我交易了 1 年半内值最高的策略。这样，资本就分配给了由参数生成最高正回报概率的策略，这个概率由概率密度函数来衡量。我比较了 RSI 2 50/50 策略和持有策略。

结果

![](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/05/density-adative.png)

![](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/05/density-adative-results.png)

结果并不特别令人印象深刻，文章的目的是尽可能简单地说明这个概念。我相信有方法可以使这种特定策略更加稳健；作为初学者，可以缩短回顾期的时间框架，使其对近期市场数据更加敏感，或者引入加权方案，更多地权衡近期数据。我会让读者自己尝试，如果你愿意分享，我很乐意发布结果。尽管结果并不壮观，但这个策略似乎能够适应市场中的不同波动，并根据当前市场范式将资本分配到更适合 RSI 参数长度的参数上。

QF
