<!--yml

分类：未分类

日期：2024-05-18 04:47:36

-->

# 智能交易：基于神经网络的时间序列（股票）预测的实用实现 - 第四部分

> 来源：[`intelligenttradingtech.blogspot.com/2010/02/practical-implementation-of-neural_04.html#0001-01-01`](http://intelligenttradingtech.blogspot.com/2010/02/practical-implementation-of-neural_04.html#0001-01-01)

考虑这是我们需要预处理数据的一个介绍。

我之前提到过，金融时间序列通常是一个单位根或非平稳信号，这意味着如果你随着时间的推移采样统计属性，它们显然会发生变化。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhotfy3qAUStcIYh4vFvQg6syIektEMfGPOoK1OzNjs2ZLGhzrCDnistWSjsxWyMyFJFqGnM5b-sSU0xZBxtmUlxgf7njfFnxYC7CEM4PmUVMZ1NmCuCmD1JElLTtIcXsoUcyWZ47hzE9k/s1600-h/fig1sp500.jpg)

图 1. 非平稳的 S&P 500 信号

你可以看到，当我们在不同点取平均值时，它总是在变化。单位根时间序列的另一个特性是它持续增长（或爆炸）。我们需要以某种方式将时间序列转换回一个平稳信号，这样神经网络才能处理并学习它。不仅神经网络需要看到类似甚至重复的数据一次又一次，而且任何超过内部压缩函数的值都会在处理元素的轨道上饱和。

许多长期金融时间序列的一个特点是它们呈指数增长，所以一个好的候选拟合可能是指数方程。然而，由于我们将使用分解去趋势，我更喜欢使用线性拟合。为了实现这一点，我们可以取数据的对数，稍后进行后处理反转操作。对指数数据取对数还将将指数回归转换为线性回归，我们可以使用线性回归并在时间序列上减去以获得一些平稳性。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgwWOBJZZoOLpLy1LUKrevueQlTMup3bdsl_cZl4iyk_Z6qJDMZeHhpQHRShPLDNhISuCsSwK8Dw5z0r_A4rvrDwzI5m57VJvZJYLodBG5eTzh4ppl_htsSmNw9_X9XUF_Z9_m3U9BzMSc/s1600-h/fig3logtransform.jpg)

图 2. 对数变换的时间序列

此外，注意我们将要预测下一天，所以我们可以简单地使用每日更新的线性回归参数来预测下一天。

如果我们有足够的数据，我们应该看到参数趋向于一个稳定的极限，正如硬币抛掷收敛于一个渐进极限。如果参数稳定，我们有信心它们从一个样本预测到下一个不会发生很大变化。

![图 9](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgBM0jjMH9iHy8wLvcTugVzQMFP0zqwuGfXM6HxYK4a-T3VrKtZzX7-hjvfQxe5xD3V7BD3sC7Ha3QXptV555KpcfUT5-Ql5x1kDyLDyDhIZELHWbvLVCUx_yBRZAlthSrf0PtY_ho

图 3. 线性预测参数的动态斜率沉降

注意参数在训练期间已经稳定到一个相当稳定的值，这暗示我们不期望它们在下一个预测估计的真实值上下太大波动。

在从对数变换的信号中减去线性回归后，我们得到了去趋势且稳定的信号。

![图 5](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjOF2kR9yojWT8dQl9RK-fwUXanf1Cj2P7Vs2nm20chX6gyJGJ8esGola319C-tf6b0PpvWoPiKiFSxQucYXBfTeHnek8UWpOXf8Cx9EUJOoFVcxM5LTjjRrblCYtYj1e9eqnzyVJF1uiY/s1600-h/fig4detrenedseries.jpg)

图 8. 去趋势的对数变换信号

注意，它比原始时间序列要稳定得多。然而，由于神经网络没有在时间窗口内看到很多重复的高频信息，我将再次进行去趋势处理，使用更快平滑的代表。首先我们将使用 100 期移动平均作为新的中间趋势，然后减去 25 期移动平均得到第二去趋势系列。

![图 1](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhn0LZl-pj8xZ7TV8WmmOAZbwxjYgYovYdWglrhJU-dtZPqPvypDpwF7lXrFEdws2-kaV_JJSTjfJMRVyDqbnDzdZb_dLZI0A0jxg5zoXl4Tq496MUWRIse7CY5RLG2s-LW7rplijU5gV8/s1600-h/fig5_2nddetrendedseries.jpg)

图 7. 第二去趋势系列。

注意即使这个小型样本也显示出神经网络学习时间序列中微小模式信号更好，这种稳定性属性非常温和。

![图 4](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEijEoaJ1Zp3YrzUEmOfJk_1EV61ypK1ejaP9Y-lX6ByCOcSMBXKluXyy1xO8bxaUpMAHx9zYm4LITCxm6hC7OeSOBXn9Me-kLLs-N1ZgdVDWtvnmxsCS9D8zHGN9nH6JL4VVC-j81Gr_X4/s1600-h/fig6stockpred.jpg)

图 6. 重建的预测样本外

上述图表展示了一个股票序列的例子，该序列通过使用 100 和 25 期移动平均以及样本外期间进行分解、平滑和重新组合。预测的平滑估计值与实际值之间存在非常好的相关性。这种系统可能会用于移动平均交叉预测，以在估计动量方面获得 1 天的优势。然而，预测值与实际值之间存在一些非常小的差异，我相信这是由于我在 Weka 上遇到的一个小问题。Weka 的输出只具有 3 位数字的精度。在 nabble 论坛上他们提到了一个在 Subversion 中的新选项，但我还没有机会去尝试它。
