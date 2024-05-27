<!--yml

类别：未分类

日期：2024 年 05 月 18 日 06:48:21

-->

# HOXO-M - 日本的匿名数据分析团队 - ：Shiny 上的 SABR 校准

> 来源：[`mockquant.blogspot.com/2013/09/sabr-calibration-on-shiny.html#0001-01-01`](http://mockquant.blogspot.com/2013/09/sabr-calibration-on-shiny.html#0001-01-01)

正如你所知(如果你经常使用 R！！！)

[Shiny](http://www.rstudio.com/shiny/)

），它允许我们轻松地在 R 中创建网络应用程序。它不需要 HTML，CSS，javascript 的知识，我的意思是，我们不需要直接编写 HTML，CSS 和 javascript 来创建网络应用程序。

你的网络应用的用户可以通过网络应用程序与输入参数进行互动。这将为你提供一个很好的机会来理解这个模型的工作原理以及它的局限性。

[Systematic Investor 的例子](http://systematicinvestor.wordpress.com/shiny/)

在金融分析中非常好用，当我第一次看到它的时候，我感到非常兴奋。我决定通过 shiny 创建自己的网络应用程序，作为一个"模拟"量化分析师。

我的应用程序在这里（你也可以在

[Github](https://github.com/teramonagi/SABRCalibrationOnShiny)

):

这是基于 Hagan 逼近公式的 SABR 模型校准(

[管理微笑风险，P. Hagan 等(pdf)](http://www.math.columbia.edu/~lrb/sabrAll.pdf)

). 在一些衍生市场中，SABR 模型是事实上的模型，你可以理解 SABR 模型在多大程度上适应市场数据（隐含波动率），以及它的局限性。
