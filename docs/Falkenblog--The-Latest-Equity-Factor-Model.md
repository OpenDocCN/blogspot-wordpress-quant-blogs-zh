<!--yml

category: 未分类

日期: 2024-05-12 21:48:25

-->

# Falkenblog: 最新股权因素模型

> Source: [`falkenblog.blogspot.com/2009/09/latest-equity-factor-model.html#0001-01-01`](http://falkenblog.blogspot.com/2009/09/latest-equity-factor-model.html#0001-01-01)

[陆政](http://www.bus.umich.edu/Academics/Departments/Finance/Finance/FacultyBio.asp?id=000798900)

and Long Chen 有一篇文章似乎引起了相当大的轰动：

[一个更好的解释更多异常的三因素模型](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=1418117)

。当前领先的三因素模型是法马-法伦奇模型，其中包括三个因素：规模、价值和市场。价值因子是通过多头持有价值股票（高账面市值比、低市盈率）和空头持有成长股（低账面市值比、高市盈率）产生的。大小因子是多头持有小盘股，空头持有大盘股。法马-法伦奇方法中交叉制表了规模和增长，以最大程度地提高它们的独立性。市场因子是市值加权市场回报减去无风险利率。

现在，法马和法伦奇创造了这个模型来解释，嗯，它自己。1992 年，他们注意到价值和规模超出了传统的 CAPM，后者仅将市场作为一个因素。因此，增加规模和价值因子解释了按价值和规模分类的股票。如果这似乎是一个解释自身的异常，那就欢迎来到现代金融，其中收益是风险的函数，而风险又是收益的函数。这就好像是通过说一个国家具有高

[索罗余量](http://en.wikipedia.org/wiki/Solow_residual)

。不管怎样，这是自 1980 年以来 CAPM 最突出的异常情况，在大多数国家都能观察到。自首次发现以来，价值效应一直保持强劲，而规模效应随后变得相当小。

但这一模型存在新的异常情况。其中一个异常是

[资本发行异常](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=251502)

，其中，资本发行者-债务或股权-往往表现不佳，而回购的公司往往表现优异。似乎内部人能够预见，或者外部人一直是糟糕的市场定时投资者，或者公司在要求获得他们不能或不愿意自行融资的新投资时，往往会浪费资金。另一个异常是现金流/资产，首次由

[Houge and Loughram](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=886093)

: 过去 6-18 个月内现金流/资产占比高的公司表现优异，现金流/资产占比低的公司表现不佳。另一个是

[动量](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=299107)

: 过去 6-18 个月内拥有高回报的公司在接下来的 6-18 个月内往往表现优异，低回报的股票则相反。此外，过去高回报的公司

[资产增长](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=1360680)

倾向于表现不佳，资产增长较低的公司倾向于表现良好。其中很大一部分是因为互联网泡沫，因为通过收购或发行新股获得大量资产的公司做得比那些没有这么做的公司差，这显然与股权发行异常有关。最后，财务担忧较高的公司

[更高的困境](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=917567)

，由违约指标衡量，表现不佳的公司比表现良好的公司差。基本上，表现优异的公司倾向于是那些即使你不知道估值是多少也会认为是好公司的公司：利润丰厚，违约率低。

现在，张和陈确定了两个用来取代价值和规模的新因素。第一个是投资与资产。这是产业、土地及设备的变化加上库存变化与资产的比率。具有很高 I/A 比率的公司比那些低 I/A 比率的公司具有更高的回报。他们的另一个因素是净收入减去非常项除以资产。ROA 更高的公司比 ROA 更低的公司做得更好。

很明显，他们的新因素是从现有的异常中衍生出来的，因为 I/A 和 ROA 将与财务困境指标、资产增长、资本发行等直接相关。因此，在这种意义上，这种新方法能够‘解释’这些异常并不奇怪，就像价值因子解释价值异常不奇怪一样。令人惊讶的是，这些因素在解释规模和价值组合方面做得比价值和规模因素更好。而且，它对动量组合回报的解释更好。

张和陈认为这是 Tobin's Q 理论的一个直接推论，指出这是“潜在地与风险假设一致的”。他们的基本论点是具有高 ROA 的公司必然具有更高的折现率，否则它们会拥有更多的资产。因此，它们当然会有更高的回报，因为它们具有更高的折现率。如果它们拥有较低的折现率，它们就会发行更多的股票（因为发行股票更便宜），并增加它们的资产，从而降低它们的 ROA。人们也可以认为动量更高的公司具有更高的回报，因为它们具有更高的折现率，而这是自相关的。

我认为‘风险假设’显然是错误的，并提出一个理论论证为什么（参见 SSRN 论文

[这里](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=1420356)

，账目

[这里](http://www.amazon.com/Finding-Alpha-Search-Return-Finance/dp/0470445904/ref=pd_rhf_p_t_1)

). 他们解释的问题在于它与直觉上衡量综合福利的协变量不匹配，比如‘市场’或者 GDP 增长等。风险在理论上完全是关于与我们的随机贴现因子的相关性，如果只是一些特征作为风险的代理，似乎是非常可疑的。可以说，相关性和协变性都是向后看的，比如 Inv/Assets 和 ROA 这样的特征更具前瞻性，但是当你基于这些特征形成投资组合，并在过去 80 年的实时数据中观察它们的相关性时，这些相关性仍然不起作用。
