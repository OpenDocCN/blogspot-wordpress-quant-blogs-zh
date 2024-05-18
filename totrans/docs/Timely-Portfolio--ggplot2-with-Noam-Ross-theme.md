<!--yml
category: 未分类
date: 2024-05-18 14:58:52
-->

# Timely Portfolio: ggplot2 with Noam Ross theme

> 来源：[http://timelyportfolio.blogspot.com/2013/07/ggplot2-with-noam-ross-theme.html#0001-01-01](http://timelyportfolio.blogspot.com/2013/07/ggplot2-with-noam-ross-theme.html#0001-01-01)

When I first saw Noam Ross' blog post ["The null model for age effects with overdispersed infection"](http://www.noamross.net/blog/2013/6/12/multi-infection-overdispersed.html), I immediately liked the look of his ggplot2 graphs. I was even more delighted when I discovered that he has made his theme available on [github](https://github.com/noamross/noamtools/blob/master/R/theme_nr.R). Even though I am all into [rCharts](http://rcharts.io/site), I still love a beautiful publication quality R graphic.

Below is some code to combine Noam Ross' theme with `autoplot.zoo` which makes plotting `xts/zoo` objects with ggplot2 easy.

```
require(ggplot2)
require(grid)
require(RColorBrewer)
require(quantmod)

# get closing values for S&P 500 from Yahoo! Finance
sp500 <- getSymbols("^GSPC", auto.assign = FALSE)[, 4] 
```

```
 sp500$ma <- runMean(sp500, n = 200)

colnames(sp500) <- c("S&P500", "200d Mov Avg")

# get noam ross ggplot2 theme from github
source("https://raw.github.com/noamross/noamtools/master/R/theme_nr.R")
# for some reason on my computer panel.background still shows up gray this
# fixes it but might not be necessary for others
theme_nr <- theme_nr() + theme(panel.background = element_rect(fill = "white")) + 
    theme(plot.title = element_text(size = rel(2), hjust = -0.05, vjust = -0.3)) + 
    theme(plot.margin = unit(c(1, 1, 2, 1), "cm"))

autoplot(sp500, facets = NULL) + theme_nr + theme(legend.position = "none") + 
    scale_colour_manual(values = brewer.pal("Blues", n = 9)[c(6, 3)]) + geom_line(size = 1.15) + 
    xlab(NULL) + ggtitle("S&P 500 (ggplot2 theme by Noam Ross)") 
```

It isn’t perfect, but I think it offers a very nice starting point.  Using ggplot2 directly would have allowed us more control over the bothersome details.

[![Rplot](img/0ce99144b9317f9256056c236813eebb.png "Rplot")](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgixo28DNw_eE8thwbgimJVbxa5H5VoSW6cS622m24Mcr6zFchKXSFXPwBWRf3KO-xJw_WYVnJdaKSymuivNJ1P2BAlN7Tzq7mngBTF2egFHc_Lx5dOHH_OAv8kgU03CEmSq3jHw6y3DA/s1600-h/Rplot%25255B1%25255D.jpg)