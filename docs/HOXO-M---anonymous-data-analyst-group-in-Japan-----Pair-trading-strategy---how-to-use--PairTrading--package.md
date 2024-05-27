<!--yml

类别：未分类

日期：2024 年 05 月 18 日 06:48:47

-->

# HOXO-M - 日本匿名数据分析小组 - : 对倒交易策略：如何使用“PairTrading”包

> 来源：[`mockquant.blogspot.com/2011/10/introduction-to-pairtrading-package.html#0001-01-01`](http://mockquant.blogspot.com/2011/10/introduction-to-pairtrading-package.html#0001-01-01)

本文向您展示了如何使用它。

对倒交易是一种市场中性交易策略，让交易者有机会在任何市场情况下获利。这种策略的理念非常简单。

1：选择两只（或任何资产）走势相似的股票

2：做空表现优异的股票，买入表现不佳的股票

3：如果“价差”（两只股票之间的价格差异）

收敛，请平仓。

所以，让我们开始解释如何使用这个包。

（这个例子在该包的 PDF 手册中）

**0：安装和加载包**

你可以像加载其他包一样通过 CRAN 安装和加载“PairTrading”包。

**1：加载样本数据**

我们在包中准备了样本股价数据。您可以使用“data”命令加载它。

```
> #load sample stock price data
> [data](http://inside-r.org/r-doc/utils/data)(stock.price)
```

**2：估计参数**

接下来，我们提取两只股票价格（从 2008 年 3 月 31 日）并估计参数。

```
> #select 2 stocks
> price.pair <- stock.price[,1:2]["2008-03-31::"]
> #Estimate parameters & plot spread
> reg <- EstimateParameters(price.pair, method = lm)
```

目前，我们只有正常的线性回归方法来估计参数，但将来我们将开发更复杂的方法。

估计结果包括以下内容。

```
> [str](http://inside-r.org/r-doc/utils/str)(reg) List of 3
 $ spread     :An ‘[xts](http://inside-r.org/packages/cran/xts)’ object from 2008-03-31 to 2011-08-05 containing:
  Data: num [1:821, 1] 0.26 0.271 0.294 0.275 0.255 ...
 - [attr](http://inside-r.org/r-doc/base/attr)(*, "dimnames")=List of 2
  ..$ : NULL
  ..$ : chr "7203"
  Indexed [by](http://inside-r.org/r-doc/base/by) [objects](http://inside-r.org/r-doc/base/objects) of [class](http://inside-r.org/r-doc/base/class): [[Date](http://inside-r.org/packages/cran/date)] TZ: 
  [xts](http://inside-r.org/packages/cran/xts) Attributes:  
 NULL
 $ hedge.ratio: num 0.285
 $ premium    : num 6.34
```

在这个估计中最重要的是“价差”，然后我们尝试绘制它。

而且，您可以使用“IsStationary”函数检查其平稳性。

这个函数返回两种单位根检验的结果。

```
> #check stationarity
> IsStationary(reg$spread, 0.1)
 PP.test adf.test 
    TRUE     TRUE 
```

（增广迪基-福勒检验（ADF）和

**3：为回测估计参数**

要运行回测，您必须使用“EstimateParametersHistorically”（菲利普斯-佩隆检验）历史估计参数。

"

方法。这个函数做了类似“滚动回归”的事情来估计参数。这一点与“EstimateParameter”函数不同。

```
> #estimate parameters for back test
> params <- EstimateParametersHistorically(price.pair, period = 180)
> #create & plot trading signals
> str(params)
An ‘xts’ object from 2008-12-18 to 2011-08-05 containing:
  Data: num [1:642, 1:3] 0.065 0.0577 0.0396 0.0136 0.021 ...
 - attr(*, "dimnames")=List of 2
  ..$ : NULL
  ..$ : chr [1:3] "spread" "hedge.ratio" "premium"
  Indexed by objects of class: [Date] TZ: 
  xts Attributes:  
 NULL
```

**4：创建交易信号**

接下来，您可以使用估计的价差创建交易信号。“Simple”函数提供了一个非常简单的交易策略（如果价差高于（低于）指定值，则买入（卖出））。

```
> #create & plot trading signals
> signal <- Simple(params$spread, 0.05)
> barplot(signal,col="blue",space = 0, border = "blue",xaxt="n",yaxt="n",xlab="",ylab="")
> par(new=TRUE)
> plot(params$spread)
```

在这种情况下，交易信号如下图所示。

最后，您可以使用“Return”函数检查对倒交易的绩效。

```
> #performance
> return.pairtrading <- Return(price.pair, lag(signal), lag(params$hedge.ratio))
> plot(100 * cumprod(1 + return.pairtrading))
```

在这种情况下，我们的策略似乎工作正常:-)

**6：结论和备注**

对倒交易是一个众所周知的交易策略，在本文中介绍了“PairTrading”包。

我们希望修改这个包，使其更实用，并适用于真实市场。

如果您有任何建议，请告诉我。

我们还创建了一个演示幻灯片来解释对倒交易的基本概念。

如果您对此感兴趣，了解对倒交易的基本概念可能会对您有帮助。

祝您愉快！
