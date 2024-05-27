<!--yml

类别：未分类

日期：2024 年 05 月 12 日 21:21:04

-->

# Falkenblog：Beta 1.0：一种新的低成本指数化策略

> 来源：[`falkenblog.blogspot.com/2010/09/beta-10-new-low-cost-indexing-strategy.html#0001-01-01`](http://falkenblog.blogspot.com/2010/09/beta-10-new-low-cost-indexing-strategy.html#0001-01-01)

在

[曾经提出过](http://www.efalken.com/RiskReturn.html)

人们为希望而付费--彩票，黑天鹅--而这表现为各种形式高波动性资产的较低回报。在实践中，情况比原始数据显示的更糟糕，因为高波动性资产往往具有更高的交易成本，因为它们通常流动性较差，具有较高的买卖价差，并且在你试图进入时会更多地移动。

因此，显而易见的是，一个追求夏普比率最大化的投资者应该以低波动性的投资组合为目标，实际上也确实有许多这样的指数和基金正在被创建。这位荷兰资产管理人

[罗宝](http://www.robeco.com/eng/lp/global/index.html)

聘用经济学家

[Pim van Vliet](http://papers.ssrn.com/sol3/cf_dev/AbsByAuth.cfm?per_id=296465)

曾经写过关于反常低波动性结果的文章，他们有两只低波动性基金，

[全球保守股权](https://www.robeco.com/com/eng/institutional_investors/product_information.jsp?pdstchn=instcom&pfndid=2581&plang=english)

和

[欧洲保守股权](https://www.robeco.com/com/eng/professionals/products/product_information.jsp?pdstchn=profcom&pfndid=3250&plang=english)

基金。我认为这种策略主导了它们的基准，因为它们避开了那些回报非常差的高飞者，同时降低了风险：在回报-波动性空间中是双赢的。机构股权管理者应该涌向这些产品，因为他们应该足够精明，能够看到夏普比率是广泛分散的股权组合的最佳度量标准。

然而，我理解很多投资者更关心的是'表现不佳'，比如任何与标准如标普 500 有偏差的地方。大约在 2000 年左右，我试图推销一个低波动策略，并且用我自己的钱运作一个小型基金，作为我作为量化分析师和风险经理的日常工作的副业。我记得很多人对我说，一切看起来都很好，但它在过去的一年里的表现将会不佳，没有人想把钱投入到最近表现不佳的策略中去。我认为这是不理性的，但考虑到资金流入基金的方式--通过相对表现--这是理性的，考虑到他们的约束条件。唉，它在接下来的两年里表现得非常好。关键是，当你使用几十年的数据来计算平均值时，你不能真正的把握市场时机；并不是一切都有动力。

我曾经担心我的结果会被套利，但现在我意识到，像许多有好主意的人一样，我的问题不是人们窃取它，而是把它塞进他们的喉咙里。 “CAPM 不适用”的想法已经得到了很好的确认。甚至高波动性股票表现不佳的事实现在几乎是普遍公认的。因此，其含义显而易见（尽管我

[不得不花费大量资金才能说这番话](http://www.efalken.com/papers/legaldocs.html)

：低波动性股票组合是一种主导的股票投资策略。

回到 1993 年，当我试图向西北大学的教员们推销我的发现时，即低波动性股票的回报高于高波动性股票时，他们认为我只是犯了一个错误，并希望我消失。我的发现不能是真的，因为理性投资者不应该允许这种情况发生，“市场”应该有一个占主导地位的夏普比率，并且我没有通过广义矩估计或巴拿赫空间来识别它。只需控制价格或大小，并进行排序，就可以找到。

我的潜在顾问的一个关键障碍是，这一发现将意味着许多基金是不理性的。事实上，作为夏普最大化者，他们是不理性的。购买希望是非常普遍的，这就是为什么你会一直收到愚蠢的垃圾邮件的原因：许多白痴会回答这些广告，因为他们认为尼日利亚的某位公爵只需要支付 2000 美元的手续费就能解锁 1000 万美元。

[彭博杂志的问题](http://falkenblog.blogspot.com/2009/10/bloomberg-magazine-shows-market-bias.html)

顶级分析师和年底报告中的顶级基金一直强调“顶级”成就者，即前一年获利最大的那些人。回报从未以任何方式进行“风险调整”。一个仅仅比标普 500 多出 2%的年度业绩的人，但从未在任何一年进入前 10％，可能在第一年业绩不佳时就会失去工作，因为他从未有过能够获得行业内那些自我颁发的可疑奖项的年份（例如，

风险杂志

的年度风险管理者——历史上包括来自安然和世界通信的人）。

我认为人们更适合被描述为羡慕而不是贪婪，这导致了基准设定，并导致了风险溢价的消失。再加上高波动性资产中存在“希望溢价”，高波动性股票基本上在长期仅持有组合中是次优选。

然而，如果你想最大化信息比率，而不是夏普比率，那么以目标为“中间”股票的策略会在收益上稍微提升，同时最小化基准风险。而且

[贝塔 1.0 策略](http://falkenblog.blogspot.com/2010/09/low-volatility-and-beta-10-portfolios.html)

选择了标普 500 指数中与 1.0 最接近的 100 只股票。因此，按构造的方式，其贝塔接近于标普 500 指数。过去 50 年的平均回报如下：

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhQGqswnuBTYPYMEg05jSwJ9FUhMz4NO6Ohq3sG2D5vf8tBFz2zSUaFFFajy7xmT9Vyew2ThDisELFNRZ_GBbcEj8tMkgVFkJyOcLyj9AX0kt1ihG1e1y9QzT7ml7vdkBfLYSvR7Q/s1600/beta1962.gif)**1962 年以来的美国回报率**

|   | Beta1.0 | 标准普尔 500 指数 |
| --- | --- | --- |
| 平均年算术回报率 | 12.9% | 10.5% |
| 平均年几何回报率 | 11.4% | 9.4% |
| 年度标准差 | 17.4% | 15.1% |
| Beta | 1.04 |   |

过去 2 年的平均回报如下：

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg4-AF_jj6R3o2EXYkB6Atnh7Yz6W35-p2MGrThUxfkPVULZk65KRQWb-LoKl9slFFOmAIjEqbMYRmk_GEJov6lThclxkFiXi0lCmTnraS1OWlh4rX6nZAhUgWBJknQ2GZPklmwYg/s1600/beta2009.gif)**2009 年以来的美国回报率**

|   | Beta1.0 | 标准普尔 500 指数 |
| --- | --- | --- |
| 平均年算术回报率 | 18.21% | 13.1% |
| 平均年几何回报率 | 15.7% | 10.8% |
| 年度标准差 | 27.6% | 24.4% |
| Beta | 1.07 |   |

这是一个我认为非常吸引人的新策略。由于大多数投资组合经理既固守其基准，又在几个百分点上表现不佳，这个策略将以一种成本更低、更直接的方式做到这一点，并且在历史上产生了 2%的溢价。
