<!--yml

类别：未分类

日期：2024-05-18 14:51:37

-->

# 及时投资组合：使用 Ekholm（2014）分解的流行共同基金

> 来源：[`timelyportfolio.blogspot.com/2014/10/popular-mutual-funds-decomposed-with.html#0001-01-01`](http://timelyportfolio.blogspot.com/2014/10/popular-mutual-funds-decomposed-with.html#0001-01-01)

虽然我们有了上篇文章["选择权与时机权 | 由乐于回应的作者精心撰写](http://timelyportfolio.blogspot.com/2014/10/selectionshare-timingshare-masterfully.html)"的基础和动力，我们还是可以运行 Ekholm 计算来查看一些流行基金自 20 世纪 80 年代初以来是如何演变的。**记住，这些只是我的观点，并非投资建议。** 我选择这四个基金是为了

1.  资产管理规模（AUM）方面的流行度

1.  风格（主动）

1.  任期（较长）

1.  演变：（2 个向不良方向演变，2 个保持良好方向的一致性）。

这将延续我构想的一系列文章，这些文章将尝试使用[Ekholm（2014）](http://ssrn.com/abstract=2463649)的分解，确定如何将其用于共同基金选择过程。作为一个提醒，下面是[Anders Ekholm](http://www.andersekholm.fi/)撰写的一篇非常出色的论文的链接。

> Ekholm, Anders G.
> 
> 投资组合方差组成：系统风险、选择风险和时机风险
> 
> 2014 年 8 月 8 日
> 
> [`ssrn.com/abstract=2463649`](http://ssrn.com/abstract=2463649)

阅读完论文并查看下面的图表后，看看你是否能得出任何结论，该图表展示了*FPA Crescent ® 基金* (FPACX), [*Sequoia ® 基金*](http://www.sequoiafund.com) (SEQUX), *[富达 ® Contrafund ®](https://fundresearch.fidelity.com/mutual-funds/summary/316071109)* (FCNTX), 和 [*美国成长基金 ®*](https://www.americanfunds.com/funds/details/gfa/a.html) (AGTHX)的 2 年滚动 Ekholm 分解。

![image](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhrTUEGcMMY2pYyVg2NW-fGfRJQ8AVOCN6n5nRPw9uQ5UHgkHXq8W-I2dqVubY6SjOTMqpwGaXiVrH03G89molzEH7IR4rfU0mdHkQzq_HvMnhP_FbUQaZIHFHQZ80X_4OocjuEQK7cBA/s1600-h/image%25255B4%25255D.png)

一如既往，我真的很希望你能复制并扩展。如果你这样做，请让我知道。下面是代码。

```
# perform Ekholm (2012,2014) analysis on some popular mutual funds

# Ekholm, A.G., 2012
# Portfolio returns and manager activity:
#    How to decompose tracking error into security selection and market timing
# Journal of Empirical Finance, Volume 19, pp 349-358

# Ekholm, Anders G., July 21, 2014
# Components of Portfolio Variance:
#    R2, SelectionShare and TimingShare
# Available at SSRN: http://ssrn.com/abstract=2463649

library(Quandl)  # use to get Fama/French factors
library(pipeR)   # pipes are the future or R
library(rlist)   # rlist - like underscore/lodash for R lists
library(dplyr)   # super fast and really powerful
library(tidyr)   # next gen wide/long formatter package
library(latticeExtra) # old but still awesome
library(directlabels) # fantastic and works with ggplot & lattice
library(quantmod) # also will load xts

# use Quandl Kenneth French Fama/French factors
# http://www.quandl.com/KFRENCH/FACTORS_D
f <- Quandl("KFRENCH/FACTORS_D",type = "xts") / 100

# grab our function from post
# http://timelyportfolio.blogspot.com/2014/10/selectionshare-timingshare-masterfully.html
devtools::source_gist("e5728c8c7fb45dbdb6e0")

tickers <- c( "FCNTX", "AGTHX", "SEQUX", "FPACX" )
ekFunds <-  lapply(
  tickers
  ,function(ticker) {
    ticker %>>%
      getSymbols( from = "1896-01-01", auto.assign = F ) %>>%
      (fund ~  
         structure(
           fund[,6] / stats::lag( fund[,6], 1 ) - 1
           ,dimnames = list(NULL,gsub(x = colnames(fund)[6], pattern  = "[\\.]Adjusted", replacement = ""))
         )
      ) %>>%
      merge( f ) %>>% #  Quandl("KFRENCH/FACTORS_D",type = "xts") / 100
      na.omit %>>%
      rollapply (
        FUN= function(x){
          x %>>%
            jensen_ekholm %>>% 
            ( data.frame( summary(.[["linmod"]])$"r.squared" , .$ekholm ) )  %>>%
            xts(order.by=tail(index(x),1)) -> return_df
          colnames(return_df)[1] <- "R_sq"
          return(return_df)
        }
        , width = 500
        #, by = 100
        , by.column=F
        , fill = NULL
      ) %>>%
      na.fill(0)
  }
)
names(ekFunds) 
ekFunds %>>%
  list.map(
    {
      structure(
        data.frame(
          date = index(.)
          , fund = names(ekFunds)[.i]
          , .
        )
      ) %>>%
        gather(measure,value,-date,-fund)
    }
  ) %>>%
  (
    do.call( rbind , . )
  ) -> ekT

ekT %>>%
  # just plot at R², SelectionShare, and TimingShare
  filter( measure %in% c("R_sq","SelectionShare","TimingShare") ) %>>%
  (
    xyplot(
      value ~ date | measure
      , groups = fund
      , data = .
      , type = "l"
      # using direct.label so not necessary
      , auto.key = list( space = "right" )
      # title our plot
      , main = paste(
        "Comparison of Ekholm Decomposition for Various Mutual Funds"
        ,paste0("2 Year Rolling since ",format(.$date[1],format="%b %d, %Y"))
        ,sep="\n"
      )
      # layout one on top of the other
      , layout = c(1,length(unique(.$measure)))
    )
  ) %>>%
  # I like labels on plot rather than legend
  directlabels::direct.label( method = "last.qp" ) %>>%
  # pretty it up with the latticeExtra Economist theme
  asTheEconomist

```
