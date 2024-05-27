<!--yml

类别：未分类

日期：2024 年 5 月 18 日 14:44:12

-->

# 历史季节性分析： 道琼斯 30 公司中哪家可能在一月份表现良好？ | Systematic Investor

> 来源：[`systematicinvestor.wordpress.com/2011/12/30/historical-seasonality-analysis-what-company-in-dow-30-is-likely-to-do-well-in-january/#0001-01-01`](https://systematicinvestor.wordpress.com/2011/12/30/historical-seasonality-analysis-what-company-in-dow-30-is-likely-to-do-well-in-january/#0001-01-01)

此内容不构成投资建议。此信息仅供参考。

股市季节性很容易理解，但如果你坚持认同[有效市场假说](http://en.wikipedia.org/wiki/Efficient-market_hypothesis)，可能难以证明。想要对季节性有一个很好的总结，可以看看 Investopedia 上的[利用季节性效应（Capitalizing On Seasonal Effects）](http://www.investopedia.com/articles/05/seasonaltrends.asp#axzz1hxtr1mbl)一文。另一个有趣的讨论是 Douglas R Terry 在他的文章[有效市场假说和季节性](http://www.alhambrapartners.com/2011/12/11/efficient-market-hypothesis-and-apple-seasonality/)中详细分析了这两个观点如何共存。

我想介绍一下我开发的新工具来研究季节性。[季节性工具](http://www.systematicportfolio.com/tools)是一个用户友好、点对点、可以创建季节性统计和报告的应用程序。

为了演示[季节性工具](http://www.systematicportfolio.com/tools)，我想展示如何使用它来评估一个投资理念。我想找出[DOW 30](http://en.wikipedia.org/wiki/Dow_Jones_Industrial_Average)中哪家公司可能在一月份表现良好，并使用[季节性工具](http://www.systematicportfolio.com/tools)来评估。

以下代码从 Yahoo Finance 加载了[DOW 30](http://en.wikipedia.org/wiki/Dow_Jones_Industrial_Average)指数中所有公司的历史价格，并计算了它们在一月份的平均表现。我将使用[Systematic Investor Toolbox](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/)来加载和分析这些数据：

```

###############################################################################
# Load Systematic Investor Toolbox (SIT)
###############################################################################
con = gzcon(url('http://www.systematicportfolio.com/sit.gz', 'rb'))
    source(con)
close(con)

    #*****************************************************************
    # Load historical data
    #****************************************************************** 
    load.packages('quantmod')        
    tickers = dow.jones.components()

    data <- new.env()
    getSymbols(tickers, src = 'yahoo', from = '1970-01-01', env = data, auto.assign = T)
        for(i in ls(data)) data[[i]] = adjustOHLC(data[[i]], use.Adjusted=T)    
    bt.prep(data, align='keep.all', dates='1970::2011')

    #*****************************************************************
    # Compute monthly returns
    #****************************************************************** 
    prices = data$prices   
    n = ncol(prices)    

    # find month ends
    month.ends = endpoints(prices, 'months')

    prices = prices[month.ends,]
    ret = prices / mlag(prices) - 1

    # keep only January    
    ret = ret[date.month(index(ret)) == 1, ]

    # keep last 20 years
    ret = last(ret,20)

    #*****************************************************************
    # Compute stats
    #****************************************************************** 
    stats = matrix(rep(NA,2*n), nc=n)
        colnames(stats) = colnames(prices)
        rownames(stats) = spl('N,Positive')

    for(i in 1:n) {
        stats['N',i] = sum(!is.na(ret[,i]))
        stats['Positive',i] = sum(ret[,i]>0, na.rm=T)    
    }
    sort(stats['Positive',])

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/12/plot1-small6.png)

[华特迪士尼公司（DIS）](http://finance.yahoo.com/q?s=dis)在过去 20 年的一月份表现积极的有 17 次。

让我们使用[季节性工具](http://www.systematicportfolio.com/tools)来研究[华特迪士尼公司（DIS）](http://finance.yahoo.com/q?s=dis)的表现。

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/12/plot2-small5.png)

季节性分析报告证实 [华特迪士尼公司（DIS）](http://finance.yahoo.com/q?s=dis) 在一月份有出色的业绩记录。接下来让我们看看一月份的详细情况。

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/12/plot3-small5.png)

详细的季节性分析报告显示，[华特迪士尼公司（DIS）](http://finance.yahoo.com/q?s=dis)在 2008 年 1 月之前有着惊人的回报。随后是 3 个连续的负值 1 月，这很可能表明了这家公司的趋势（制度）发生了变化。

那么我是否期待[华特迪士尼公司（DIS）](http://finance.yahoo.com/q?s=dis)在即将到来的 1 月份呈现积极的态势？我不再那么确定了。

要查看此示例的完整源代码，请查看[github 上的 bt.test.r 中的 bt.seasonality.test()函数](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
