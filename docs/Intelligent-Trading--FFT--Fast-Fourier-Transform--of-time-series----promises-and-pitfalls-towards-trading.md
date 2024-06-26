<!--yml

类别：未分类

日期：2024-05-18 04:46:20

-->

# 智能交易：时间序列的 FFT（快速傅里叶变换）——交易中的承诺与陷阱

> 来源：[`intelligenttradingtech.blogspot.com/2010/02/fft-of-time-series-promises-and.html#0001-01-01`](http://intelligenttradingtech.blogspot.com/2010/02/fft-of-time-series-promises-and.html#0001-01-01)

![图像](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhY8YiJBD0gv93-SrmWQArf0mc8mt4zDjSrLwI_pgXi1PL-fqld5Ra0DgSYwEJ36SM7S0v-XVHu25VdUy0EaOADB8oVgSIB71mOJOM2jxTSuFvME53YN_U3yU6pygua36bWiiS8nS-c3Zc/s1600-h/fft_ex.jpg)

图 1。分别使用前三个和 20 个谐波重构的 FFT 变换时间序列（EBAY）。

我看到很多交易员对高级信号处理技术感兴趣。了解它们可能是否有用通常是很有教益的。傅里叶分析的概念是，任何周期信号都可以分解为泰勒级数或适当缩放的正弦和余弦波形（甚至是方波！）的总和。关键要求是信号是周期性的，这意味着它们正向和反向重复到正无穷和负无穷。任何处理金融序列的人都知道它们是非周期的（意味着它们不会无限期地重复）。FFT，或快速傅里叶变换，是一种算法，它基本上使用卷积技术有效地找到构成感兴趣信号的谐波的幅度和位置。我们经常可以通过添加和删除连续的谐波（这类似于选择性地过滤构成信号的特定谐波）来操纵 FFT 频谱，以获得底层信号的平滑版本。

在发布的示例中，我展示了使用前三个谐波（并切断所有其他谐波）重构变换波形的效果，其中我们看到了信号的低通版本。第二个示例包括了前 20 个谐波，这开始更接近信号，但是对信号的平滑表示，这通常是一种很好的方法来隔离平滑信号分量和高频噪声。注意，在本讨论中，术语谐波和泛音实际上是同义的（泛音更具体地是基频的整数倍）；两者都代表了组成总波形的频谱频率分量。我想通过这个简单的示例说明的主要问题之一是'缠绕效应'的问题。正如我之前提到的，正确应用傅里叶变换的一个要求是信号是周期性的或重复的，因为卷积的基函数（正弦和余弦）是无限重复的函数。

有了这个要求，重构的波形试图尽可能匹配周期性重复的开始和端点。结果是在端点（左和右）处出现了严重问题，这些地方通常是我们最关心的。所以在听到高级信号处理技术应用的时候，通常要谨慎。应用 FFT 技术有几个其他要求和限制，其中包括：需要 2^n 个样本，fsample 必须大于或等于采样信号最大带宽的两倍（奈奎斯特准则），有限的频谱音调箱分辨率；忽略这些问题中的任何一个都可能导致严重的重构错误。
