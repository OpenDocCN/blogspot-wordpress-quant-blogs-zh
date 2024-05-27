<!--yml

类别：未分类

日期：2024-05-18 15:18:23

-->

# 及时投资组合：10 年收益率系列的历史债券价格和总回报

> 数据来源：[`timelyportfolio.blogspot.com/2011/04/historical-bond-price-and-total-returns.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/04/historical-bond-price-and-total-returns.html#0001-01-01)

没有访问 Barclays 或 Merrill 债券指数到 1970 年代，或者 Ned Davis 到 1950 年代，研究历史债券回报是非常困难的。以下是一种获取 1962 年以来的 10 年美国国债价格和总回报的方法。我希望能追溯到 1871 年，但 Shiller 和美联储的月收益率是每日收益率的平均值，而不是月末值。将此方法应用于这些月平均值不起作用。

R 代码：

需要(RQuantLib)

需要(quantmod)

需要(PerformanceAnalytics)

获取符号("DGS10",源="FRED") #从美联储 Fred 加载美国国债 10 年

#美联储的月收益率系列是每日收益率的月平均值

#Shiller 系列也是月平均值

#计算回报的月平均值并不能工作

#因此我们得到的是每日数据，用 to.monthly 取月末数据

#不幸的是，这个系列并不能追溯到那么久远

DGS10<-to.monthly(DGS10)[,4]

DGS10 价格回报<-DGS10 #设置此选项以保存价格回报

DGS10 价格回报[1,1]<-0

DGS10 价格回报的列名<-"价格回报"

#我知道我需要矢量化这个，但还不够资格

#请随意评论以向我展示如何做到这一点

对于（i 在 1:(NROW(DGS10)-1)）{

DGS10 价格回报[i+1,1]<-固定利率债券价格(收益率=DGS10[i+1,1]/100,发行日期=系统日期(),

到期日= advance("UnitedStates/GovernmentBond", 系统日期(), 10, 3),

利率=DGS10[i,1]/100,期限=2)[1]/100-1

}

#总回报将是价格回报+收益率/12（一个月）

DGS10 总回报<-DGS10 价格回报+滞后(DGS10,k=1)/12/100

DGS10 总回报的列名<-"总回报"

图表.绩效总结(合并(DGS10 价格回报,DGS10 总回报),y 对数=TRUE,颜色集=c("海军蓝","深橄榄绿 3"),主="美国 10 年收益率的模拟回报")

mtext("数据来源：美国联邦储备银行 FRED",侧=1,调整=0)
