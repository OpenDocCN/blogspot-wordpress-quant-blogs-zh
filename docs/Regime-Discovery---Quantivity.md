<!--yml

类别：未分类

日期：2024 年 05 月 18 日 13:53:39

-->

# 制度发现 | 量化

> 来源：[`quantivity.wordpress.com/2010/02/15/regime-discovery/#0001-01-01`](https://quantivity.wordpress.com/2010/02/15/regime-discovery/#0001-01-01)

在考虑[市场制度](https://quantivity.wordpress.com/2009/12/31/market-regime-trading-redux/)时，许多交易者首先考虑宏观原则：商业周期、风险偏好、利率、流动性、市场波动性，*等等*。这种观点是通过将[群体行为](http://en.wikipedia.org/wiki/Herd_behavior)应用于市场动态来激发的：当许多人以和谐（趋势）或不和谐（范围）的方式进行交易时，就会出现制度。从这个意义上说，群体行为是制度的一个[不可观察的](https://quantivity.wordpress.com/2010/02/15/trading-the-unobservable/)因素。

然而，这种解释对交易来说并不是非常有见地：要么必须预测未来，要么接受利用已建立的趋势（*即*宏观经济预测或趋势跟随）。尽管这两种策略都在积极交易，但利润往往难以预测。

另一种方法是尝试构建*制度发现*模型，它可以在形成早期量化地定量地识别制度，并概率地指导如何在群体之前交易（无论是秒还是天）。例如，HP、VGT 和 DJIA 的价格或波动性如何随 IBM 价格变化而变化。或者，USD 交叉盘如何对未观察到的美联储干预做出反应。

如何构建这种类型的发现模型并不明显。以下是一个草图，鼓励读者发表评论。

从以下假设开始：

> 制度发现通过[二阶因果](https://quantivity.wordpress.com/2010/01/10/causality-exogeny-regimes/)信息传播推动价格和波动率。

换句话说：一个证券的价格变化将导致一个或多个其他证券的价格相应变化。或者，类比地说；想象一下湖中扔一块小石头：

+   湖：*可观察变量*的宇宙，由来自世界各地交易所和场外交易的所有时间序列组成（尽管零售交易者无法访问此宇宙，但对于连接良好的量化 HF 而言，此宇宙是可用的）

+   小石头：导致*单个*工具在*单个*时间点价格变化的事件

从这个角度来看，制度发现需要一个模型，描述多个工具之间的价格如何随时间顺序变化以响应单个工具的价格变化（*即*一个工具之间的顺序价格模型）。因此，一个相应的模型应该潜在地适用于任何交易多种证券的市场，这些证券的价格据信是由信息传播驱动的：

+   股票：一个工具的价格变化导致其他工具的价格/波动性变化，原因包括 ETF 组合、配对交易、套期保值，*等等*。

+   外汇：央行干预导致更新的报价/交易在经销商之间传播

+   ir: 中央银行利率变动导致信贷和股票工具的价格/波动变化。

表示不同证券间序列价格/波动变化模型的研究值得关注。 [Tr8dr](http://tr8dr.wordpress.com/) 最近撰写了几篇应用聚类和相关性的有趣帖子，包括[资产间相关性的最小生成树](http://tr8dr.wordpress.com/2009/12/28/10-years/)和[股票聚类](http://tr8dr.wordpress.com/2009/12/30/equity-clusters/)。较早的文献包括[Zoran Obradovic](http://www.ist.temple.edu/%7Ezoran/)（1990 年代中期）、[Takayuki Mizuno](http://en.scientificcommons.org/takayuki_mizuno)和[Laszlo Gillemot](http://en.scientificcommons.org/laszlo_gillemot)的有趣文章。
