<!--yml

类别：未分类

日期：2024-05-18 15:16:06

-->

# 及时投资组合：Russell Napier，ASIP 在 FT 中表示新兴市场货币

> 来源：[`timelyportfolio.blogspot.com/2011/05/russell-napier-asip-in-ft-says-emerging.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/05/russell-napier-asip-in-ft-says-emerging.html#0001-01-01)

显然，我已经屈服于确认偏差，因为今年我的第二喜欢的 CFA 协会年度会议演讲来自苏格兰本地人 Russell Napier，ASIP，他的观点与我几乎完全一致。[`video.ft.com/v/946244201001/Long-View-Historian-sees-S-P-fall-to-400`](http://video.ft.com/v/946244201001/Long-View-Historian-sees-S-P-fall-to-400)

作为《巴伦周刊》春季大型资金调查中最看空的基金经理之一，我预测标普 500 指数将跌至 900 点，因此我无法想象他预计的标普 500 可能的价格为 400 点会遭到多大的阻力。然而，考虑到对下一危机或 Napier 的“大重置”的不恰当反应，900 到 400 并不是完全不可想象的。

> “Kenton Russell，经纪公司 Sterne Agee 的分析师，曾经看涨，但现在毫不掩饰自己的看跌态度。他说：“人们的主要假设是美元稳定。“如果你在持有美国的长债和股票时忽视了美元，那么你没有关注这个交易最关键的要素。”
> 
> 基于美元的贬值，周三对欧元的汇率创下了 15 个月新低，Russell 表示，市场回到了金融危机前看到的“低点”。他预计在未来一年左右，股市将下跌约 20%，随着投资者意识到美国已经“达到财政和货币政策的极限”，道琼斯工业平均指数(DJIA)可能会跌至 9500 点，标普 500 指数(S&P)可能会跌至 900 点。
> 
> 20%的调整“并不意味着崩溃”，Russell 表示，尽管有些人可能会认为它会像。他建议做空[iShares Russell 2000](http://online.barrons.com/public/quotes/main.html?type=djn&symbol=IWM)交易所交易基金(IWM)，买入[iShares MSCI Emerging Markets](http://online.barrons.com/public/quotes/main.html?type=djn&symbol=EEM)ETF(EEM)，因为他认为亚洲货币被低估了。

我们都非常强烈地同意我们对新兴市场货币的看法。试图将我上周在会议上听到和学到的内容与我的博客和 R 结合起来，我想我应该更新我 2011 年 3 月的帖子[长 EEM 短 IWM-它以 3 种方式起作用](http://timelyportfolio.blogspot.com/2011/03/long-eem-short-iwm-how-it-works-in-3.html)。这个想法在 R 中很容易分析，即使是零售投资者也很容易实现。所有细节请参阅[原帖](http://timelyportfolio.blogspot.com/2011/03/long-eem-short-iwm-how-it-works-in-3.html)。这里是更新后的图表和一些新的图表。

R 代码：

require(quantmod)

require(PerformanceAnalytics)

require(fAssets)

require(ggplot2)

tckr<-c("EEM","IEF","IWM","GLD","SPY")

start<-"2005-01-01"

end<- format(Sys.Date(),"%Y-%m-%d") # yyyy-mm-dd

# 从 Yahoo! Finance 获取 tckr 指数数据

getSymbols(tckr, from=start, to=end)

EEM<-adjustOHLC(EEM,use.Adjusted=T)

IEF<-adjustOHLC(IEF,use.Adjusted=T)

IWM<-adjustOHLC(IWM,use.Adjusted=T)

GLD<-adjustOHLC(GLD,use.Adjusted=T)

SPY<-adjustOHLC(SPY,use.Adjusted=T)

EEM<-to.weekly(EEM, indexAt='endof')

IEF<-to.weekly(IEF, indexAt='endof')

IWM<-to.weekly(IWM, indexAt='endof')

GLD<-to.weekly(GLD, indexAt='endof')

SPY<-to.weekly(SPY, indexAt='endof')

EEMIWM<-to.weekly(EEM/IWM, indexAt='endof')

RetToAnalyze<-merge(weeklyReturn(EEM),weeklyReturn(IEF),weeklyReturn(IWM),weeklyReturn(GLD),weeklyReturn(SPY),weeklyReturn(EEMIWM))

colnames(RetToAnalyze)<-c(tckr,"EEMIWM")

assetsDendrogramPlot(as.timeSeries(RetToAnalyze))

assetsCorEigenPlot(as.timeSeries(RetToAnalyze))

mtext("来源：Yahoo! Finance",side=1,adj=0)

chart.Correlation(RetToAnalyze[,1:6,drop=F], main="自 2005 年以来的相关性")

mtext("来源：Yahoo! Finance",side=1,adj=0)

#获取与 IEF（债券）和 SPY（股票）的滚动相关性

corEEMIWMtoBonds<-runCor(RetToAnalyze[,6],RetToAnalyze[,2],25)

corEEMIWMtoStocks<-runCor(RetToAnalyze[,6],RetToAnalyze[,5],25)

chartSeries(EEMIWM,TA="addBBands();addTA(corEEMIWMtoBonds);addTA(corEEMIWMtoStocks)",theme="white")

mtext("来源：Yahoo! Finance",side=1,adj=0)

#下行风险比较

downsideTable<-melt(cbind(rownames(table.DownsideRisk(RetToAnalyze)),table.DownsideRisk(RetToAnalyze)))

colnames(downsideTable)<-c("Statistic","Portfolio","Value")

ggplot(downsideTable, stat="identity", aes(x=Statistic,y=Value,fill=Portfolio)) + geom_bar(position="dodge") + coord_flip()

mtext("来源：Yahoo! Finance",side=1,adj=0)

chart.Boxplot(RetToAnalyze,main="2005 年至 2011 年 5 月各种资产的箱线图")

mtext("来源：Yahoo! Finance",side=1,adj=0)

assetsRiskReturnPlot(RetToAnalyze)

table.CaptureRatios(RetToAnalyze[,6],RetToAnalyze[,5])

pfolioHist(RetToAnalyze[,6])

assetsMomentsPlot(as.timeSeries(RetToAnalyze), main="自 2005 年以来各种资产的时刻图")
