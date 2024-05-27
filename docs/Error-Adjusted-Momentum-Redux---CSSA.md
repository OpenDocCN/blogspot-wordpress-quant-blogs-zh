<!--yml

类别：未分类

日期：2024-05-12 17:48:59

-->

# 误差调整动量再论 | CSSA

> 来源：[`cssanalytics.wordpress.com/2015/02/02/error-adjusted-momentum-redux/#0001-01-01`](https://cssanalytics.wordpress.com/2015/02/02/error-adjusted-momentum-redux/#0001-01-01)

Capital Spectator 的詹姆斯·皮切尔诺（James Picerno）最近在他的文章 “[基于动量的交易信号具有战略价值](http://www.capitalspectator.com/a-momentum-based-trading-signal-with-strategic-value/)” 中对 [误差调整动量](https://cssanalytics.wordpress.com/2014/07/30/error-adjusted-momentum/ "Error-Adjusted Momentum") 进行了良好的评估。Capital Spectator 博客内容丰富，涵盖了从经济学到资产配置和投资策略等各种主题。皮切尔诺出版了许多书籍，但我最喜欢的是 [Dynamic Asset Allocation](http://www.amazon.com/gp/product/1576603598?ie=UTF8&tag=thecapitalspe-20&linkCode=as2&camp=1789&creative=9325&creativeASIN=1576603598)，它在我的书架上有一个方便的位置。《动态资产配置》是对组合管理战略的实践案例的良好回顾。

为了在误差调整的动量策略上增添一些新的想法，我建议读者尝试使用多个时间窗口（即平均期）和误差回溯，以及来自日内、日常甚至每周不同频率的数据点，并将它们汇总以增加稳健性。风险或波动性可以替代或与误差调整一起使用。某种方式标准化收益的一般概念，以考虑变化的方差/误差，创造了一种有效的非线性滤波器，是[自适应移动平均线](http://www.investopedia.com/articles/trading/08/adaptive-moving-averages.asp)的优秀替代品。相比之下，典型的自适应移动平均线方法尝试根据某个指标变化来调整回溯窗口（使移动平均线速度更快或更慢）。有关移动平均线的学术研究表明，这种方法在金融市场之外的各种时间序列数据中几乎没有取得成功。

我个人尝试过几乎每一种我能找到的具有自适应移动平均框架的方法，但都没有取得实质性的成功。问题的一部分在于，转向较短期的移动平均会增加标准误差，因为你使用的数据较少。此外，通过忽略较旧的数据并转向较短的窗口，你假设时间序列的动态变化没有记忆。波动率预测方法的成功部分表明，时间序列变化的影响随时间衰减，而不是一次性全部消失。误差调整的动量方法是一种非线性滤波器，在我个人的经验中，这类方法通常在金融时间序列中效果更好。这种特定的滤波器允许足够的回顾窗口进行平均以获得良好的估计（从统计样本大小的角度来看），并保留随时间演变的动态信息。关键在于，它同时能够根据观察到的误差（或其他度量）强调/减弱数据集的各部分。在滤波器中用加权移动平均代替简单移动平均也可以更好地捕捉误差变化的路径依赖性。

与任何方法一样，应用相同概念的许多不同方式，读者被鼓励进行实验。警告是，最好使用集成中的多种方法，而不是选择最佳方法——我们通过实验尝试的事物越多（尤其是如果没有附加逻辑理论/假设），数据挖掘的风险就越大。我关注的一篇好博客中的一句最喜欢的引用来自 [Volatility Made Simple](http://volatilitymadesimple.com/)——它表达得最好：“被利用的概念比选择的具体参数更重要。所有参数集合将在长期内根据核心概念的成功或失败而共同上升或下降。”
