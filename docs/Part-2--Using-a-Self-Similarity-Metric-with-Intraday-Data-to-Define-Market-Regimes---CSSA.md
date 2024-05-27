<!--yml

分类：未分类

日期：2024-05-12 17:47:31

-->

# 第二部分：使用自相似性指标与日内数据定义市场体制 | CSSA

> 来源：[`cssanalytics.wordpress.com/2015/04/17/part-2-using-a-self-similarity-metric-with-intraday-data-to-define-market-regimes/#0001-01-01`](https://cssanalytics.wordpress.com/2015/04/17/part-2-using-a-self-similarity-metric-with-intraday-data-to-define-market-regimes/#0001-01-01)

自相似性指标系列一直很受欢迎。最近，Jeff Swanson 的流行网站[System Trader Success](http://systemtradersuccess.com/)分享了一篇原始文章，该网站涵盖了关于交易系统开发的一系列发人深省的 articles，非常值得一读。Jeff 还发布了一些 TradeStation 代码供指标使用，一些读者可能会发现这些代码很有价值。在垂直博客的一个极好例子中，Mike Harris 在他的[Price Action Blog](http://www.priceactionlab.com/Blog/2015/04/performance-in-stable-and-chaotic-markets-based-on-the-cssa-regime-indicator/)上对自相似性指标进行了一项非常有趣的分析，该博客还有很多其他有趣的 articles，值得关注。

我必须说，这个博客最令人满意的方面之一是与不同水平的读者（和博主）的互动。多年来，我发展了几种关系，其中一些发展成了新的商业机会。很多年前，在积极运营 CSS Analytics 时，我有幸与一群非常有才华和敬业的人合作。很高兴看到其中许多人已经在定量领域取得了相当的成功。那个才华横溢小组的原始成员之一是 David Abrams。多年来，我们在系统开发上投入了大量时间，尽管我们不再积极合作，但我们仍然设法保持联系。David 与我分享了一些关于我最近在博客上介绍的混沌/稳定性自相似性指标的视觉和分析。我建议我们为 CSSA 读者发布这个内容，他非常友好地同意分享。

**Dave Abrams 是 Wilbanks, Smith and Thomas 资产管理公司（www.wstam.com）在弗吉尼亚州诺福克市的定量策略总监，该公司设计风险管理的基金模型和标普指数（该公司的 25 亿资产中有大约 4 亿是定量）。他之前是 CSS Analytics 定量研究小组的一部分。**

**可视化混沌稳定性指标**

在 Tradestation 图表中可视化 DV 的新自相似性体制方法很有用。以下是使用默认参数（N = 10 天，60 天平均值，252 百分比排名长度）的策略和指标。我将指标值减去 0.5 以使值围绕 0 居中，并以彩色直方图显示。

以下是 SPY 上的混沌稳定性作为买入/卖出指标的样子：

![pic 1](https://cssanalytics.files.wordpress.com/2015/04/pic-1.png)

当前指标处于新的“卖出”位置，因为其值低于零。

这可能反映了我们过去几个月更随机和横向的市场运动。与任何指标一样，这个看跌信号并不完美，并且在 2014 年 4 月至 7 月初，尽管混沌稳定性值深陷红色，但市场仍取得了良好的上涨。查看一些其他图表有助于了解买入和卖出信号何时发生。

![pic2](https://cssanalytics.files.wordpress.com/2015/04/pic2.png)

![pic3](https://cssanalytics.files.wordpress.com/2015/04/pic3.png)

![pic 1](https://cssanalytics.files.wordpress.com/2015/04/pic-1.png)

![pic4](https://cssanalytics.files.wordpress.com/2015/04/pic4.png)

如果不仔细检查，很难看出发生了什么，但似乎混沌/稳定性指标在市场持续向下移动或持续牛市向上移动走出修正或在建立的上涨趋势顶部时闪烁买入信号。卖出信号往往出现在市场顶部附近，此时市场波动较大或在市场在其长期趋势内横向移动的区域。由于持续性在上涨和下跌移动中都存在，信号与趋势跟踪策略不相关或甚至呈负相关，如原始帖子中所强调。这对于那些希望在单一资产上多样化趋势策略的人来说很重要。

**平滑混沌稳定性指标**

当我查看图表时，我注意到指标经常从买入变为卖出-尤其是当值在接近零时波动。平滑似乎是一个合理的办法来减少一些摆动交易并减少周转率。为了解决这个问题，我将约翰·埃勒的超级平滑方法（http://traders.com/Documentation/FEEDbk_docs/2014/01/TradersTips.html）应用于混沌稳定性测量。注意下面的指标。这减少了 11%的交易数量，并将盈利因子提高了 6 %。

![pic5](https://cssanalytics.files.wordpress.com/2015/04/pic5.png)

**前进测试分析**

新指标的一个挑战是，它们往往承诺很多，但在现实世界中却未能兑现。通常这种情况发生的原因是因为开发者提供的例子是针对特定的一组参数进行调整的——换句话说，这个指标是过度拟合的，不够健壮。那么 DV 的创新新指标只是幸运，还是稳定的呢？评估一个指标是否具有预测能力的一个最佳方法就是进行前瞻性测试。没有预测能力的指标往往会在这种测试中失败。为了进行评估，我在 Tradestation 中进行了一次前瞻性测试。这个模块会不断地重新优化参数，这样我们每次使用的时候都是用的样本外的结果。如果使用前瞻性测试表现良好，我们就能对策略有更大的信心。结果如下：

![图 6](https://cssanalytics.files.wordpress.com/2015/04/pic-6.png)

根据这些评估标准，DV 混沌/稳定性指标表现出色。除了通过前瞻性测试，指标的逻辑也是合理的，这是经常被忽视但重要的定性评估。在我们的量化研究方法中，我们总是应用前瞻性分析和定性评估。下面是前瞻性结果中显示的每个样本外时期的假设股票曲线。

![图 7](https://cssanalytics.files.wordpress.com/2015/04/pic7.png)

Tradestation 前瞻性分析器性能图表。这些结果是假设的结果，并不是未来结果的指标，也不代表任何投资者实际获得的回报。

好的量化研究是不同但稳定的想法的组合，这些想法要么相互确认，要么为整体模型增加多样性。我同意雷·达里奥的观点，15 个非相关的回报流是投资的圣杯（

[`www.businessinsider.com/heres-the-most-genius-thing-ray-dalio-said-2011-9`](http://www.businessinsider.com/heres-the-most-genius-thing-ray-dalio-said-2011-9)。DV 的混沌稳定性模型可能是可行的非相关候选者。

披露

上述研究讨论仅出于讨论目的，并不构成投资建议，也不推荐任何特定的投资策略，包括所展示的任何模型。展示投资组合表现基于假设性及回测结果存在固有限制。与实际记录不同，假设性结果无法准确反映材料经济或市场因素对证券价格的影响，因此，结果可能由于这些因素的影响而被高估或低估。由于假设性结果不反映实际交易，且可能无法准确反映材料经济和市场因素的影响，因此无法知道这些因素对上述展示模型可能产生的影响。无论基于假设模型还是实际投资结果的过往表现，都不预示未来表现。
