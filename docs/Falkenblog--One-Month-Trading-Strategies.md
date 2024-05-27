<!--yml

类别：未分类

日期：2024-05-12 19:57:35

-->

# Falkenblog：一个月交易策略

> 来源：[`falkenblog.blogspot.com/2022/06/one-month-trading-strategies.html#0001-01-01`](http://falkenblog.blogspot.com/2022/06/one-month-trading-strategies.html#0001-01-01)

Robeco 的量化投资团队中约有一半最近发表了一篇关于月度交易策略的简短论文（参见 Blitz *et everybody* [Beyond Fama-French Factors: Alpha from Short-Term Signals Frequencies](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=4115411)）。我可以想象这些家伙一直在讨论这些事情，最终有人说，“这将成为一篇不错的论文！”

“短期”指的是一个月的交易周期。任何低于一个月的周期都不会与“价值”等标准量化因素有重叠，因为它们涉及不同的数据库：分钟甚至是刻度数据，二级报价。它们的扩展性较差，交易量较大，使得它们更多地属于对冲基金而不是大型机构基金的领域。或者，超短期模式可以包含在执行桌的策略中，其中任何 Alpha 都会反映在较低的交易成本中。

该论文使用了 MSCI World 数据库对五个知名的异常情况进行了分析，该数据库涵盖了发达国家交易量最大的前 2000 只股票。

1.  月度均值回归。见[Lehman（1988）](https://www.nber.org/system/files/working_papers/w2533/w2533.pdf)。t 月的收益意味着 t+1 月的低回报。

1.  行业动量。见[Moskowitz 和 Grinblatt（1999）](http://stat.wharton.upenn.edu/~steele/Courses/956/Resource/Momentum/MoskowitzGrinblatt99.pdf)。这激励作者对上面提到的均值回归异常进行行业调整，使其更加独立。

1.  过去一个月的分析师盈利调整。基于[Van der Hart、Slagter 和 van Dijk（2003）](https://www.econstor.eu/bitstream/10419/85812/1/01009.pdf)。这个信号使用了上调盈利调整次数减去下调盈利调整次数，除以过去一个月的分析师总数。这与行业动量类似，这意味着投资者的低反应。

1.  同一月季节性股票回报。见[Heston 和 Sadka（2008）](https://w4.stern.nyu.edu/finance/docs/pdfs/Seminars/063f-sadka.pdf)。该策略基于一些股票在特定月份表现良好的观点，比如四月。

1.  高一个月的特异性波动性预示着低回报。见[Ang、Hodrick、Xing 和 Zhang（2006）](https://www.nber.org/system/files/working_papers/w10852/w10852.pdf)。这通常会是一个长期低波动、短期高波动的组合。

所有这些异常情况最初记录的月度超额收益约为 1.5%，如预期的那样，现在被认为充其量是这个数字的三分之一；至少它们不是零，就像大多数已发表的异常情况那样。

有趣的是，莱曼的论文记录了 20 世纪 90 年代蓬勃发展的盈利‘配对交易’策略背后的负周和月自相关性。 [Lo and Mackinlay](https://academic.oup.com/rfs/article-abstract/1/1/41/1601244) 在 1988 年也注意到了这一模式，尽管他们的重点是测试随机行走，所以你必须在字里行间看出其中的意思。DE Shaw 那时也通过这个策略赚了很多钱，所以也许贝佐斯用这个策略资助了亚马逊。这个策略的一个流行版本是配对交易，例如，如果可口可乐下跌而百事平盘，那么就买入可口可乐并卖出百事。在互联网泡沫破裂后的 2003 年左右，配对交易变得不那么有利可图了。然而，这是一个很好的例子，展示了一篇学术论文对于那些足够敏锐看出其真实价值的人是很有价值的（需要注意的是，莱曼的简单策略从来没有成为一篇备受推崇的学术论文）。

关于 DE Shaw，值得一提。当他们用这个简单的策略赚了很多钱后，他们没有告诉任何人。他们会告诉面试者他们使用了神经网络，这是类似于当今的人工智能或机器学习的概念：时髦而模糊。我亲眼见证了这种伪装策略几次，其中一个交易员的优势是*x*，但他会告诉其他人一个似是而非的与*x*无关的事情。不出所料，所谓的优势比真正的优势更加复杂和老练（例如，“我使用卡尔曼滤波器估计生成动态阿尔法的潜在高频因素”与“我根据上周的行业调整收益购买 50 个失败者和卖出 50 个赢家”）。

如果每个策略都能产生 0.5%的月收益，那么考虑将它们组合起来能有多好是很有趣的。下面是这些单一策略收益相关性的矩阵。可以看到，通过使用行业调整收益，月度均值回归信号变得与行业动量显著负相关。尽管我喜欢减少直接抵消效应的想法（高行业收益 —> 做多; 高收益 —> 做空），但我对负相关性有多高感到不安。在金融领域，解释变量之间的高相关性表明冗余和缺乏有效的分散化。

*STR= 短期均值回归, IND_MOM= 行业动量, REV30D= 分析师修订动量, SEA_SAME= 季节性同月, iVOL= 一个月特异波动性。*

他们的多因素方法将输入数据标准化成[Winsorized](https://zh.wikipedia.org/wiki/%E6%96%87%E6%81%A9%E6%89%80%E5%88%86%E5%B8%83) z-分数并相加。这种"标准化并相加"的方法是在没有强有力理论支持时创建多因素模型的坚固方式（例如法玛-法伦因子与布莱克-斯科利斯）。Robyn Dawes 在这里为这种技术提出了论据[（点击此处查看原文）](https://www.cmu.edu/dietrich/sds/docs/dawes/the-robust-beauty-of-improper-linear-models-in-decision-making.pdf)。他的论文被收录在 Kahneman，Slovic 和 Tversky 的开创性论文[《不确定条件下的判断》](https://www.cambridge.org/core/books/judgment-under-uncertainty/6F9E814794E08EC43D426E480A4B412C)中，这是 1982 年出版的一本关于偏见的文章集。相比之下，多元回归权重（系数）会受到因素之间的协方差以及与解释变量的相关性的影响。这些异常值仅因其与未来回报的相关性而为人所知，而不是它们互相之间的相关性。因此，在*先验*排除它们的相关性效果是避免过度拟合的一种有效方式，就像线性回归限制并主导大多数其他技术一样（简单就是聪明）。关键是将显著的预测因子标准化为可比较的单位（例如 z-分数、百分位数）并相加。

我应该注意到，著名的因子量化专家[Bob Haugen](https://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.475.4056&rep=rep1&type=pdf) 在 21 世纪初应用了更复杂的回归方法来对因素进行权重，结果一塌糊涂。这就是为什么我不认为 Haugen 是低波动性投资的[OG](https://www.urbandictionary.com/define.php?term=OG)。他是第一个指出低波动性与高于平均回报相关的人之一，但他将这一发现埋在了另外十几种因素中，每种因素都有数种变体。他在 2003 年左右推销了一套 50 个因素给我的老公司 Deephaven，使用滚动回归，低波动性因子的因子载荷在正负之间反弹；该模型宣传过去 20 年每年 20%以上的历史回报，但我见到它从未奏效。

我不是绝对反对对因素进行加权；我只是认为像 Robeco 在这里所做的那样采用简单的"标准化并相加"方法是最好的，并且通常需要非常深思熟虑地限制交互效果（例如，不要只是将它们扔到一个机器学习算法中）。

该论文记录了交易成本，这将使策略产生零回报以解决这个问题。这种方法的一个好处是调整事实，即一些实现的周转率比其他低，因此策略的这个方面随后包含在测试中。下图中的 y 轴表示使策略产生零超额收益所需的单程交易成本。合并信号几乎使回报翻倍，这是有道理的。你不应该期望*n*因子模型比 1 因子模型好*n*倍。

<图片>![</图片>](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fbucketeer-e05bbc84-baa3-437e-9518-adb32be77984.s3.amazonaws.com%2Fpublic%2Fimages%2F8aa65807-afc3-4639-852d-835d816995c6_471x278.png)

来自 Blitz et al

他们指出一些简单的退出规则可以减少周转率，从而降低交易成本，而不是降低总体回报。因此，在下图中，没有单一异常可以克服其交易成本，但多因素方法可以。此外，您可以对入场和出场规则进行直接调整，即使减少总回报（极右列与中间列相比），仍然可以增加净回报。

<图片>![</图片>](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fbucketeer-e05bbc84-baa3-437e-9518-adb32be77984.s3.amazonaws.com%2Fpublic%2Fimages%2F8d34ed88-9332-4985-83d8-06d88da23bd6_458x263.png)

来自 Blitz et al

他们还提供了关于仅限多头实施的数据，并发现总的超额回报减少了一半，这表明结果不是由空头推动的。这一点很重要，因为很难得到完整的历史数据集，即使以任何利率也不能做空许多客观上不好的股票。

我对他们的结果持谨慎态度有几个原因。首先，考虑下面图表来自 Hesten 和 Sadka（2006）关于月度季节效应的论文。这显示了对单个股票的先前月度回报的平均滞后回归加权。注意显著的 12 个月的峰值，好像一支股票在持续 20 年的特定最佳月份。这种效应随着时间的稳定看起来太持久，以至于看起来像是测量问题而不是真实回报。

<图片>![</图片>](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fbucketeer-e05bbc84-baa3-437e-9518-adb32be77984.s3.amazonaws.com%2Fpublic%2Fimages%2F2a98dbd1-ea57-42d9-a567-25ae4f4cf86a_456x287.png)

来自 Hesten 和 Sadka（2006）

这个文献中的另一个问题是，将“阿尔法”或残差呈现给因子组合往往更好地被视为对错配模型的反映，而不是超额回报。请注意，这些模型中最大的因子是 CAPM 贝塔。我们知道贝塔最多与横截面回报不相关。因此，你可以通过相对于所有人都知道有系统偏差的预测来定义这个术语，从而轻松产生大量的“超额回报”（即高贝塔股票应该做得更好，但实际上并不是这样）。你可以创建一个零贝塔组合，将其添加到一个贝塔=1.0 组合，似乎可以创建一个占主导地位的组合，但这并不明显。这些倾斜的时间变化特异风险不能被分散掉，并且可能降低一个简单市场组合的夏普率。

<picture>![</picture>](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fbucketeer-e05bbc84-baa3-437e-9518-adb32be77984.s3.amazonaws.com%2Fpublic%2Fimages%2Fd86eca35-f4e6-4e18-b26d-8ecbe20ed46b_752x452.png)

美国股票按 CAPM 贝塔值预排序，2000-2020

有趣的是，Larry Swedroe[最近讨论了](https://twitter.com/larryswedroe/status/1532753750573604864)[Medhat and Schmeling (2021)](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3150525)的一篇论文。他们发现，月度均值回归仅适用于低换手率股票；对于高换手率股票，效果是找到相反的月度动量。我没有看到这一点，但这凸显了这些研究中的许多自由度。你如何定义“超额”回报？你的宇宙中有多大的切割？你使用了什么时段？你包括了日本吗（他们的股市模式和电视游戏节目一样奇怪）？

Robeco 的文章提供了一个不错的基准，并概述了一个简单的组合策略。如果你持怀疑态度，你可以简单地将它们添加到你的入场和出场规则中。
