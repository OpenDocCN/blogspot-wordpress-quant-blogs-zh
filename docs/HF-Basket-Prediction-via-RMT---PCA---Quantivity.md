<!--yml

分类：未分类

日期：2024-05-18 13:53:17

-->

# 通过 RMT / PCA 进行 HF 篮子预测 | Quantivity

> 来源：[`quantivity.wordpress.com/2010/08/22/high-frequency-prediction-via-rmt-pca/#0001-01-01`](https://quantivity.wordpress.com/2010/08/22/high-frequency-prediction-via-rmt-pca/#0001-01-01)

如果*稳健的*主要成分可以在实时中为任意篮子进行识别，并用于 HF*日内*预测呢？这将是高频[市场制度](https://quantivity.wordpress.com/2009/12/31/market-regime-trading-redux/)的精髓。

[田中山胁](http://irene.ike.tottori-u.ac.jp/mieko/profile_e.html)提出了这种方法的新兴存在，并在即将举行的[KES2010](http://kes2010.kesinternational.org/)和[经济物理学研讨会 2010 年](http://www.phys.sinica.edu.tw/~socioecono/econophysics2010/)的[摘要](http://www.phys.sinica.edu.tw/~socioecono/econophysics2010/pdf/TanakaYamawakiAbstract.pdf)中论证了这一点。这项工作依托了 Plerou 等人的研究，他们首次将[随机矩阵理论](http://en.wikipedia.org/wiki/Random_matrix)（RMT，又名随机特征分析）应用于[金融数据中交叉相关性的随机矩阵方法](http://arxiv.org/abs/cond-mat/0108023)。

尽管实时 PCA 的应用概念并不新鲜，但可能新颖的是：使用 RMT 来严格地分离相关信号和噪音，在实时中这样做，并且专注于日内预测。

更具体地讲，Tanaka-Yamawaki 介绍了：

> 一些股票与其他股票存在强烈的相关性……然而，这种相关性的网络不稳定，模式只是临时的。在这种情况下，对网络的详细描述可能并不是非常有用，因为情况很快变化，过去的知识在新环境下已不再有效。然而，如果我们有**一个方法，在很短的时间内提取出表征市场运动主要成分的方法，那么这将给我们提供一个强大的工具来描述市场的时间特征**，并帮助我们建立一个预测这种市场未来走势的时变模型。

这种分析在两个方面似乎有潜在的成果：

+   HF 动态：Plerou 专注于较低频率（30 分钟和日常）收益，因此错过了高频动态。

+   HFT：有趣的是识别哪些（如果有的话）高频交易类型的影响是可见的，因为一些影响不太可能可见（*例如*单个工具的前置交易），而其他一些影响可能是可见的（*例如*指数套利）。

当它们被发布时，阅读这些论文将会很有趣。
