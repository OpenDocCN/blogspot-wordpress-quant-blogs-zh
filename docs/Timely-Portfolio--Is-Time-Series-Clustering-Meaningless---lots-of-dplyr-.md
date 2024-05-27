<!--yml

分类：未分类

date: 2024-05-18 14:49:53

-->

# 及时投资组合：时间序列聚类有意义吗？（大量 dplyr）

> 来源：[时间序列聚类实验](http://timelyportfolio.blogspot.com/2015/03/experiments-in-time-series-clustering.html)

一位好心的读者在我的[时间序列聚类实验](http://timelyportfolio.blogspot.com/2015/03/experiments-in-time-series-clustering.html)一文的评论中指引我找到了这篇论文。

> 时间序列子序列聚类是没有意义的：对先前和未来研究的启示
> 
> Eamonn Keogh 和 Jessica Lin
> 
> 加州大学河滨分校计算机科学与工程学院
> 
> [`www.cs.ucr.edu/~eamonn/meaningless.pdf`](http://www.cs.ucr.edu/~eamonn/meaningless.pdf "http://www.cs.ucr.edu/~eamonn/meaningless.pdf")

如我上篇文章所说，我不知道我在做什么，所以我没有讨论或争论时间序列聚类的依据。读了几遍论文后，我觉得我理解了他们的观点，并且我认为我所做的不“毫无意义”。在他们金融时间序列的例子中，他们使用价格并谈到试图寻找模式。我只想通过各种特征，如**收益**的自相关性而不是价格，收益的分布，以及其他各种分类器，将哪些年份最相似进行分类。

这次整个练习给了我一个很好的借口更深入地挖掘。我想分享我到目前为止所做的一切，希望读者可能会有所阐述、争论，或者给我指出好的方向。

无论你对时间序列聚类有多大的兴趣，你可能会喜欢我用 dplyr 和管道生成结果的功能。此外，我还没有看到 dplyr `do` 应用于自相关`ACF`，所以你可能想在代码的最后一段中查看一下。

这篇文章和上一篇文章的所有代码都在这个[Github 仓库](https://github.com/timelyportfolio/TSclust_experiments)中。

![image](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgwSif_WWnYlk1HqSxfwAaJJnkzxav7_p-JTi4ySlMmCa3lJN1CpIGHA6Go2MRcNI49NiyHTuU6HbtnEzGzP-YNCE1CMey_0YoGVKzjidXGBIyH1qeix4J188wvUWgbA2XHMBWAxO1Myg/s1600-h/image%25255B3%25255D.png)

```
 library(TSclust)
library(quantmod)
library(dplyr)
library(pipeR)
library(tidyr)

sp5 <- getSymbols("^GSPC",auto.assign=F,from="1900-01-01")[,4]

sp5 %>>%
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
(~sp_wide) %>>%
  # use TSclust diss; notes lots of METHOD options
  diss( METHOD="ACF" ) %>>%
  hclust %>>%
(~hc) %>>%
  ape::as.phylo() %>>% 
  treewidget #%>>%
  #htmlwidgets::as.iframe(file="index.html",selfcontained=F,libdir = "./lib")

library(lattice)
library(ggplot2)
# get wide to long the hard way
#  could have easily changed to above pipe to save long
#  as an intermediate step
#  but this makes for a fun lapply
#  and also we can add in our cluster here
sp_wide %>>%
  (
    lapply(
      rownames(.)
      ,function(yr){
        data.frame(
          year = as.Date(paste0(yr,"-01-01"),"%Y-%m-%d")
          ,cluster = cutree(hc,10)[yr]
          ,pos = 1:length(.[yr,])
          ,roc = .[yr,]
        )
      }
    )
  ) %>>%
  (do.call(rbind,.)) %>>%
(~sp_long)

sp_long %>>%
  ggplot( aes( x = roc, group = year, color = factor(cluster) ) ) %>>%
  + geom_density() %>>%
  + facet_wrap(  ~ cluster, ncol = 1 ) %>>%
  + xlim(-0.05,0.05) %>>%
  + labs(title='Density of S&P 500 Years Clustered by TSclust') %>>%
  + theme_bw() %>>%
  # thanks to my friend Zev Ross for his cheatsheet
  + theme( plot.title = element_text(size=15, face="bold", hjust=0) ) %>>%
  + theme( legend.position="none" )  %>>%
  + scale_color_brewer( palette="Paired" ) 
```

![acf_plot](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgPhHFGdmddjO-yr2TvxVACQP1u03lH-NIWXF0ZQ6dx0qXxSNNCWCZYocEv1a0J1cMBq3ez-sme5pUutT-JFWB_E06WHP71p-71ULETsOCsIRNJf5JOFkVOb-2lKwsTTQ5PQQfp2-2_qg/s1600-h/acf_plot%25255B3%25255D.png)

```
 # explore autocorrelations
sp5 %>>%
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
  ( .[,-ncol(.)] ) %>>% t -> sP

sp_long %>>%
  group_by( cluster, year ) %>>%
  do(
    . %>>%
    (
      clustd ~ 
      acf(clustd$roc,plot=F) %>>%
        (a ~
          data.frame(
            cluster = clustd[1,2]
            ,year = clustd[1,1]
            ,lag = a$lag[-1]
            ,acf = a$acf[-1]
          )
        )
    )
  ) %>>%
  as.data.frame %>>%
  ggplot( aes( x = factor(cluster), y = acf, color = factor(cluster) ) ) %>>%
    + geom_point() %>>%
    + facet_wrap( ~lag, ncol = 4 ) %>>%
    + labs(title='ACF of S&P 500 Years Clustered by TSclust') %>>%
    + theme_bw() %>>%
    # thanks to my friend Zev Ross for his cheatsheet
    + theme(
        plot.title = element_text(size=15, face="bold", hjust=0)
        ,legend.title=element_blank()
    ) %>>%
    + theme(legend.position="none")  %>>%
    + scale_color_brewer(palette="Paired") 
```

如果你能读到这里，我很乐意听到你的意见。
