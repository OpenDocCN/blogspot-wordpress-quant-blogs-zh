<!--yml

类别: 未分类

日期：2024 年 05 月 18 日 06:49:14

-->

# HOXO-M - 匿名数据分析师团队在日本 - ：收益曲线变化的主成分分析

> 来源：[`mockquant.blogspot.com/2010/12/principal-component-analysis-to-yield.html#0001-01-01`](http://mockquant.blogspot.com/2010/12/principal-component-analysis-to-yield.html#0001-01-01)

在量化金融中，经常说收益曲线变化可以用三个因素解释，即“平行移动”、“扭曲”和“蝴蝶”。因为我发现我们可以从[FRB 的网站](http://www.federalreserve.gov/datadownload/Choose.aspx?rel=H.15)获取历史收益曲线数据，我来检查这些谚语是否正确。

收益曲线数据可以通过点击“转到下载”和“下载文件”按钮进行下载。默认数据格式为 csv。如果您想获取其他格式的数据，您应该点击“构建数据包”按钮来更改格式。

我假设下载的数据位于”

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

现在，我已经获得了收益曲线变化数据。

<fieldset>

接下来，进行主成分分析并绘制结果。

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

结果图像如下所示

这些结果表明，每三个主成分对应于“平行移动”、“扭曲”和“蝴蝶”。

累积比例由“摘要”函数显示。

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

结果是，收益曲线变化可以由三个主成分解释。
