<!--yml

类别：未分类

日期：2024-05-12 19:04:34

-->

# 量化交易：一种优化参数的方法

> 来源：[`epchan.blogspot.com/2010/01/method-for-optimizing-parameters.html#0001-01-01`](http://epchan.blogspot.com/2010/01/method-for-optimizing-parameters.html#0001-01-01)

大多数交易系统都有许多内嵌的参数，例如回望期、进入和退出阈值等。我的博客读者（例如

[这里](http://epchan.blogspot.com/2008/05/parameterless-trading-models.html)

和

[这里](http://epchan.blogspot.com/2008/08/more-on-parameterless-trading-model.html)

)和我的

[书籍](http://www.amazon.com/dp/0470284889?tag=quantitativet-20&camp=14573&creative=327641&linkCode=as1&creativeASIN=0470284889&adid=1ZQ6268JYSSZDWNC9976&)

就会知道我对参数优化的看法：我不是它的粉丝。这是因为我相信金融时间序列太非平稳，不能让人说出在回测中最优的就是未来最优的。我所知道的大部分交易者宁愿交易一个对参数小变化不敏感的策略，或者另一点，“参数无关”的策略，这实际上是具有不同参数的模型的平均值。

话说回来，如果你只能用一个特定的参数集交易一个模型，理性地问如何挑选最佳（最优）的参数集是合理的。许多交易模型有很多参数，同时找到所有这些参数的最优值是非常繁琐的。最近，罗恩·舍恩伯格发表了一篇

[文章](http://www.futuresmag.com/Issues/2010/February-2010/Pages/Using-DOE-method-in-trading.aspx)

在《期货杂志》上详细介绍了一种只用极少计算资源就能实现的方法。

罗恩使用的关键技术是将收益表面作为参数的函数进行三次多项式拟合。罗恩在 larry connors 的书“

[短期交易策略](http://www.amazon.com/dp/0981923909?tag=quantitativet-20&camp=14573&creative=327641&linkCode=as1&creativeASIN=0981923909&adid=1BPFA03ZZFNQ82NW23QT&)

"作为一个例子。这个策略有 5 个需要优化的参数，但罗恩只需要为 62 组不同的参数计算收益，整个过程只需要 58 秒。

尽管罗恩已经确认 connors 挑选的大部分参数都是接近最优的，但他确实发现了一些惊喜：具体来说，RSI 周期 3 或 4 的盈利能力明显高于 connors 使用的 2，至少在回测期间是这样的。

现在，为了真正测试这种优化，如果罗恩在保留一些样本外数据的情况下进行这种优化，这将有助于了解这些参数在保留的数据集中是否仍然是最优的。由于他没有这样做，我们需要再等一年才能自己找出答案！
