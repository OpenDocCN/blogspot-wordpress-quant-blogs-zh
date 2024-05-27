<!--yml

类别：未分类

日期：2024-05-18 04:45:42

-->

# 智能交易：使用 R 进行小波频谱图非平稳金融时间序列分析（TTR/Quantmod/dPlR）与 USDEUR

> 来源：[`intelligenttradingtech.blogspot.com/2010/04/wavelet-spectograph-analysis-using-r.html#0001-01-01`](http://intelligenttradingtech.blogspot.com/2010/04/wavelet-spectograph-analysis-using-r.html#0001-01-01)

最近，我一直在进行关于适用于非平稳信号的光谱成像和分解技术的研究。如前所述，傅立叶分析的一个主要问题之一是基础函数在两个方向上都延伸到无穷远，信号被假定为平稳的。虽然我现在不会过多展开，但小波的一个优点是它们使用局部小窗口基函数，使它们能够捕获不仅是非平稳信号，而且是非周期信号：在处理金融时间序列时，这是傅立叶方法的两个重大优势。

我组织了一些小例子来理解如何直观地理解频谱图。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEipNyBRAcp-JhdlexzpGbmJ_Fa6gY_jlm9OZ5SnWX5u3X1dk4fvWwNvAkWZRC5C1WlPGPWWHficyj4IeYQUNxuZPB42cq8R89J1_tE33XeQ2KH-jgy3sq8L4mQ7AboiFBrLy9MC3DyxCO0/s1600/58_cycle1.jpg)

图 1\. 用 11 个八度和 2048（2¹¹）个数据点捕获的简单 58 天周期

正如早期的基于教程的文章所述，我们使用一个简单的 58 天周期来展示基本的时间序列正弦波形。现在底部的图表被称为频谱图。这个频谱图的波小波变换类型被称为连续小波 Morlet 变换。该软件包是 dpLR（树轮年代学程序库），由

[安迪·邦恩](http://myweb.facstaff.wwu.edu/bunna/dplR.htm)

. 该软件包旨在分析树木年轮。请注意，有许多工具利用这种技术，从核磁共振成像到气象学，再到语音处理。在我看来，这是现代版的 DFT 类型的频谱工具（但是，用于非平稳和非周期信号）。现在看频谱图，请记住单位是天，而不是年（我需要看看如何修改，希望邦恩博士在听着=)。

时间尺度表示线性时间，或一个 2048 天窗口的采样。我们可以使用任何时间序列，但需要长度=2^N；如果不是，有一个函数用零填充数据的其余部分，以达到该长度。垂直刻度是对数刻度，显示所谓的“八度”。借用音乐术语，我们可以认为它们是音阶，每个前一个音阶的幅度翻倍，并在这些音阶上表示局部频率能量信息。颜色表示信号在感兴趣区域的热或功率。由于这种变换有一些问题，我们忽略了超出暗抛物线区域（影响锥）的不确定信息。很清楚，最高的能量是右边的暗红色区域，大约在 58 天。这里重要的是，不仅要理解周期的确切值，而是主导周期（s）的持续性。我们注意到，周期在整个频谱时间序列长度内持续存在（正如我们从 2D 时间序列图中预期的那样）。

如果我们使用随时间变化的不同频率会发生什么？在这里，我们明显地发现，与傅里叶方法相比，有一个明显的优势。傅里叶分解能够定位主导音，但是，因为它使用无限基，重建的信号不会捕捉不同频率的隔离。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgvMiwdbYt3gnLtyHZwUyjluqf5b7QqxRceiv4obC_3F0h8DAq4A6FGFZL9STs3qQ-C7NQdzdWuCUEbGmXcF8YXiG-j9GLB7sI3S2F_6polCfbOqoGeJT7-SkfPLz3mdhKsHQLiMnIr7ak/s1600/composite_cycles1.jpg)

图 2。由 3 个主导音组成的复合平稳时间序列

注意，通过遵循图表并寻找最集中的能量（红色）区域，我们可以清晰地看到主导音的区域，这些区域大约在 48、253 和 532 天的周期附近。我们还注意到，能量密度可以从时间上下文中观察，我们的眼睛只需沿着时间跟随并观察信号能量集中的强区域。

好吧，但如果信号本身是非平稳的呢？

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEif0Q9IJO7tqpzLe5v8a_jYu-ppqPjQrlq4SIJAXsfWd3CxU4z-nLZDc5o37dx1o1wLvmSp8_DaQQp0-KoGyRBKel0MSoQ5bk0QMVWBOGxmC4hfpTEhsQbDuNFj4bv1kygey6QdDNdbW0E/s1600/composite_exp3.jpg)

图 3。复合信号添加到指数曲线中，使信号非平稳

注意，尽管我们现在有一个非平稳的信号，但通过眼睛仍然可以检测到潜在的周期成分稳定性区域！

最后，通过 TTR/Quantmod 包捕获了 USDEUR 的金融时间序列。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEh1tCqfF-UXhL7i13dFM0ceVkVzSAl1Jxr6cGNLFeDkGQUAxgxzbgqI7Tghh8gGqOlXsNYciDCYL6yk8jRMNpBwYx1dES7nmzz8I-K2HVNLKWpC0GaIDXLp_CPl5-RDXGzozGuc7tOakts/s1600/usdeur1.jpg)

图 4.  USDEUR 时间序列光谱图

请注意，即使是在非平稳的金融信号中，也存在一个非常清晰的、主导的周期模式，它大致持续 255 天（任何熟悉交易的人都知道那大约是一年中的交易日数）。

请记住，在采样方法中也可能存在混叠（和扩散），这些可能看起来像周期信号，但实际上仅仅是 underlying sampled signal 的数字杂波。我们还可以在最低的刻度下看到非常短期的噪声。

这个方法的另一个有趣应用是，它不仅可以用作现代工具来增强非平稳分解，对于熟悉基于模式的技巧的人来说，它（以及周期图的对立面）经常用于模式识别和马尔可夫类型的建模。

这就全部结束了。希望您对基于小波的谱技术和对傅里叶谱分析有所了解。

我一直在考虑是否要把文章分开，但因为我在 R bloggers 论坛上发了文章，所以我想让本地读者看到完整的文章。

这就结束了。
