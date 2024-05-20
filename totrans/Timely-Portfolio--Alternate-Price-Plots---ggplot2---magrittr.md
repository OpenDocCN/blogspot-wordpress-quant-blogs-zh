<!--yml
category: 未分类
date: 2024-05-18 14:52:36
-->

# Timely Portfolio: Alternate Price Plots | ggplot2 + magrittr

> 来源：[http://timelyportfolio.blogspot.com/2014/07/alternate-price-plots-ggplot2-magrittr.html#0001-01-01](http://timelyportfolio.blogspot.com/2014/07/alternate-price-plots-ggplot2-magrittr.html#0001-01-01)

Just some quick experiments with ggplot2 + magrittr to plot prices differently than the traditional ways. We will get daily data on the S&P 500 from [FRED](http://research.stlouisfed.org/fred2/) using `getSymbols` and then push it through a `magrittr` pipe to various alternative plots.

A couple notes for those who might be interested in magrittr. If you want to `->` or `<-` but do not want the pipe fun to end, then you can use `assign` like this.

```
mydata
  %T>% assign( x="sp_df", value = ., envir = .GlobalEnv ) %>%
```

Also for those who want to use the special `+` inside a pipe or just want your `+` on a different line for tidy code and easy commenting, then you can do like this.

```
ggplot( ) %>%
  + geom_point()
```

Let me know if I have it all wrong, and now some plots as promised.

```
require(ggplot2)
require(dplyr)
require(magrittr)
require(quantmod)

getSymbols("SP500", src="FRED", from = "1900-01-01", auto.assign=F) %>%
  na.omit %>%
  data.frame(
    date = index(.)
  ) %T>% assign( x="sp_df", value = ., envir = .GlobalEnv ) %>%
  mutate( year = format(date,"%Y") ) %>%
  ggplot(  aes( x=SP500, group = year ) ) %>%
    + geom_density() %>%
    + facet_wrap(~year,nrow=1) %>% 
    + coord_flip() %>%
    + theme_bw() %>%
    + theme(
        axis.line=element_blank()
        ,axis.text.x=element_blank()
        ,axis.title.x=element_blank()
      ) 
```

![plot of chunk unnamed-chunk-3](img/0ecc86dc3283db8c6f5665a75a240107.png "plot of chunk unnamed-chunk-3")

```
sp_df %>%
  ggplot( aes( x = format(date,"%Y"), y = SP500 ) ) %T>% 
  ( function(x){ print( x + geom_line() ) } ) %T>%
  ( function(x){ print( x + geom_point() ) } ) %T>%
  ( function(x){ print( x + geom_hex( bins = 20 ) ) } ) %>%
  + geom_violin()
```

![plot of chunk unnamed-chunk-3](img/4c043e19861f219867d8c1f52d1e6082.png "plot of chunk unnamed-chunk-3")![plot of chunk unnamed-chunk-3](img/1cad4f7e1ea3c90a8a4d75a3faed03e3.png "plot of chunk unnamed-chunk-3")![plot of chunk unnamed-chunk-3](img/b818aace0ae36ec7fe0c0d9722dd20e5.png "plot of chunk unnamed-chunk-3")![plot of chunk unnamed-chunk-3](img/5ab64434efe547498c596738e809f65f.png "plot of chunk unnamed-chunk-3")

If you are interested in seeing the source Rmd, then it is [here](https://github.com/timelyportfolio/magrittr_ggplot/blob/gh-pages/alternative_price_plots.Rmd). One more note is this is copied/pasted with only minor changes from Rstudio knitted Rmd.