<!--yml
category: 未分类
date: 2024-05-18 14:52:04
-->

# Timely Portfolio: Frazzini goes French

> 来源：[http://timelyportfolio.blogspot.com/2014/09/frazzini-oes-french.html#0001-01-01](http://timelyportfolio.blogspot.com/2014/09/frazzini-oes-french.html#0001-01-01)

A kind reader commented “Don’t know if you have seen it, but Frazzini goes French now too” .  I have [profusely thanked and praised](http://timelyportfolio.blogspot.com/search/label/french) Kenneth French for his incredible [data library](http://mba.tuck.dartmouth.edu/pages/faculty/ken.french/data_library.html).  Now, it appears I’ll have to repeatedly do the same for [Andrea Frazzini](http://www.econ.yale.edu/~af227/data_library.htm).

Here is a quick plot of [Quality Minus Junk (QMJ)](http://ssrn.com/abstract=231243) around the world.  The code snippet is below the chart.

[![image](img/cefe83254c59121da80e326bb7192ae0.png "image")](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiw-mOxS2Bqz7FGTESjwr-XvV0Js5J2zxxZQ5MaE-Yk_-lZSSu2tbifXZfe4Q1jDtYLUOH-3Q46II4g2iqImRE_gnicTfm6iHBEyH_HpSBFR2McIOrm6csiInIRXCRnxwAW5S6vdkczDQ/s1600-h/image%25255B7%25255D.png)

```
#ssrn citation to the paper
#Asness, Clifford S. and Frazzini, Andrea and Pedersen, Lasse Heje
#Quality Minus Junk (October 9, 2013)
#Available at SSRN: http://ssrn.com/abstract=231243

require(gdata)
require(quantmod)
require(latticeExtra)

#read spreadsheet
qmjFactors <- read.xls(
  "http://www.econ.yale.edu/~af227/data/QMJ%20-%20Factors%20-%20monthly.xlsx"
  ,pattern = "DATE"
  ,blank.lines.skip = T
  ,stringsAsFactors = F
)
#convert spreadsheet data to R xts
#remove % with gsub, make numeric, and divide by 100
qmjFactors.xts <- as.xts(
  do.call(cbind,
          lapply(
            qmjFactors[,-1]
            ,function(x){
              df<-data.frame(as.numeric(
                gsub(
                  x=x
                  ,pattern="%"
                  ,replacement=""
                )
              )/100)
              colnames(df) <- colnames(x)
              return(df)
            }
          )
  )  #date is first column; will use in order.by
  ,order.by = as.Date(qmjFactors[,1]) #as.Date(paste0(qmjFactors[,1],"-01"),format="%Y%m%d")
)

#xyplot(qmjFactors.xts)

asTheEconomist(
  xyplot(
    cumprod(1+na.omit(qmjFactors.xts))
    , scales = list( y = list( relation = "same" ) )
    , main = "Quality Minus Junk (2013)\nAsness,Frazzini, Pedersen\nhttp://ssrn.com/abstract=231243"
  )
)
```