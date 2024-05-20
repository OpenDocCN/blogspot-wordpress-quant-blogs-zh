<!--yml
category: 未分类
date: 2024-05-18 14:52:12
-->

# Timely Portfolio: Fama/French Factors in 1 line of code

> 来源：[http://timelyportfolio.blogspot.com/2014/08/famafrench-factors-in-1-line-of-code.html#0001-01-01](http://timelyportfolio.blogspot.com/2014/08/famafrench-factors-in-1-line-of-code.html#0001-01-01)

In the past, getting Fama/French factors from the [Kenneth French dataset](mba.tuck.dartmouth.edu/pages/faculty/ken.french/data_library.html) involved a convoluted procedure to download the zip file, unzip the file, clean the data, and convert to xts.  Now with [Quandl](http://www.quandl.com/KFRENCH/FACTORS_D), we can do it simply in one line of code.  **Note:  this data is available in multiple formats (JSON, CSV, XML) from the API and for [multiple code languages](http://www.quandl.com/help/libraries).**

```
# use Quandl Kenneth French Fama/French factors
# http://www.quandl.com/KFRENCH/FACTORS_D

library(Quandl)
library(quantmod)

f <- Quandl(
  "KFRENCH/FACTORS_D"
)

f <- as.xts(f[,-1],order.by=f[,1])

plot.zoo( f, main = NA )
mtext(
  text = "Fama/French Factors from Quandl"
  , adj = 0
  , outer = T
  , line = -2
  , cex = 2
)

```

[![image](img/788c3c1b9e0363f14e4456c3e24cc5d0.png "image")](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjxS1j5Jn3q3F0V6t0QIMSoh-6DGAUhqv_rtBmJufKPev6b4OnKCuRDuTdJxDXtA3WXQzQN-5JSqkSjtxhEmu4pNOpefjhhrvpPB235GuFhLzMyugImvESj7e-Rds5W88_46fbnJKUwDg/s1600-h/image%25255B4%25255D.png)