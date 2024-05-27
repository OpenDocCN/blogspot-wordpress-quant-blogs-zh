<!--yml

category: 未分类

date: 2024-05-18 15:05:06

-->

# Timely Portfolio: 地平线图的应用

> 来源：[`timelyportfolio.blogspot.com/2012/07/application-of-horizon-plots.html#0001-01-01`](http://timelyportfolio.blogspot.com/2012/07/application-of-horizon-plots.html#0001-01-01)

*有关背景，请参见先前的帖子* [*地平线图已经可用*](http://timelyportfolio.blogspot.com/2012/06/horizon-plot-already-available.html) *和* [*R 中的 Cubism 地平线图*](http://timelyportfolio.blogspot.com/2012/06/cubism-horizon-charts-in-r.html)

良好的可视化简化了一切，而且有效且漂亮的可视化能更好地讲述故事。

尽管地平线图不是立即直观的，但我接受它们作为分析多于四个序列的极其有效的方法。我希望它们变得更加流行，这样我就可以更有信心地使用它们。如果我们查看 PerformanceAnalytics 提供的管理数据集的传统累计增长图，我会因为 10 个不同的序列而感到困惑，线条和颜色太多。尽管这种图表有效，但它可以做得更好。

我们可以将数据面板化，但我认为这会使比较更加困难。

在这种情况下和其他许多情况下，地平线图提供了一种既吸引人又有效的可视化方式。以下是一个使用 latticeExtra 的 horizonplot 函数且几乎没有调整的示例。您可以检测到同时存在的协同运动或季节性，并可以比较振幅。

通过一些额外的格式化，我们可以得到理想的视觉化效果——既漂亮又有效。超过 10 个序列的良好缩放能力提供了传统折线图无法获得的强大功能。

再举一个例子，让我们看看如何使用地平线图来监控类似于[Mebane Faber 的定时模型](http://www.mebanefaber.com/timing-model/ "http://www.mebanefaber.com/timing-model/")的移动平均系统。如果您点击链接，可以看到价格和移动平均值的良好可视化。地平线图可以更有效地完成这个任务。

我个人更喜欢镜像地平线图。让我们加入这个元素。

请帮助我普及这些极其强大的图表。

[R 代码来自 GIST（复制/粘贴请选择原始格式）：](https://gist.github.com/3218639)
