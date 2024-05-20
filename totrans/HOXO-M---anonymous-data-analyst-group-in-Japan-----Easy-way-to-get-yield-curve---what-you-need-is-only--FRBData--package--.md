<!--yml
category: 未分类
date: 2024-05-18 06:49:02
-->

# HOXO-M - anonymous data analyst group in Japan - : Easy way to get yield curve : what you need is only "FRBData" package !

> 来源：[http://mockquant.blogspot.com/2011/04/easy-way-to-get-yield-curve-what-you.html#0001-01-01](http://mockquant.blogspot.com/2011/04/easy-way-to-get-yield-curve-what-you.html#0001-01-01)

I made 

[FRBData package](http://cran.r-project.org/web/packages/FRBData/index.html)

 and registerd it on CRAN.

This package allow you to download financial data from

[FRB's website](http://www.federalreserve.gov/)

.

[This website](http://www.federalreserve.gov/econresdata/default.htm)

 provide many economical data such as consumer credit, money stock.

This article show you how to use this package.

(But, it has only a function about interest rate now.　I will create other functions to download other macro-economical data in next version.)

First, because some mirror-site don't update this package at this time, you should install it via CRAN.

(you may need to install the R which has version more than 2.12.)

<fieldset>
[Created by Pretty R at inside-R.org](http://www.inside-r.org/pretty-r "Created by Pretty R at inside-R.org")</fieldset>

Load library.

<fieldset>
[Created by Pretty R at inside-R.org](http://www.inside-r.org/pretty-r "Created by Pretty R at inside-R.org")</fieldset>

As an example, we download treasury and swap curve from 2005 to 2011.

<fieldset>

```
start <- as.Date("2005-12-31")
end   <- as.Date("2011-03-31")
```

```
curve.treasury <- GetInterestRates("TCMNOM", from = start, to = end)
curve.swap     <- GetInterestRates("SWAPS",  from = start, to = end)
```

[Created by Pretty R at inside-R.org](http://www.inside-r.org/pretty-r "Created by Pretty R at inside-R.org")</fieldset>

these data are an xts object.

<fieldset>

```
> class(curve.swap)
[1] "xts" "zoo"
> head(curve.swap)
             1Y   2Y   3Y   4Y   5Y   7Y  10Y  30Y
2006-01-03 4.83 4.81 4.80 4.82 4.83 4.86 4.90 5.05
2006-01-04 4.79 4.76 4.76 4.78 4.80 4.84 4.90 5.08
2006-01-05 4.79 4.76 4.76 4.77 4.79 4.83 4.89 5.06
2006-01-06 4.81 4.78 4.78 4.80 4.81 4.85 4.90 5.08
2006-01-09 4.81 4.77 4.77 4.78 4.80 4.83 4.88 5.05
2006-01-10 4.83 4.81 4.80 4.82 4.83 4.86 4.92 5.08
```

[Created by Pretty R at inside-R.org](http://www.inside-r.org/pretty-r "Created by Pretty R at inside-R.org")</fieldset>

plot "10Y swap spread"

<fieldset>

```
#plot 10Y swap spread
plot(curve.swap[, "10Y"] - curve.treasury[, "10Y"], main = "swap spread")
```

[Created by Pretty R at inside-R.org](http://www.inside-r.org/pretty-r "Created by Pretty R at inside-R.org")</fieldset>

plot time-varying treasury term structure

<fieldset>

```
#plot yield curve by each year
curve.treasury.each.year <- t(curve.treasury[endpoints(curve.swap, on = "years")])
par(xaxt="n")
matplot(curve.treasury.each.year, main = "time-varying treasury yield curve",
 type = "l", lwd = 2,lty = 1, xlab = "Term", ylab = "Yield")
legend(8.5, 2.0, legend = substr(colnames(curve.treasury.each.year), 1, 4),
 col=1:ncol(curve.treasury.each.year), lty = 1, lwd = 2)
par(xaxt = "s")
axis(1,1:length(rownames(curve.treasury.each.year)),rownames(curve.treasury.each.year))
```

[Created by Pretty R at inside-R.org](http://www.inside-r.org/pretty-r "Created by Pretty R at inside-R.org")</fieldset>

If you would like to get other interest rate data, please check 

[Reference manual](http://cran.r-project.org/web/packages/FRBData/FRBData.pdf)

.

I think that this package will provide you good chance of analyzing yield curve such as yield curve e arbitrage.

Enjoy !

(...and tell me interesting quant job in secret :) )