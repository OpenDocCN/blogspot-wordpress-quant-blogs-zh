<!--yml

分类：未分类

日期：2024-05-18 15:08:17

-->

# 及时投资组合：系统投资者精细工作的简化示例

> 来源：[`timelyportfolio.blogspot.com/2012/02/simplified-example-of-systematic.html#0001-01-01`](http://timelyportfolio.blogspot.com/2012/02/simplified-example-of-systematic.html#0001-01-01)

这只是一个示例，并不是投资建议。根据此操作将会损失大量金钱。

[系统投资者博客](http://systematicinvestor.wordpress.com/)（一定要查看网站）提供了使用 R 语言进行金融方面非常好的示例。由于我坚信更多的示例总是更好的，我想提供一个非常简单的示例，说明如何使用他的[系统投资者工具箱（SIT）](https://github.com/systematicinvestor/SIT)进行系统开发。这将为我们提供一系列类似于我的[构建量化策略（Part 6）](http://timelyportfolio.blogspot.com/2011/07/quantstrat-to-build-on-part-6.html)博文的构建块。我们将使用我们熟悉的上升/下降（CUD）指标对标普 500 指数进行比较，并与[Mebane Faber](http://www.mebanefaber.com)的 10 个月移动平均进行比较。

我知道这看起来不怎么样，但我希望从尽可能简单的基数开始。任何忠诚的读者都已经知道 CUD 在赚钱方面并不是那么出色。

[R 代码在 GIST 中](https://gist.github.com/1793607)

：
