<!--yml
category: 未分类
date: 2024-05-18 06:49:14
-->

# HOXO-M - anonymous data analyst group in Japan - : Principal component analysis to yield curve change

> 来源：[http://mockquant.blogspot.com/2010/12/principal-component-analysis-to-yield.html#0001-01-01](http://mockquant.blogspot.com/2010/12/principal-component-analysis-to-yield.html#0001-01-01)

In quantitive finance,it is often said that yield curve change is explained by three factor, "parallel shift", "twist" and "butterfly". Because I found that we can get historical yield curve data from [FRB's web site](http://www.federalreserve.gov/datadownload/Choose.aspx?rel=H.15), I check whether these proverbial facts are correct or not.

Yield curve data can be downloaded to click "Go to download" and "Download File" button. Default data format is csv. If you would like to get data another format, you should click "Build package" button to change format.

  I assume that downloaded data is located at  "

C:\tmp"

<fieldset>

```
#load data
term.structure <- read.csv("C:\\tmp\\FRB_H15.csv",stringsAsFactors=FALSE)
#use nearest 1000days data only.
term.structure <- tail(term.structure,1000)
#First column is "DATE".I don't need it.
term.structure <- term.structure[,-1]
label.term <- c("1M","3M","6M","1Y","2Y","3Y","5Y","7Y","10Y","20Y","30Y")
colnames(term.structure) <- label.term
#some rows have invalid value. I erase that's row
term.structure　<- subset(term.structure,term.structure/fieldset>1M' != "ND")
term.structure <- apply(term.structure,2,as.numeric)
#calculate diff.
term.structure.diff <- diff(term.structure)
```

</fieldset>

Now,I have gotten yield curve change data.

<fieldset>

Next,do principal component analysis and plot the result.

```
term.structure.princomp<- princomp(term.structure.diff)
factor.loadings <- term.structure.princomp$loadings[,1:3]
legend.loadings <- c("First principal component","Second principal component","Third principal component")
par(xaxt="n")
matplot(factor.loadings,type="l",
  lwd=3,lty=1,xlab = "Term", ylab = "Factor loadings")
legend(4,max(factor.loadings),legend=legend.loadings,col=1:3,lty=1,lwd=3)
par(xaxt="s")
axis(1,1:length(label.term),label.term)
```

</fieldset>

Result image is shown like below

These result imply that Each three principal component correspond to "parallel shift", "twist" and "butterfly".

Cumulative Proportion are shown by "summary" function.

<fieldset>

```
> summary(term.structure.princomp)
Importance of components:
                          Comp.1    Comp.2     Comp.3     Comp.4     Comp.5      Comp.6      Comp.7      Comp.8
Standard deviation     0.2028719 0.1381839 0.06938957 0.05234510 0.03430404 0.022611518 0.016081738 0.013068448
Proportion of Variance 0.5862010 0.2719681 0.06857903 0.03902608 0.01676075 0.007282195 0.003683570 0.002432489
Cumulative Proportion  0.5862010 0.8581690 0.92674803 0.96577411 0.98253486 0.989817052 0.993500621 0.995933111
```

</fieldset>

As a result, yield cuve change can be explained by three principal component.