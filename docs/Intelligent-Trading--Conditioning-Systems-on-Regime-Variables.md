<!--yml

类别：未分类

日期：2024-05-18 04:45:04

-->

# 智能交易：基于体制变量的条件系统

> 来源：[`intelligenttradingtech.blogspot.com/2010/08/conditioning-systems-on-regime.html#0001-01-01`](http://intelligenttradingtech.blogspot.com/2010/08/conditioning-systems-on-regime.html#0001-01-01)

这是一个关于基于体制类型切换系统（有时称为门控）的简单例子。

在过去的帖子中，我已经多次提出了基于体制条件系统的想法。一些文本称这为过滤，尽管我更喜欢使用条件门控这个术语。简单想法是在某些条件下开启某个系统，在另一些条件下切换系统，或者简单地在不同条件下跟踪底层系列。在此情况下，门控条件是体制，进而是指由 VIX 测量的 High 或 Low 波动性。虽然我没有透露底层系统本身的细节，但在公共领域看到了足够的讨论，以至于我觉得其他交易员已经掌握了这里展示的想法。

图 1。终端财富与 VIX 阈值对比

下面的动画展示了在条件变量 VIX 的每一步系统结果。注意到在 23 值时有了显著的改进。同样，如早先帖子中提到的，最优切换点 23 是最稳健的值，因为即使 OOS 结果位于最优切换点的左侧或右侧，它们也将是在广泛依赖性范围内最好的局部值。细心的观察者可能已经注意到，这个系统只是在低 VIX 体制下跟踪买入持有，而在高体制下开启系统 V。显然，在 VIX 达到一定值后，终端财富只是跟踪买入持有，因为当低于某个阈值时，它总是锁定在跟踪模式。

系统仅在样本中显示，然而，我发现它在 OOS 中也非常成功。

<param name="movie" value="http://www.youtube.com/v/ZcSyV0mMcA0&hl=en&fs=1"><param name="allowFullScreen" value="true"><param name="allowscriptaccess" value="always"><embed src="http://www.youtube.com/v/ZcSyV0mMcA0&hl=en&fs=1" type="application/x-shockwave-flash" allowscriptaccess="always" allowfullscreen="true">

视频 1。通过线性 VIX 范围调整股权曲线系统。
