<!--yml
category: 未分类
date: 2024-05-18 14:50:46
-->

# Timely Portfolio: Pipeline to Plot Annual % Change

> 来源：[http://timelyportfolio.blogspot.com/2014/11/pipeline-to-plot-annual-change.html#0001-01-01](http://timelyportfolio.blogspot.com/2014/11/pipeline-to-plot-annual-change.html#0001-01-01)

[![image](img/231b3f19482296dfe063850d5ff9f650.png "image")](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgOhWTd0T4x6C1NeYkpH_rASqNKMIBQd8pt5hhXpF90H81RQFgVpnrUaip2nx0i7NIUlYRUmPtT-lIRw4EflpzmVVO52c7nezqvwZautdYvRoh2FtoBYo30jz-drML38GtzCNdQTeWR5Q/s1600-h/image%25255B4%25255D.png)

*(thanks [tradeblotter](http://tradeblotter.wordpress.com) for pointing out error in code in first release)*

Pipes in R make my life incredibly easy, and I think my code easier to read.   Note, there are a couple different flavors of pipes (see [magrittr](https://github.com/smbache/magrittr) and [pipeR](http://renkun.me/pipeR-tutorial/)).  For now, I choose pipeR.

```
library(quantmod)
library(pipeR)
library(ggplot2)

getSymbols("^GSPC",from="1900-01-01",auto.assign=F) %>>% #get S&P 500 from Yahoo!Finance
  ( .[endpoints(.,"years"),4] ) %>>% #get end of year
  ROC( type="discrete", n=1 ) %>>%   #get one year rate of change
  na.fill(0) %>>%                    #fill first year with 0
  (                                  #make data.frame
    data.frame(
      date = as.Date(format(index(.),"%Y-01-01"))
      ,.
    )
  ) %>>%
  structure(                         #hard way to do colnames()
    names = c("date","change")
  ) %>>%
  ggplot(                            #start our plot pipe
    aes( y= change, x=  date)
  ) %>>%
  + geom_bar( stat="identity" ) %>>% #choose bar
  + labs( title = "Annual Change of the S&P 500" ) #give plot a title
```

Or if we wanted to use the new pipeline syntax for the plot portion.

```
library(quantmod)
library(pipeR)
library(ggplot2)

getSymbols("^GSPC",from="1900-01-01",auto.assign=F) %>>% #get S&P 500 from Yahoo!Finance
  ( .[endpoints(.,"years"),4] ) %>>% #get end of year
  ROC( type="discrete", n=1 ) %>>%   #get one year rate of change
  na.fill(0) %>>%                    #fill first year with 0
  (                                  #make data.frame
    data.frame(
      date = as.Date(format(index(.),"%Y-01-01"))
      ,.
    )
  ) %>>%
  structure(                         #hard way to do colnames()
    names = c("date","change")
  ) %>>%
  (
    pipeline({
      ggplot(., aes( y= change, x=  date) )
      + geom_bar( stat="identity" )
      + labs( title = "Annual Change of the S&P 500 (source: Yahoo! Finance)" )
    })
  )
```