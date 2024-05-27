<!--yml

类别：未分类

日期：2024-05-12 17:49:45

-->

# 距离加权移动平均（DWMA 和 IDWMA）| CSSA

> 来源：[`cssanalytics.wordpress.com/2014/12/18/distance-weighted-moving-averages-dwma-and-idwma/#0001-01-01`](https://cssanalytics.wordpress.com/2014/12/18/distance-weighted-moving-averages-dwma-and-idwma/#0001-01-01)

[距离加权移动平均](http://www.encyclopediaofmath.org/index.php/Distance-weighted_mean)是另一种[非线性滤波器](https://cssanalytics.wordpress.com/2014/12/03/combining-acceleration-and-volatility-into-a-non-linear-filter-nlv/ "Combining Acceleration and Volatility into a Non-Linear Filter (NLV)")，为进一步的研究和探索提供了基础。在其传统形式中，距离加权移动平均（DWMA）旨在成为移动平均的强健版本，以减少异常值的影响。以下是来自数学百科全书的计算：  

![dwma](https://cssanalytics.files.wordpress.com/2014/12/dwma.png)

请注意上面的示例中，“12”明显是相对于其他数据点的异常值，因此在最终平均值中被分配的权重较小。这种方法相对于简单的温索拉法（从计算中识别的异常值被省略）的优势在于，使用了所有的数据，而不需要指定任意的阈值。这对于多维数据尤其有价值。通过在 DWMA 的计算中对距离值取平方而不仅仅是取绝对值，可以使平均值对异常值的不敏感性更强。请注意，这个概念也可以被反转以强调异常值或更大的数据点。这可以通过消除将距离作为分数倒数的需要，而仅仅使用距离权重来实现。这可以称为“反向距离移动平均”或 IDWMA，对于希望忽略时间序列中的小波动（可以被视为“[白噪声](https://cssanalytics.wordpress.com/2013/04/23/filtering-white-noise/ "Filtering White Noise")”）并使平均值更加响应突破的情况非常有用。此外，这种方法在风险敏感性重要的波动率计算中可能更有价值。下面的图表显示了这些不同的移动平均如何响应具有异常值的虚构时间序列：

![dwma2](https://cssanalytics.files.wordpress.com/2014/12/dwma2.png)

注意 DWMA 对价格波动和大幅跳跃的敏感性最低，而 IDWMA 最敏感。比较而言，SMA 的响应介于 DWMA 和 IDWMA 之间。关键在于，移动平均线并非固有上优于另一种，而是每一种都适用于不同的应用，并且在不同的时间序列上可能表现更好或更糟。有了这个说法，让我们来看一些实际例子。我通常更喜欢使用收益而不是价格，所以在这种情况下，我们将以两种不同的时间序列——标准普尔 500 和黄金——来应用不同的移动平均变体：DWMA、IDWMA 和 SMA。交易者和投资者都很容易认识到标准普尔 500 在短期内非常嘈杂。相反，用长期测量方式来预测黄金往往是不可预测的，但大幅度波动在短期内往往是可预测的。这是是使用不同变体的 10 天移动平均线从 1995 年至今的表现。规则是，如果平均值高于零则持有，如果低于零则持有现金（在本例中假设现金无利息）：

![dwma3](https://cssanalytics.files.wordpress.com/2014/12/dwma3.png)

![dwma4](https://cssanalytics.files.wordpress.com/2014/12/dwma4.png)

与传统观察一致，DWMA 在过滤掉大嘈杂或回归平均的价格波动时，对标准普尔 500 的表现最佳。相反，IDWMA 的表现最差，因为它通过强调这些波动来扭曲平均值。但在黄金这种情况下，IDWMA 受益于强调这些大（看似有用的趋势信号），而 DWMA 的表现最差。在两种情况下，SMA 的表现居中。距离加权移动平均线的一个缺点是，计算忽略了每个数据点的时间位置。如果有一个离群值，那么它发生在 60 天前就不那么重要了，而发生在今天则重要得多。通过巧妙地操纵计算，可以解决这个问题。然而，主要的启示是可以为不同的时间序列使用不同的加权方案来进行移动平均，并且产生潜在的更好结果。也许一个自适应的方法会产生好的结果。此外，对不同类型的应用，应该对适当的移动平均计算进行深思熟虑。例如，您可能希望使用 DWMA 而不是中值来计算相关性——这可能被离群值严重扭曲。也许在绩效或交易统计中使用 DWMA 也是有意义的。正如前面提到的那样，在许多情况下，使用 IDWMA 在基于波动率的计算中是有帮助的。把这看作是一种非常简单的工具，加到你的量化工具箱里。
