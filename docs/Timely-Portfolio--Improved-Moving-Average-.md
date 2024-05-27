<!--yml

类别：未分类

日期：2024-05-18 15:10:13

-->

# Timely Portfolio: Improved Moving Average?

> 来源：[`timelyportfolio.blogspot.com/2011/12/improved-moving-average.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/12/improved-moving-average.html#0001-01-01)

*我被告知该代码并不能完美反映所介绍的改进移动平均。在另一篇文章中，我将探讨差异。作者现已发布了他们版本的代码[`www.quantf.com/fotis-papailias/improved-moving-average-code-is-available-for-download/332`](http://www.quantf.com/fotis-papailias/improved-moving-average-code-is-available-for-download/332 "http://www.quantf.com/fotis-papailias/improved-moving-average-code-is-available-for-download/332").*

当[@quantfblog](http://twitter.com/#!/quantfblog)在 Twitter 上关注我时，我很高兴地发现他们的论文。

> [Papailias, Fotis and Thomakos, Dimitrios D., An Improved Moving Average Technical Trading Rule (September 11, 2011). Available at SSRN: http://ssrn.com/abstract=1926376](http://ssrn.com/abstract=1926376)
> 
> [Papailias, Fotis and Thomakos, Dimitrios D., An Improved Moving Average Technical Trading Rule II - Can We Obtain Performance Improvements with Short Sales? (November 12, 2011). Available at SSRN: http://ssrn.com/abstract=1958906](http://ssrn.com/abstract=1958906)

由一个越来越好看的网站[`www.quantf.com`](http://www.quantf.com)支持。我只是忍不住把他们的改进移动平均想法带到 R 中并运行一些额外的测试。整个过程非常愉快，因为作者愿意在实施过程中进行测试、发表评论和建议。非常感谢他们给予的所有帮助。

在这个过程中，我并不提供投资建议。这只是一个测试/说明。追求这些概念很可能会损失（全部）你的钱。

为了好玩，我想到比较一下“改进的移动平均”与[Mebane Faber](http://mebanefaber.com)风格的 10 个月移动平均系统。

虽然我喜欢测试，但我还是不太确定“改进的移动平均”是否真的有所改进，但它确实可能比标准移动平均更适合某人的效用曲线。最重要的是，这个过程向我证明了几件事：

> 1) 开源和合作的美丽。作者在我完成这个过程时非常慷慨和 helpful。为了更好地展示开源的力量，我将使用 ttrTests 进行额外的测试，并在未来的帖子中使用来自[`systematicinvestor.wordpress.com`](http://systematicinvestor.wordpress.com)的 bt 示例。
> 
> 2) 即使是简单的移动平均也可以变得非常复杂。做出一个非常小的改动会显著改变结果。

[R 代码来自 GIST:](https://gist.github.com/1405561)
