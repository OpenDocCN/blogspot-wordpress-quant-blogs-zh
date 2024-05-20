<!--yml
category: 未分类
date: 2024-05-18 06:48:47
-->

# HOXO-M - anonymous data analyst group in Japan - : Pair trading strategy : how to use "PairTrading" package

> 来源：[http://mockquant.blogspot.com/2011/10/introduction-to-pairtrading-package.html#0001-01-01](http://mockquant.blogspot.com/2011/10/introduction-to-pairtrading-package.html#0001-01-01)

This article shows you how you can use it.

The pair trading is a market neutral trading strategy and gives traders a chance to profit regardless of market conditions. The idea of this strategy is quite simple.

 1 : Select two stocks(or any assets) moving similarly

 2 : Short out-performing stock, buy under-performing one

 3 : If "spread"(price difference between two stocks)

converge, close your position.

So, Let's start to explain how to use this package.

(This example is in PDF manual of this package)

**0: Install & load package**

You can install and load "PairTrading" package via CRAN in the same way as other packages.

**1: Load sample data**

We prepared sample stock price data in our package. You can load it by using "data" command.

 ```
> #load sample stock price data
> [data](http://inside-r.org/r-doc/utils/data)(stock.price)
```

**2: Estimate parameters**

Next, We extract two stock prices(from 31 Mar, 2008) and estimate parameters.

```
> #select 2 stocks
> price.pair <- stock.price[,1:2]["2008-03-31::"]
> #Estimate parameters & plot spread
> reg <- EstimateParameters(price.pair, method = lm)
```

At the moment, we have only normal linear regression method to estimate parameters, but we will develop more sophisticated method in the future.

The estimation result contains the following contents.

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

The most important thing in this estimation is "spread", then we try to plot it.

 And, you can check the stationarity of that by using "IsStationary" function.

This function return the result of two types unit root test.

```
> #check stationarity
> IsStationary(reg$spread, 0.1)
 PP.test adf.test 
    TRUE     TRUE 
```

( augmented Dickey–Fuller test (ADF) and 

Phillips-Perron test) **3: Estimate parameters for back-test**

To run back-test, you have to estimate parameters historically by using "EstimateParametersHistorically

"

function. This function do something like "rolling regression" to estimate parameters. This point is different from "EstimateParameter" function.

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

**4: Create trading signal**

Next, you create trading singal using estimated spread. "Simple" function give a very simple trading strategy(If The spread is more(less) than specified value, you will buy(sell))

```
> #create & plot trading signals
> signal <- Simple(params$spread, 0.05)
> barplot(signal,col="blue",space = 0, border = "blue",xaxt="n",yaxt="n",xlab="",ylab="")
> par(new=TRUE)
> plot(params$spread)
```

In this case, The trading signal is drawn as below.

Last, you can check the performance of pair trading by using "Return" function.

```
> #performance
> return.pairtrading <- Return(price.pair, lag(signal), lag(params$hedge.ratio))
> plot(100 * cumprod(1 + return.pairtrading))
```

In this case, our strategy seems to work correctly :-)

**6: Conclusion and remarks**

Pair trading is well-known trading strategy, and I introduced "PairTrading" package in this article.

We would like to modify this package to be more useful and fit in real-market.

If you have any suggestion, please let me know.

And we created a presentation slide to explain the basic concept of pair trading.

It may be useful for you to understand the basic concept of pair trading if you are interested in it.

Enjoy!