<!--yml

分类：未分类

日期：2024-05-18 13:55:46

-->

# 市场体制仪表板 | Quantivity

> 来源：[`quantivity.wordpress.com/2009/08/23/market-regime-dashboard/#0001-01-01`](https://quantivity.wordpress.com/2009/08/23/market-regime-dashboard/#0001-01-01)

在[上一篇文章](https://quantivity.wordpress.com/2009/08/16/naive-backtesting-is-bogus/)中，以及随后的优秀读者评论中，提出了有效量化交易需要动态适应环境。然而，最困难的系统性量化问题之一是*确定相关的“环境”，如何衡量它，以及如何可视化它*。

人们过于经常地专注于分析原始价格图表以获取背景信息([技术分析](http://en.wikipedia.org/wiki/Technical_analysis)特别有害)。这是不幸的，因为基本的时间序列分析可以揭示并可视化其他方式无法看到的丰富信息。

一系列四篇文章试图建立一个“视觉仪表板”用于*单一工具的市场体制*（以图片形式，因为一张图片胜过千言万语）。为了简单起见，每篇文章都关注于 2007 年至 2008 年的 SPY，并探讨时间域和频域。前两篇文章将重点讨论在时间域内识别体制结构：

+   原始结构：可视化分布和瞬间

+   相关性结构：可视化自相关测度

后两篇文章将重点讨论在频域内识别体制结构：

+   频域结构：通过[傅里叶分析](http://en.wikipedia.org/wiki/Fourier_analysis)可视化稳定的正弦频率

+   小波结构：可视化非稳定的[小波](http://en.wikipedia.org/wiki/Wavelet_analysis)

对于刚开始接触这些技术的读者，它们可以通过类比欣赏乐队来理解。首先，必须理解音符的进展和顺序，由每种乐器演奏的乐谱表达；这是时间域。其次，必须理解如何区分每种乐器或乐器组演奏的[旋律](http://en.wikipedia.org/wiki/Melodies)和[和声](http://en.wikipedia.org/wiki/Harmonies)；这是频域。两者都很重要，每个提供对同一现象的[正交](http://en.wikipedia.org/wiki/Orthogonality)（或[正交 normal](http://en.wikipedia.org/wiki/Orthonormal)）视角。

这个仪表板旨在提供基本的可视化，可以捕捉许多工具的体制，适用于交易和风险管理。
