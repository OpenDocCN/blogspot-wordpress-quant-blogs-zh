<!--yml

类别：未分类

日期：2024-05-18 15:05:34

-->

# 及时组合：更多对疯狂 RUT 的探索

> 来源：[`timelyportfolio.blogspot.com/2012/07/more-exploration-of-crazy-rut.html#0001-01-01`](http://timelyportfolio.blogspot.com/2012/07/more-exploration-of-crazy-rut.html#0001-01-01)

在使用 R 中的 lawstat 包时，我无意中开始尝试构建系统（标准免责声明：不是投资建议，会亏很多钱，所以请谨慎）基于 Jarque Bera 正态性检验（[Wikipedia 上的条目](http://en.wikipedia.org/wiki/Jarque%E2%80%93Bera_test)或研究论文[`scholar.google.com/scholar?cluster=18293285759900281575&hl=en&as_sdt=0,1`](http://scholar.google.com/scholar?cluster=18293285759900281575&hl=en&as_sdt=0,1 "http://scholar.google.com/scholar?cluster=18293285759900281575&hl=en&as_sdt=0,1")）。由于我只是随便玩玩，我有点故意地为在 Russell 2000 上运行的系统进行了曲线拟合。经过大量实验，我找到了一些非常有趣的东西，这导致我在多个其他指数上进行了测试。它似乎只在 Russell 2000 上表现得非常出色，主要是在过去的 5 年中，这当然让我回到了在[Crazy RUT](http://timelyportfolio.blogspot.com/2011/07/crazy-rut.html)中提出的问题，并在[Crazy RUT in Academic Context Why Trend is Not Your Friend](http://timelyportfolio.blogspot.com/2012/06/crazy-rut-in-academic-context.html)中再次探讨，“为什么大多数动量系统在过去十年中在 Russell 2000 上不起作用，而它们在几乎所有其他指数上都有效？”请告诉我如果你有一个好的解释，或者你想测试政权。这是结果。对于这些漂亮的东西我花了很少的时间，我很抱歉。

更奇怪的是，该系统应用于肯尼斯·弗伦奇的小型分类，结果不同。

这是该系统在标普 500 指数上的表现，但确实没有什么特别之处。

[GIST 上的 R 代码（原始格式以便复制/粘贴）：](https://gist.github.com/3056379)
