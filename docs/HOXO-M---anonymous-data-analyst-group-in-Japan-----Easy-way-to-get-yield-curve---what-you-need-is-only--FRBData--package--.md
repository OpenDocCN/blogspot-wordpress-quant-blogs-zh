<!--yml

类别：未分类

日期：2024-05-18 06:49:02

-->

# HOXO-M - 日本的匿名数据分析集团 -：获取收益率曲线的简便方法：你只需要 "FRBData" 软件包！

> 来源：[`mockquant.blogspot.com/2011/04/easy-way-to-get-yield-curve-what-you.html#0001-01-01`](http://mockquant.blogspot.com/2011/04/easy-way-to-get-yield-curve-what-you.html#0001-01-01)

我做

[FRBData 软件包](http://cran.r-project.org/web/packages/FRBData/index.html)

并在 CRAN 上注册了它。

此软件包允许您从中下载财务数据

[FRB 的网站](http://www.federalreserve.gov/)

.

[此网站](http://www.federalreserve.gov/econresdata/default.htm)

提供许多经济数据，如消费者信贷、货币供应量。

本文向您展示了如何使用此软件包。

（但是，它目前只有一个与利率相关的功能。我将在下一个版本中创建其他功能来下载其他宏观经济数据。）

首先，因为某些镜像站点目前没有更新此软件包，您应该通过 CRAN 安装它。

（您可能需要安装版本大于 2.12 的 R。）

<fieldset>

[由 Pretty R 在 inside-R.org 上创建](http://www.inside-r.org/pretty-r "由 Pretty R 在 inside-R.org 上创建")</fieldset>

加载库。

<fieldset>

[由 Pretty R 在 inside-R.org 上创建](http://www.inside-r.org/pretty-r "由 Pretty R 在 inside-R.org 上创建")</fieldset>

作为示例，我们从 2005 年到 2011 年下载国库券和互换曲线。

<fieldset>

```
start <- as.Date("2005-12-31")
end   <- as.Date("2011-03-31")
```

```
curve.treasury <- GetInterestRates("TCMNOM", from = start, to = end)
curve.swap     <- GetInterestRates("SWAPS",  from = start, to = end)
```

[由 Pretty R 在 inside-R.org 上创建](http://www.inside-r.org/pretty-r "由 Pretty R 在 inside-R.org 上创建")</fieldset>

这些数据是 xts 对象。

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

[由 Pretty R 在 inside-R.org 上创建](http://www.inside-r.org/pretty-r "由 Pretty R 在 inside-R.org 上创建")</fieldset>

绘制 "10 年期互换点差"

<fieldset>

```
#plot 10Y swap spread
plot(curve.swap[, "10Y"] - curve.treasury[, "10Y"], main = "swap spread")
```

[由 Pretty R 在 inside-R.org 上创建](http://www.inside-r.org/pretty-r "由 Pretty R 在 inside-R.org 上创建")</fieldset>

绘制时变国库券期限结构

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

[由 Pretty R 在 inside-R.org 上创建](http://www.inside-r.org/pretty-r "由 Pretty R 在 inside-R.org 上创建")</fieldset>

如果您想获取其他利率数据，请查看

[参考手册](http://cran.r-project.org/web/packages/FRBData/FRBData.pdf)

.

我认为这个软件包将为您提供分析收益率曲线的良好机会，比如收益率曲线套利。

祝你愉快！

（...并私下告诉我一些有趣的量化工作：））
