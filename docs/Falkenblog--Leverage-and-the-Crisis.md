<!--yml

类别：未分类

日期：2024 年 05 月 12 日 22:19:37

-->

# Falkenblog: 杠杆与危机

> 来源：[`falkenblog.blogspot.com/2009/03/leverage-and-crisis.html#0001-01-01`](http://falkenblog.blogspot.com/2009/03/leverage-and-crisis.html#0001-01-01)

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhH7OovF74pSyyEiO8Q5oIOuURHKZHTvRGpUEhn9ZkC54_ZBMRnThFSoH8oYo5PzQH1-41yrowjPoja6zC20jxwD4hZKS-CnVT62H5WnBA8tnv66sv52d4c2EjkRJsOqgha6cNmZg/s1600-h/archimedes_lever_2.jpg)

最近的危机导致了一大批关于罪魁祸首的文章产生：傲慢、过少的监管、政府鼓励向贫困地区放贷，

[信用违约掉期](http://econlog.econlib.org/archives/2008/12/no_further_ques.html)

,

[维京海盗的男子气概](http://www.vanityfair.com/politics/features/2009/04/iceland200904)

,

[Copula 模型](http://www.wired.com/techbiz/it/magazine/17-03/wp_quant?currentPage=all)

, 监

[监管资本要求](http://online.wsj.com/article/SB123086073738348053.html)

,

[风险值](http://falkenblog.blogspot.com/2008/12/taleb-blames-var-merton-scholes-for.html)

,

[巴塞尔 2 监管协议](http://isitonlyme.wordpress.com/2008/10/11/basel-2-and-its-impact-on-the-global-financial-crisis/)

,

[格林斯潘的宽松货币政策](http://www.researchmag.com/Issues/2008/10/Pages/Greenspan-s-Legacy.aspx)

,

[太大而无法倒闭](http://www.nytimes.com/2008/07/20/weekinreview/20goodman.html)

, 中国投资，不对称奖金，

[《格拉斯-斯蒂格尔法》的废除](http://bubblemeter.blogspot.com/2008/09/bill-clinton-is-right-about-glass.html)

, 最终金融机构的过度杠杆。杠杆，英国人称之为'gearing'，是资产与股本的比例（想想阿基米德）。我一直在研究基于财务比率的银行违约模型，以及评级、股本回报或利差与杠杆的关系，对于银行来说，历史上没有太多相关内容。历史上，杠杆并不是金融机构表现的一个强有力指标（对于非金融机构有效），这并不是说无关紧要，只是观察到的杠杆比率代表各种问题的均衡解决方案，而剩余的横截面相关性通常没有信息意义。自

nature

资产和负债的关系远比资产负债表显示的更重要，这也是为什么我不积极交易金融机构。银行的财务报表太复杂，没有用，这是导致这一危机恶化的原因之一，因为他们现在无法证明自己并不破产。

首先考虑一个做多 BBB（Baa）债券，做空 AAA（Aaa）债券的策略的回报。下面列出了该策略的总回报。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiVU-TGy1A66Y7GJOMVCCJnp3Qc1ghgMCVsHNc5C6DcqCtPg1gZwBG2QSOKli8-amCYRK_KKnFAoL7P0NRV-i9PYc8uDwLpjpEeoyY1Lcvb7sGdZGzG99NnwQNc-6Zdtd95kOkgKA/s1600-h/maxdraw.jpg)

请注意，这种策略通常情况下是赚钱的。事实上，这是一个著名的金融难题，因为这种交易的回报比通过标准效用函数产生的回报高。也就是说，年化夏普比率约为 0.4，这大约是股票市场的夏普比率，这本身就产生了众所周知的'股票溢价难题'。

还要注意的是，这种策略的回撤随时间而变化。在大萧条（1930 年代）时约为 20%，最近经历了 15%的回撤。可以想象有人会认为大萧条不再是一个相关的基准，如果是这样，那么 6%的回撤就是一个合理的最坏情况。现在，大多数投资者在最坏的情况下都将资本应用于约 3 倍，这意味着使用宽松的 6%最坏情况，资本为 18%。每年的回报仅为 1.4%，因此在 18%的资本上的 1.4%回报（这些是发行价格债券的函数）约为经济资本的 7.8%的回报，对于一个充满不确定性的东西来说，这通常不是一个好的投资。因此，虽然从夏普比率上看这可能是一个难题，但由于债券中的长尾峰度（下行肥尾），一个不应该将风险资本作为标准差函数，而是一个压力测试，这在这种情况下使这成为一笔糟糕的交易（遗憾的是，效用函数理论家侧重于标准差）。这种策略只在以下情况下对银行有意义：1）不按市值计量和 2）通过贷款服务产生辅助收入。

因此，我确实感到困惑，很多银行最终基本上拥有高度杠杆头寸，即买入高评级抵押贷款，该抵押贷款由银行融资利率（通常为 A 级信用）资助，因为即使这场危机没有发生，BBB 评级的抵押贷款支持证券也没有出现违约，标准的 BBB-AAA 利差变化也能够让投资者遭受损失。我怀疑很多人，像瑞银一样，是通过先收购证券再打包成中级证券并以高利润出售，但后来却被困在高评级证券中，通过查看历史上的 BBB 违约率并忽略市值认为这不是问题。无论如何，如果他们想'套利'AAA-BBB 利差，他们的杠杆比率就应该是 5.5:1（1/0.18），因此，投资银行的实际高杠杆率意味着他们没有关注利差波动，而与违约率和房价假设无关。

但这是否是我们金融灾难的关键呢？难道他们仅仅是增加了 30 倍的杠杆来套利一些薄的投资级信用利差吗？观察投资银行的杠杆比率（资产/净资产），我们可以看到，雷曼兄弟、美林和熊斯登在 2007 年 12 月左右均在 30 左右。然而，他们在 1995 年也是这个水平。当然，像花旗银行和摩根士丹利这样的银行，在此期间大幅增加了杠杆，但这些都是例外。因此，一般情况下，并没有出现杠杆大幅增加的情况，因为这只局限在少数几家投资银行。然而，我们确实看到了杠杆与股票收益之间的关系。根据 2006 年时市值超过 10 亿美元的所有美国投资银行，并从 2006 年到现在观察股票收益，我们看到了一个温和但显著的负相关关系。更高的杠杆意味着未来市场下跌幅度更大。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg9DqyQizZk1bXbjX90FBYJW3Bmbr7wGcEDuV8n1Sh9dd1zIhJEjIFprt_VWI5jR24LBFJByu6AeuOS6AQIMuZpTMsqbSv-sOP_1r3OIcklfvF9oS2-fEcHH2f-y5pMLDRf2GjYDQ/s1600-h/invbank.jpg)

但这些都是投资银行，当电视上有人说“银行家”时，他们通常指的是“投资银行家”，这完全是不同的事物。银行家们的收入并不高，除非是最高层的人士，他们也不是你传统的‘宇宙掌控者”。他们了解贷款承销和服务的细节，而不是交易和做交易。商业银行的杠杆比率在过去十年里有所下降，从平均 12 左右降至 10 左右。大多数银行都是商业银行，不是投资银行。我们看到 2006 年时杠杆和随后股市表现之间几乎没有关系（使用那些 2006 年时市值超过 10 亿美元的美国银行）。这是一个典型的银行关系，通常情况下，净杠杆贷款，不会与评级、利差和其他财务表现指标等事务相关联。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiduGah5q25x2gIekHWQmqhMfI4mUtkFmpvODknQorovkB_pvJlx4-mv4KclKunO_Q6Roajtkz_BYognbB9QKc_HoumlcpYH4lVqZKlyjwHLwCDo7EzhMS0fQYFvN1jSxRX7vgP9w/s1600-h/commbank.jpg)

因此，我认为那些储存了大量交易市场 BBB 评级债务的投资银行正在做一个糟糕的交易，并且将杠杆运用得太高了。这似乎解释了这些公司的一些问题。然而，大多数银行都没有增加杠杆，商业银行的杠杆和未来的收益之间几乎没有关系，因为自 2006 年以来两者市值已经下降了约 60%。因此，尽管杠杆还是有些相关性，但在大局中，这是一个次要问题。

关键在于抵押贷款的质量，对于观察财务报表的投资者来说，2006 年时银行的抵押贷款资产性质基本上零有意义的信息。
