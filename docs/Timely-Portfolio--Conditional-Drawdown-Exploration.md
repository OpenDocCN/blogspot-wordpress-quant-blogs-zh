<!--yml

类别：未分类

日期：2024-05-18 15:06:31

-->

# 及时投资组合：条件回撤探索

> 来源：[`timelyportfolio.blogspot.com/2012/05/conditional-drawdown-exploration.html#0001-01-01`](http://timelyportfolio.blogspot.com/2012/05/conditional-drawdown-exploration.html#0001-01-01)

阅读完 [Strub, Issam S., Trade Sizing Techniques for Drawdown and Tail Risk Control (May 21, 2012)](http://ssrn.com/abstract=2063848) 后，我觉得我应该尝试将其与其他两篇关于条件回撤的优秀 R 文章联系起来：

> [`systematicinvestor.wordpress.com/2011/11/01/minimizing-downside-risk/`](http://systematicinvestor.wordpress.com/2011/11/01/minimizing-downside-risk/)
> 
> [`www.rinfinance.com/agenda/2010/Carl+Peterson+Boudt_Tutorial.pdf`](http://www.rinfinance.com/agenda/2010/Carl+Peterson+Boudt_Tutorial.pdf)

像往常一样，所有这些都不构成投资建议。

在 Strub 的论文中，他使用条件回撤（CDaR）和条件 VaR（CVaR）来计算定向（突破确定）长/短货币头寸的头寸大小。结果足够有趣，值得尝试稍微改变以复制。对于这篇文章，我将使用 CDaR 来确定仅有长头寸的 [Mebane Faber 10 个月移动平均策略](http://www.amazon.com/s/ref=nb_sb_noss_1?url=search-alias%3Daps&field-keywords=mebane+faber) 上的头寸大小。我们将从有效前沿的比较开始，然后放弃前沿采用系统化方法。

*(蓝色文字代表对评论的回应中添加的解释)*

如果我们在下面观察回报与风险的每个度量之间的前沿图表——最常见的标准差、CDaR（条件回撤）和 CVaR（条件风险方差）——我们会发现前沿图表没有明显不同。从视觉上看，最不同并且是在不好的方向上的是图表左上角的红色 CVaR 线。红色 CVaR 线为每个标准差单位提供的回报低于其他两条前沿线，但当我们将 CDaR 或 CVaR 用作我们的风险度量的 x 轴时，这种表现不明显。

就像上面的前沿图表一样，过渡图表仅显示每个潜在风险单位的略有不同的有效配置。在风险轴的低端（图表左侧），我们可以看到配置之间的最大差异。

缺乏明显不同的结果似乎与均值-方差优化的众所周知的问题一致。这些问题在 [这篇 Morningstar 文章](http://corporate.morningstar.com/ib/html/pdf.htm?../documents/MethodologyDocuments/ResearchPapers/RobustAssetAllocation.pdf) 中描述得非常好。

> “众所周知，均值-方差优化对回报、标准差和协方差的估计非常敏感（参见 Michaud [1989] 和 Best 和 Grauer [1991]）。在这三个输入因素中，回报无疑是最重要的，不幸的是，也是最不稳定的。Chopra 和 Ziemba [1993] 估计，在适度风险容忍水平下，均值-方差优化对回报估计误差相对于风险（方差）估计误差的敏感性是 11 倍，对风险（方差）估计误差相对于协方差（也适用于相关性）的敏感性是两倍。Richard Michaud 将“Markowitz 优化谜题”这一表述用于描述输入敏感性和由此产生的高度集中的资产配置问题（参见 Michaud [1989]）。
> 
> 输入敏感性表明，模型的输出（资产分配）由于输入（资本市场假设）的小变化而显著变化。估计误差指的是在向前看的背景下，输入因素是预测，因此很可能不是完美的（即它们包含误差）。将这两个问题结合起来，使一个无信息的从业者可能造成比好处更大的损害。”

为了再次审视显著差异的缺失，让我们看看每个有效前沿的 25th 分配的累积回报。

尽管整个期间的前沿并没有显著不同，我们仍然可以以一种不同的方式使用这些更复杂的风险度量来确定头寸大小。作为一个简单的例子，与[Strub](http://ssrn.com/abstract=2063848)中提供的示例类似，假设我们想要在每个这 3 种货币中追求一个 Mebane Faber 风格的 10 个月移动平均值的长仓策略。我们还希望将每个头寸的 CDaR 限制在 5%，所以如果我们完全分配，这 3 个 CDaR 的总和将是 15%。我们将尝试通过使用 12 个月的滚动 CDaR 作为下一个月预期的 CDaR 来实现这一点。以下是 12 个月滚动 CDaR 的图表。

如果我们只是将每个超过其 10 个月移动平均值的货币组合的 100%分配，结果看起来就像这样。我们的组合最大杠杆将是 300%。

然而，如果我们想在平静时期分配超过 100%，并在动荡时期限制我们的 CDaR，我们可以通过 12 个月滚动 CDaR 来调整我们的分配。作为一个例子，如果过去 12 个月新西兰元的 CDaR 是 15%，而我们希望 5%的 CDaR，我们可以分配给新西兰元 33%或 15%历史/5%目标。当 CDaR 很小时，这可能导致近乎无限大的头寸规模，因此我们也可以说，我们希望对单一货币的最大分配在组合层面上是 200%或 600%。累积回报图表看起来就像这样。

我认为这不太可能是一个最终的分配机制，我当然也不会觉得舒适，但我希望它提供了一些有指导意义的构建模块，你可以在此基础上建立一个分配系统。

[R 代码来自 GIST:](https://gist.github.com/2844444)
