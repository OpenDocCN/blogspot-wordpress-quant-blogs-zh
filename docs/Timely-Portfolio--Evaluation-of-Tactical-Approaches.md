<!--yml

category: 未分类

date: 2024-05-18 15:06:23

-->

# 及时投资组合：战术方法评估

> 来源：[`timelyportfolio.blogspot.com/2012/06/evaluation-of-tactical-approaches.html#0001-01-01`](http://timelyportfolio.blogspot.com/2012/06/evaluation-of-tactical-approaches.html#0001-01-01)

战术方法通常是根据最佳累积回报来选择的，这暗含了重大的事后偏见。仅仅因为某种方法在一段时间内占据主导地位，并不意味着它就是最佳方法。随着投资界放弃买入持有法，转向战术配置，我猜想，最佳累积回报会吸引最多的资金。

[Mebane Faber](http://www.mebanefaber.com/)的 10 个月移动平均系统在

> **[战术资产配置的量化方法](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=962461)**
> 
> *财富管理杂志，2007 年春季*

并在他的书中进一步完善

提供了一个实现大多数人认为是良好结果的简单方法——尊重累积回报，但风险显著减少，无论风险度量如何。让我们玩一下自由度，并对系统进行轻微调整，看看它们在过去的表现如何。然后让我们试着决定未来应该追求哪种方法，考虑到信息非常不完整。一旦我们决定了，让我们再决定未来结果的可信度有多高。

我将测试四个在方法上非常相似的系统：

不是投资建议。请不要使用，结果将是巨大的和痛苦的损失。

1.  Mebane Faber 10 个月移动平均

1.  滚动专有（微笑着说，但不要使用表情符号）夏普比率 > 10 个月移动平均

1.  滚动专有夏普比率 > 0

1.  滚动专有夏普比率 > 6 个月前的滚动专有夏普比率

在[下载和解析 EDHEC 对冲基金指数](http://tradeblotter.wordpress.com/2012/06/04/download-and-parse-edhec-hedge-fund-indexes/)给出的良好示例的帮助下，我们可以可视化每种方法的累积回报和回撤。我在 1985 年标了一条线，这是我们可能选择方法 #2 的时间，因为它在 1950 年至 1985 年期间提供了明显更好的累积回报。然而，我们在 1985 年做出选择后的结果并不如我们预期的那样好。

再次使用[下载和解析 EDHEC 对冲基金指数](http://tradeblotter.wordpress.com/2012/06/04/download-and-parse-edhec-hedge-fund-indexes/)，我们可以使用一些更复杂的风险测量方法。中间（MovAvgSharpe 或方法 #2）在累积基础上提供了最低水平的历史风险。尽管自 1985 年首次获得第一名以来表现有所下降，这可能还是会鼓励我们选择这种方法。

为了继续我们从累积回报向其他统计数据的转变，我们可以检查月度变化的分布以及一些更高阶的统计数据偏斜度和峰度。

即使在我们进行了所有的探索之后，我们也无法预测任何事情。为了更加自信，我们可能会使用 ttrTests（在帖子[`timelyportfolio.blogspot.com/search/label/ttrTests`](http://timelyportfolio.blogspot.com/search/label/ttrTests "http://timelyportfolio.blogspot.com/search/label/ttrTests")中解释），使用随机投资组合，如[`portfolioprobe.com`](http://portfolioprobe.com)所提倡和很好地解释的那样，以及/或让相对强度来决定，如[`systematicrelativestrength.com/`](http://systematicrelativestrength.com/ "http://systematicrelativestrength.com/")所提倡和很好地解释的那样。然而，在 30 年的时间里，我们不知道什么会做得最好，甚至不知道最好意味着什么。

[R 代码在 GIST 中：](https://gist.github.com/2897532)
