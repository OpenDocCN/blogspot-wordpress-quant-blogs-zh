<!--yml

类别：未分类

日期：2024-05-18 13:52:19

-->

# 投资组合理论已死，现在怎么办？| Quantivity

> 来源：[`quantivity.wordpress.com/2011/04/10/portfolio-theory-is-dead-now-what/#0001-01-01`](https://quantivity.wordpress.com/2011/04/10/portfolio-theory-is-dead-now-what/#0001-01-01)

读者经常问量化投资公司 Quantivity 对*长期*量化策略的看法，以及相应现代投资组合理论（[modern portfolio theory](http://en.wikipedia.org/wiki/Modern_portfolio_theory)）和资产配置（战略和[tactical](http://en.wikipedia.org/wiki/Tactical_asset_allocation)）的相关性。简而言之，Quantivity 对现代投资组合理论和资产配置并不是很感兴趣。

话说回来，全面理解这些理论为什么是错误的以及如何出错是有洞察力的，对于短期和长期量化策略都是相关的。这一观点是基于标准机构和个人投资组合管理，如[Grinold 和 Kahn](http://books.google.com/books?id=a1yB8LTQnOEC)和[Faber](http://www.theivyportfolio.com/)，以及经济学和金融学的学术背景。

尽管有 intellectual tradition，但大量的相反证据实在是太压倒性了：

+   几十年来的[CAPM](http://en.wikipedia.org/wiki/Capital_asset_pricing_model)反例。

+   全球范围内跨资产的相关性不断增加，显著降低了多样化（[diversification](http://en.wikipedia.org/wiki/Diversification_%28finance%29）的效率。

+   两个市场泡沫，在科技和金融领域充分验证了[行为金融](http://en.wikipedia.org/wiki/Behavioral_economics)的有效性。

+   自 2007 年以来，跨多个市场的量化一直在迅速加速。

+   “波动性”作为一种提议的资产类别的兴起，回溯到 2003 年的[Derman](http://www.ederman.com/new/docs/gaim-trading_volatility.pdf)。

甚至 Kahn 去年还在[Quantitative Equity Investing: Out of Style?](https://www2.blackrock.com/webcore/litService/search/getDocument.seam?ContentID=1111105185)一文中发表了评论。

所有这些都指向金融经济学的一个基本猜想：接受逐渐增加的“风险”需要相应更高的回报作为补偿。或者说，用行话来说：风险溢价（[risk premium](http://en.wikipedia.org/wiki/Risk_premium)）非负且在增加。这个猜想是均值-方差优化、多样化、基准设定、指数投资以及现代零售投资的大部分理论基础。

然而，*证据强烈表明这个猜想是错误的*。

考虑到这一点，相关实际影响是什么？由于这一猜想的错误，对量化策略的影响有几个方面需要考虑，这取决于您的投资期限：

+   长期：投资组合优化、泡沫、嫉妒效用函数和彩票股票。

+   短期：波动性偏见、方差最小化、对称损失和政体指标。

后续文章将扩展这些考虑，从最小方差组合（MVPs）开始。

为了激发对这个话题的兴趣，博客圈中的[Falkenblog](http://falkenblog.blogspot.com/)和[Estimation Risk](http://estimationrisk.blogspot.com/)都是直言不讳的倡导者。在机构方面，[Clarke](https://www.aninvestor.com/analytic-people/index.aspx#8)和[de Silva](https://www.aninvestor.com/analytic-people/index.aspx#8)来自[Analytic Investors](https://www.aninvestor.com/)以及[Robeco](http://www.robeco.com/)的 Pim van Vliet 都在积极发表文章。MSCI Barra 提供了关于[全球最低波动率](http://www.msci.com/products/indices/stategy/minimum_volatility/)的指数。

这个话题也涉及到正在进行量的主题[市场制度](https://quantivity.wordpress.com/2009/12/31/market-regime-trading-redux/)，如[Scherer](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=1681306)（2010，第 6 页）：

> 存在两种股票市场制度的证据。两者各自呈正态分布，但结合在一起则呈非正态。由于信贷危机对这两个时间序列的负面影响，这一时期的夏普比率接近于零。

如果确实如此，那么 MVP 的*过去*表现作为*事前的*市场*制度指标*具有有趣的潜力。再次，从[Scherer](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=1681306)（2010，第 5 页）：

![scherer-mvc-regime-indicator](https://quantivity.wordpress.com/wp-content/uploads/2011/04/scherer-mvc-regime-indicator.png)

以下文章值得对市场制度提出质疑的读者考虑，这些文献最近汇聚到将最小方差作为优于[Markowitz](http://en.wikipedia.org/wiki/Harry_Markowitz)-衍生模型的投资组合构成指导原则：

+   [资本化加权股票组合的有效市场无效率](http://www.iijournals.com/doi/abs/10.3905/jpm.1991.409335)，由 Haugen 和 Baker（1991）撰写

+   资产回报、特异性方差与共同基金](http://www.efalken.com/papers/EF%20Dissertation.pdf)，由 Falkenstein（1994）撰写

+   [股票市场中的不对称波动与风险](http://ideas.repec.org/p/nbr/nberwo/6022.html)，由 Bekaert 和 Wu（1997）撰写

+   关于投资组合优化：预测协方差和选择风险模型](http://bear.warrington.ufl.edu/karceski/research%20papers/rfs%20winter%201999.pdf)，由 Karceski *等*（1999）撰写

+   [大投资组合中的风险降低：为什么实施错误的约束有助于](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=424756)，由 Jagannathan 和 Ma（2002）撰写

+   [波动率与预期回报的横截面](http://www.afajof.org/afa/forthcoming/ang1.pdf)，由 Ang *等*（2004）撰写

+   美国股票市场中的最小方差组合](http://www.iijournals.com/doi/abs/10.3905/jpm.2006.661366)，由 Clarke，De Silva 和 Thorley（2006）撰写

+   [波动率和预期回报的横截面](http://www0.gsb.columbia.edu/faculty/rhodrick/crosssection.pdf)，作者：Ang 等（2006 年）

+   [总体特异风险和市场回报](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=947873)，作者：Bali 和 Cakici（2006 年）

+   [估计全球最小方差投资组合](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=940367)，作者：Memmel 和 Kempf（2006 年）

+   [波动效应：降低风险而不降低回报](https://www.robeco.com/com/eng/images/blitz-vliet_jpm_robeco_2007_tcm633-252202.pdf)，作者：Blitz 和 van Vliet（2007 年）

+   [一般中的风险和回报：理论与证据](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=1420356)，作者：Falkenstein（2010 年）

+   [最佳与天真的分散化：1/N 投资组合策略有多低效？](http://faculty.london.edu/avmiguel/DeMiguel-Garlappi-Uppal-RFS.pdf)，作者：DeMiguel 等（2009 年）

+   [用鲁棒估计改进投资组合选择](http://www.est.uc3m.es/fjnm/esp/papers/RobustPortfolios.pdf)，作者：DeMiguel 和 Nogales（2009 年）

+   [投资组合优化的一般方法：通过限制投资组合规范来提高性能](http://www.est.uc3m.es/fjnm/esp/papers/DGNU.pdf)，作者：DeMiguel 等（2009 年）

+   [波动率和偏斜的定价：一种新的解释](http://www.iijournals.com/doi/abs/10.3905/JOI.2009.18.3.027)，作者：Bradford（2009 年）

+   [等权风险贡献投资组合的特性](http://www.iijournals.com/doi/abs/10.3905/jpm.2010.36.4.060)，作者：Maillard、Roncalli 和 Teïletche（2010 年）

+   [最小方差投资组合构成](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=1549949)，作者：Clarke、De Silva 和 Thorley（2010 年）

+   [最小方差投资的新视角](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=1681306)，作者：Scherer（2010 年）

+   [股票回报序列依赖性和样本外投资组合表现](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=1572526)，作者：DeMiguel 等（2010 年）

+   [反对贝塔的赌注](http://www.utahwfc.org/2011_papers/betting.pdf)，作者：Frazzini 和 Pedersen（2010 年）

+   [最小方差的变种](http://qwafafew.org/images/uploads/2011-03-16-ny-Falk.ppt)，作者：Falk（2011 年）

+   [预期特异偏斜](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=1541002)，作者：Boyer、Mitton 和 Vorkink

+   [风险和回报之间令人困惑的关系](http://qwafafew.org/images/uploads/2011-03-16-ny-Luo.pdf)，作者：罗伊等（2011 年）

+   最小方差：揭示“魔力”，作者：Alvarez 等（2011 年）

+   [利用期权隐含波动率和偏斜改进投资组合选择](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=1474212)，作者：DeMiguel 等（2011 年）

+   [基准作为套利的限制：理解低波动性异常](http://people.hbs.edu/mbaker/cv/papers/Benchmarks_as_Limits_unpub_01_14_10_faj.v67.n1.4.pdf)，作者：Baker（2011 年）
