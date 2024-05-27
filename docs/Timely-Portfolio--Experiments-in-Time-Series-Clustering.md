<!--yml

类别：未分类

日期：2024-05-18 14:49:57

-->

# 及时投资组合：时间序列聚类实验

> 来源：[`timelyportfolio.blogspot.com/2015/03/experiments-in-time-series-clustering.html#0001-01-01`](http://timelyportfolio.blogspot.com/2015/03/experiments-in-time-series-clustering.html#0001-01-01)

昨晚我注意到这条关于 R 包[TSclust](http://cran.r-project.org/web/packages/TSclust/index.html)的推文。

我应该首先说，我真的不知道我在做什么，**所以请小心**。我想将 TSclust 应用于标普 500 价格时间序列，看看会发生什么。我取了 1 天的简单变化率，用 dplyr 按年分组，然后用一天中的那一天索引，全部在一个[pipeR](http://renkun.me/pipeR-tutorial/)管道中完成。由于 TSclust 论文

> TSclust：用于时间序列聚类的 R 包
> 
> 统计软件杂志，第 62 卷，第 1 期
> 
> 2014 年 11 月
> 
> [`www.jstatsoft.org/v62/i01/paper`](http://www.jstatsoft.org/v62/i01/paper)

在他们的经合组织利率示例中展示了与 hclust 的互操作性（第 5.2 节），我认为可以用[epiwidgets 包中的 treewidget](http://www.buildingwidgets.com/blog/2015/2/26/week-08-interactive-phylogeny)很好地可视化结果。仅仅因为 htmlwidget 是为了系统发育而设计的，并不意味着我们不能用它来处理金融数据。以下是结果。

为了参考和搜索，我将复制下面的代码，但所有这些都可以在这[Github 仓库](https://github.com/timelyportfolio/TSclust_experiments)中找到。

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
