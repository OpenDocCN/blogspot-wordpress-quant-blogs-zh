<!--yml

类别：未分类

日期：2024 年 05 月 18 日 15:19:13

-->

# 及时投资组合：长期持有 EEM 短期持有 IWM-三种方式的运作

> 来源：[`timelyportfolio.blogspot.com/2011/03/long-eem-short-iwm-how-it-works-in-3.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/03/long-eem-short-iwm-how-it-works-in-3.html#0001-01-01)

长期持有 EEM 短期持有 IWM 可能以 3 种方式进行：

1) 参见我的上一篇帖子“[亚洲货币机会](http://timelyportfolio.blogspot.com/2011/03/asian-currency-opportunity.html)”，其中货币低估意味着与美元和日元相比的潜在收益增加了 20-50% 和 50%-100%。然而，即使没有货币低估，差价也能抵御美元下跌，这对大多数美国债券、股票和房地产投资者来说是不够充分的对冲。

2) 如果货币低估程度不够，EEM 在股权基础上提供更好的增长，估值远低于等值基础。这些并不是最佳的价值指标，但它们是公开的，所以我可以在这里分享它们。

[Vanguard](https://personal.vanguard.com/us/funds/vanguard/all?sort=name&sortorder=asc) 提供的新兴市场和美国小盘股估值数据

|  |
| --- |
| 股票特征截至 2011 年 2 月 28 日 |  |  |  |
|  | 新兴市场股票指数投资 | MSCI 新兴市场指数净美元 | 小盘指数基金投资 | MSCI 美国小盘 1750 指数 |
| 股票数量 | 900 | 796 | 1722 | 1716 |
| 中位市值 | 186 亿美元 | 189 亿美元 | 18 亿美元 | 18 亿美元 |
| 市盈率 | 14.5 倍 | 14.3 倍 | 26.1 倍 | 26.1 倍 |
| 价格/账面价值比 | 2.2 倍 | 2.1 倍 | 2.1 倍 | 2.1 倍 |
| 股东权益回报率 | 21.70% | 21.00% | 10.20% | 10.20% |
| 盈利增长率 | 14.30% | 13.70% | 3.80% | 4.00% |

来自[iShares EEM](http://us.ishares.com/product_info/fund/overview/EEM.htm) 和 [iShares IWM](http://us.ishares.com/product_info/fund/overview/IWM.htm) 的新兴市场和美国小盘股估值数据

| 基本面与风险截至 2011 年 2 月 28 日 |
| --- |
|  | EEM | IWM |
| 12 个月收益率 | 1.41% | 1.09% |
| 市盈率 | 18.69 | 27.98 |
| 价格/账面价值比 | 3.44 | 3.58 |

3) 在持续且危险的高相关性环境中，差距为股票和债券提供了低相关性。

我仍然不确定这是如何计算的，但我认为这提供了对统计学另一种看法，并且我觉得其他例子并没有很好地涵盖这一点。图表上最接近的点是最相关的。

R 代码：

require(quantmod)

require(PerformanceAnalytics)

require(fAssets)

tckr<-c("EEM","IEF","IWM","GLD","SPY")

start<-"2005-01-01"

end<- format(Sys.Date(),"%Y-%m-%d") # yyyy-mm-dd

# 从雅虎!财务中获取 tckr 指数数据

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

mtext("数据来源：雅虎财经",side=1,adj=0)

chart.Correlation(RetToAnalyze[,1:6,drop=F], main="自 2005 以来的相关性")

mtext("数据来源：雅虎财经",side=1,adj=0)

#获取 IEF(债券)和 SPY(股票)的滚动相关性

corEEMIWMtoBonds<-runCor(RetToAnalyze[,6],RetToAnalyze[,2],25)

corEEMIWMtoStocks<-runCor(RetToAnalyze[,6],RetToAnalyze[,5],25)

chartSeries(EEMIWM,TA="addBBands();addTA(corEEMIWMtoBonds);addTA(corEEMIWMtoStocks)",theme="white")

mtext("数据来源：雅虎财经",side=1,adj=0)

免责声明：一如既往，这些都是我的观点，未来是不可预测的。条件会变化，我可能会在没有在博客上披露的情况下进行调整。您自己做投资决定，我绝不是在给您建议。我不对您的盈利或亏损承担任何责任。
