<!--yml

类别：未分类

日期：2024-05-12 20:32:04

→

# Falkenblog: 哈佛风险谬论

> 来源：[`falkenblog.blogspot.com/2012/04/harvard-risk-confabulations.html#0001-01-01`](http://falkenblog.blogspot.com/2012/04/harvard-risk-confabulations.html#0001-01-01)

约翰·坎贝尔是全球最受尊敬的金融经济学家之一，这意味着他发表的论文非常严谨且广受好评，这些论文表明某些奇怪的结果是风险的函数，尽管该风险指标完全不合直觉。以坎贝尔、吉格里奥、波尔克和特利（2012）的论文为例，题为

[随时间变化的**资本资产定价模型**](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=2021846)

并发现

> 1963 年后的成长股负 CAPM 阿尔法值之所以合理，是因为这些股票为长期投资者对冲了预期股票回报下降和波动性增加的风险。

考虑 1986 年至 2012 年月度数据中股票市场（Rm-Rf）与 VIX 变化之间的相关性：

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgK8DS42CMYY2SB5PduN0G11xmz6xqZjH0urHoXNqkbc12LGXQfe6w61wRWdTI9JXv0mJ5OMSJWEPkkwBnFh2FQ8WnL6ohKN2UWu7NaeNkEWAAkeGtMGg8YUy1yFw9LFszm748PkQ/s1600/rmvix.tif)

存在一种很好的负相关关系，因为市场下跌时波动性上升，反之亦然。这就是为什么通过做多 VXX（VIX 的 ETF）来对冲市场风险的原因（尽管，你

[付出很多](http://falkenblog.blogspot.com/2012/03/vxx-expensive-again.html)

为此！）。

现在考虑 HML 或“

[价值风险代理投资组合](http://mba.tuck.dartmouth.edu/pages/faculty/ken.french/data_library.html)

，它与 VIX 指数有轻微的正相关性，表明

价值

股票在波动性更大的时期具有类似保险的特性，表现更佳。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjIKoWC1VyUWJmdOpARZmz7gU6GiZaRz4g9yaC-lHuOrD31lVZ2Nq_UqKqewCl7_pW_oGHQtjJmpq5w68QN6lajTslmVSjQgDMGVzg2fvmaDG8-Bc4vCu0l_s1DPDZlBxgD86k9Ow/s1600/hmlvix.tif)

也就是说，当波动性上升时，价值而非成长表现更佳，但更重要的是，R²

²

对于这个价值投资组合仅为 2%，而市场对 VIX 变化的回归中为 50%。人们可能会认为，如果正的市场风险溢价有大的负权重，那么小的正效应不会解释价值效应。然而，你可能不熟悉经济学家们广泛使用的强大现代计量经济学方法。

首先，他们选取了 6 个时间序列（综合市场、股票方差、综合市盈率、收益率曲线差、价值投资组合以及 Baa-Aaa 收益率差），并创建了一个向量自回归模型（VAR）。这个 VAR 模型用于估计回报和波动性，进而评估价值/成长型投资组合所承担的风险。该方法采用了一种封闭形式的解决方案，该模型使用了“风险厌恶系数”，这很棒，因为它为你提供了另一个自由参数，并且是一种巧妙的数学技巧。坎贝尔等人随意地指出，“我们模型的实证应用是成功的”，因为存在“合理的偏好参数，使得长期投资者”即使价值股似乎能产生超额回报，也不会轻易投资于价值股。

因此，一个完全不符合直觉的股票回报溢价和波动性风险因素的模型，在给定某些未观察到的参数的情况下，可以解释价值溢价。然而，股票回报溢价和波动性本身并不能解释任何问题。

鉴于我对金融和宏观经济的理解，我对那些声称他们的模型运作良好的弦理论家持高度怀疑态度，因为如果你给学者任何一组程式化的事实（例如，价值效应、物理学的基本事实），更多的数学可以自信地解释它。根据我后续的虚构研究，

[已经宣传了数周，](http://www.amazon.com/Whos-Charge-Free-Science-Brain/dp/0061906107/ref=sr_1_1?s=books&ie=UTF8&qid=1331592463&sr=1-1)

只要能合理化他们的偏见，他们就会认为某事是成功的，这并不太难。
