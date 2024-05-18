<!--yml
category: 未分类
date: 2024-05-18 14:49:57
-->

# Timely Portfolio: Experiments in Time Series Clustering

> 来源：[http://timelyportfolio.blogspot.com/2015/03/experiments-in-time-series-clustering.html#0001-01-01](http://timelyportfolio.blogspot.com/2015/03/experiments-in-time-series-clustering.html#0001-01-01)

Last night I spotted this tweet about the R package [TSclust](http://cran.r-project.org/web/packages/TSclust/index.html).

I should start by saying that I really don’t know what I’m doing, **so be warned**.  I thought it would interesting to apply TSclust to the S&P 500 price time series.  I took the 1-day simple rate of change, grouped by year with dplyr, and then indexed by the day of the year all in one [pipeR](http://renkun.me/pipeR-tutorial/) pipeline.  Since the TSclust paper

> TSclust: An R Package for Time Series Clustering
> 
> Journal of Statistical Software, Volume 62, Issue 1
> 
> November 2014
> 
> [http://www.jstatsoft.org/v62/i01/paper](http://www.jstatsoft.org/v62/i01/paper "http://www.jstatsoft.org/v62/i01/paper")

demonstrates interoperability with hclust in their OECD interest rate example ( Section 5.2 ), I thought I could visualize the results nicely with [treewidget from the epiwidgets package](http://www.buildingwidgets.com/blog/2015/2/26/week-08-interactive-phylogeny).  Just because the htmlwidget was designed for phylogeny doesn’t mean we can’t use it for finance.  Here is the result.

For reference and searching, I’ll copy the code below, but all of this can be found in this [Github repo](https://github.com/timelyportfolio/TSclust_experiments).

```
 library(TSclust)
library(quantmod)
library(dplyr)
library(pipeR)
library(tidyr)
library(epiwidgets)

sp5 >%
  # dplyr doesn't like xts, so make a data.frame
  (
    data.frame(
      date = index(.)
      ,price = .[,1,drop=T]
    )
  ) %>>%
  # add a column for Year
  mutate( year = as.numeric(format(date,"%Y"))) %>>%
  # group by our new Year column
  group_by( year ) %>>%
  # within each year, find what day in the year so we can join
  mutate( pos = rank(date) ) %>>%
  mutate( roc = price/lag(price,k=1) - 1 ) %>>%
  # can remove date
  select( -c(date,price) ) %>>%
  as.data.frame %>>%
  # years as columns as pos as row
  spread( year, roc ) %>>%
  # remove last year since assume not complete
  ( .[,-ncol(.)] ) %>>%
  # remove pos since index will be same
  select( -pos ) %>>%
  # fill nas with previous value
  na.fill( 0 ) %>>%
  t %>>%
  # use TSclust diss; notes lots of METHOD options
  diss( METHOD="ACF" ) %>>%
  hclust %>>%
  ape::as.phylo() %>>% 
  treewidget

```