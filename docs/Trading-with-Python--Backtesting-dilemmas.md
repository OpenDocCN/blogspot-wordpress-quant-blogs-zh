<!--yml

分类：未分类

日期：2024-05-18 15:42:23

-->

# 用 Python 交易：回测困境

> 来源：[`tradingwithpython.blogspot.com/2014/05/backtesting-dilemmas.html#0001-01-01`](http://tradingwithpython.blogspot.com/2014/05/backtesting-dilemmas.html#0001-01-01)

量化交易者在成功交易策略的道路上面临着不少挑战。在这里，我将讨论在回测中涉及的一些困境。一个好的交易模拟必须：

1.  好的近似于现实世界。显然，这是最重要的要求。

1.  允许无限制的灵活性：工具不应该阻碍测试现成的想法。可以量化的任何东西都应该可用。

1.  易于实施和维护。这全是关于生产力和能够测试许多想法以找到一个有效的方法。

1.  允许进行参数扫描、前进测试和优化。这是为了调查策略性能和稳定性，这取决于策略参数。

满足上述所有要求的问题在于，第 2 和第 3 点是相互冲突的。没有工具能不付出高复杂度（=低可维护性）的成本就做到一切。通常，第三方点击工具会严重限制测试自定义信号和奇怪投资组合的自由，而在另一端，定制编码的解决方案可能需要数十小时甚至更多时间来实现，并且最终可能得出杂乱无章、难以理解的代码。因此，试图结合这两个世界的最佳特点，让我们从中间开始：使用现有的回测框架并将其调整到我们的口味。

在接下来的文章中，我将研究三种我找到的可能候选者：

+   **Zipline**（[`github.com/quantopian/zipline`](https://github.com/quantopian/zipline)）广为人知，是 Quantopian 的引擎

+   **PyAlgotrade** 似乎在积极开发且文档齐全

+   **pybacktest**（[`github.com/ematvey/pybacktest`](https://github.com/ematvey/pybacktest)）是一个轻量级的向量框架，可能因其简单性和性能而有趣。

我将研究这些工具的适用性，将它们与一个假设的交易策略进行基准测试。如果没有这些选项符合我的要求，我需要决定是否愿意投资编写自己的框架（至少通过查看可用的选项，我会知道什么是

*不是*

工作）或者坚持为每个策略使用定制代码。

第一个用于评估的是

**Zipline**

.

我对 Zipline 的第一印象和

**Quantopian**

是一个积极的评价。Zipline 由一个开发团队支持，并在生产中得到测试，所以质量（缺陷）应该非常好。在

**网站**：[`www.quantopian.com/help#api-doco`](https://www.quantopian.com/help#api-doco)

和一个示例

**GitHub 上的笔记本**：[`nbviewer.ipython.org/github/twiecki/financial-analysis-python-tutorial/blob/master/3.%20Backtesting%20using%20Zipline.ipynb`](http://nbviewer.ipython.org/github/twiecki/financial-analysis-python-tutorial/blob/master/3.%20Backtesting%20using%20Zipline.ipynb)

.

为了掌握它，我下载了示例笔记本并开始与之交互。令我失望的是，我在第一个示例中很快就遇到了麻烦。

**最简单的 Zipline 算法：买入苹果**

数据集只有 3028 天，但运行这个示例似乎永远也完不成。以下是我测量的结果：

```
dma = DualMovingAverage()
%timeit perf = dma.run(data)

1 loops, best of 3: 52.5 s per loop

```

我没有期待 Zipline 这个基于事件的回测工具会有出色的表现，但是 3000 个样本几乎要花一分钟的时间实在是太糟糕了。这种性能对于任何类型的扫描或优化来说都是不可接受的。当处理更大的数据集，比如日内数据或多种证券时，这个问题会更加严重，这些数据集很容易包含数十万个样本。

不幸的是，我不得不将 Zipline 从可用的回测工具列表中删除，因为它远远没有达到我的要求#4。

在接下来的文章中，我将看看 PyAlgotrade。

**注意：我当前的系统有几岁了，运行着 AMD Athlon II X2 @2800MHZ 和 3GB 的 RAM。在使用基于向量的回测时，我习惯于单个回测计算时间少于一秒，参数扫描一分钟或两分钟。基本的向前测试，10 步和 20x20 网格的参数扫描，使用 zipline 将耗时惊人的 66 小时。我没有那么有耐心。**
