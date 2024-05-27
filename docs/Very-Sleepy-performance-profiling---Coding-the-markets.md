<!--yml

分类：未分类

date: 2024-05-12 19:30:58

-->

# [Very Sleepy 性能分析](https://etrading.wordpress.com/2015/10/05/very-sleepy-performance-profiling/#0001-01-01) | 交易编程

> 来源：[`etrading.wordpress.com/2015/10/05/very-sleepy-performance-profiling/#0001-01-01`](https://etrading.wordpress.com/2015/10/05/very-sleepy-performance-profiling/#0001-01-01)

## Very Sleepy 性能分析

### 2024 年 5 月 12 日 19:30:58

最近我一直在使用非常出色的[Very Sleepy 分析器](https://github.com/VerySleepy/verysleepy)来优化 SpreadServeEngine 的加载器、编译器和解释器性能。我们的一位测试用户非常热心地提供了一个非常大的电子表格，这导致了非常长的加载和计算周期。在 90 年代，你必须为[Pure Software](https://en.wikipedia.org/wiki/Pure_Software)的 Purify 和 Quantify 工具购买认真的许可证才能做这种工作。现在像[Dr Memory](http://www.drmemory.org/)和 Very Sleepy 这样的工具是免费的，并且是开源的。自从我上次做真正的、系统的性能分析调优练习以来已经有一段时间了，我很快就回忆起了关于哪些代码部分可能是 CPU 密集型的先入之见是如何迅速被打破的。不久之后，我就面临了 C++开发中的一个永恒真理，或者说是任何语言开发中的真理：malloc 和 free 是昂贵的。这就是[LMAX 团队编写自己的 Java 集合](http://www.infoq.com/presentations/LMAX)的原因。printf 也不是便宜的。答案是在许多最常使用的编译器和解释器类中引入内存池，并为解释器跟踪设置配置开关。解释器跟踪需要在发布构建中可用，因为它是一种深入了解电子表格执行情况的好方法。结果是加载时间提高了 30 倍，在非常大的表格上的计算周期也更快。
