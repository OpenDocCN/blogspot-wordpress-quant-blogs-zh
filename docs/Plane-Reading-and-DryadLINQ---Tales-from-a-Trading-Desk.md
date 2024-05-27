<!--yml

类别：未分类

日期：2024-05-18 06:14:30

-->

# 飞机阅读和 DryadLINQ | 交易桌上的故事

> 来源：[`mdavey.wordpress.com/2010/08/27/plane-reading-and-dryadlinq/#0001-01-01`](https://mdavey.wordpress.com/2010/08/27/plane-reading-and-dryadlinq/#0001-01-01)

有一次我没有飞往纽约。但像往常一样，在漫长的飞行中总得读点什么。

+   [jQuery](http://weblogs.asp.net/jalpeshpvadgama/archive/2010/08/27/jquery-javascript-library-write-less-do-more.aspx)——JavaScript 库，写得更少，做得更多

+   HTML5 [Reset](http://html5reset.org/)

+   HTML5 [Boilerplate](http://html5boilerplate.com/)

+   Azure Throughput [分析器](http://research.microsoft.com/en-us/downloads/5c8189b9-53aa-4d6a-a086-013d927e15a7/default.aspx)

+   [Orleans](http://www.zdnet.com/blog/microsoft/orleans-microsofts-next-generation-programming-model-for-the-cloud/7152)：微软针对云计算的下一代编程模型

+   [Rx](http://blogs.msdn.com/b/jeffva/archive/2010/08/20/rx-on-the-server-part-3-of-n-writing-an-observable-to-a-stream.aspx) 在服务器上，第 n 部分 3：将可观察对象写入流

所以让我们回到 DryadLINQ。Dryad 已经在我雷达上很长时间了——我也稍微写过一些关于它的博客。我与 Dryad 和 Windows HPC 2008 R2 之间的一个问题是你需要大量的硬件才能进行开发 😦 我相信如果我能得到更多的硬件，我会做到比我现在已经实现的更多。到目前为止，我发现 HPC API 是“痛苦的”。

所以让我回到 Dryad 和实时市场风险（一个我似乎花了不少时间从解决方案到 iPad UX 的话题）。在 DryadLINQ 中，我可以使用

> 分区表 trades = PartitionedTable.Get(inputUri);

这导致了使用类似的东西来计算市场风险：

> 结果 var result = trades.Select(t => Risk(t, curves);

假设我有一个函数：

> TResult Risk(Trade t, Curve[] curves);

然而上面的方法是有缺陷的，因为我不想把所有的曲线都发送给每一个交易，因为这样会占用过多的网络带宽:-)

**侧边栏：** DryadLINQ 编程指南的示例主要来源于平面文件中的数据集，这也不是我通常作为交易存储库所拥有的特权。考虑到为 Dryad 开发所需安装的硬件/软件量，微软是否会提出一个模拟模式来加速开发并降低成本呢？

无论如何，让我们回到一个更好的解决方案，可能来自于直方图示例，特别是 BuildHistogram 函数。

> 返回 inputTable
> 
> .SelectMany(x => x.line.Split(' '))
> 
> .GroupBy(x => x)
> 
> .Select(x => new Pair(x.Key, x.Count()))
> 
> .OrderByDescending(x => x.Count)
> 
> .Take(k);

特别是如果交易集是一个完整的簿记/投资组合，那么也许我们想要进行一个 SelectMany，按产品将交易分割出来，然后也许按货币进行 GroupBy。我们然后可以将适当的收益率曲线发送到正确的交易。

还需要更多的思考。

~ mdavey 于 2010 年 8 月 27 日发表。

发布于[高性能计算](https://mdavey.wordpress.com/category/hpc/)

标签：[微软](https://mdavey.wordpress.com/tag/microsoft/)
