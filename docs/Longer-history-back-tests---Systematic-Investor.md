<!--yml

类别：未分类

日期：2024-05-18 14:32:36

-->

# 更长历史回测 | 系统投资者

> 来源：[`systematicinvestor.wordpress.com/2013/07/12/longer-history-back-tests/#0001-01-01`](https://systematicinvestor.wordpress.com/2013/07/12/longer-history-back-tests/#0001-01-01)

评估新的交易想法或策略的重要一步是看看它过去的表现如何（即创建回测并在不同的经济和市场条件下检查股票曲线）

然而，创建一个长期回测通常是有问题的，因为大多数 ETF 没有长期的价格历史。减轻短期价格历史的一种方法是找到一个适当的代理资产/指数来延长 ETF 的价格历史。

例如，在我的上一篇文章[更新：扩展商品时间序列](https://systematicinvestor.wordpress.com/2013/07/04/update-extending-commodity-time-series/)中，我展示了如何使用[汤姆森路透/杰弗里斯 CRB 指数](http://www.jefferies.com/Commodities/2cc/389)来扩展商品 ETF 的价格历史。

我在 GitHub 上的[data.proxy.r 文件中创建了两个函数](https://github.com/systematicinvestor/SIT/blob/master/R/data.proxy.r)，以帮助可视化和计算潜在代理时间序列的统计数据：

+   proxy.test 函数将为所有给定的系列在共同期间创建一个图并计算总结性统计数据

+   proxy.overlay.plot 函数将为所有给定的系列创建一个叠加图（一个所有较短系列都叠加在最长系列上的图）

以下是一个使用这些函数对商品 ETF 和汤姆森路透/杰弗里斯 CRB 指数的示例。

```

###############################################################################
# Load Systematic Investor Toolbox (SIT)
# https://systematicinvestor.wordpress.com/systematic-investor-toolbox/
###############################################################################
setInternet2(TRUE)
con = gzcon(url('http://www.systematicportfolio.com/sit.gz', 'rb'))
    source(con)
close(con)

    #*****************************************************************
    # Load historical data
    #******************************************************************   
    load.packages('quantmod')  

    tickers = spl('GSG,DBC')
    data = new.env()
    getSymbols(tickers, src = 'yahoo', from = '1970-01-01', env = data, auto.assign = T)   
        for(i in ls(data)) data[[i]] = adjustOHLC(data[[i]], use.Adjusted=T)

    # "TRJ_CRB" file was downloaded from the http://www.jefferies.com/Commodities/2cc/389
    # for "TRJ/CRB Index-Total Return"
    temp = extract.table.from.webpage( join(readLines("TRJ_CRB")), 'EODValue' )
    temp = join( apply(temp, 1, join, ','), '\n' )
    data$CRB_1 = make.stock.xts( read.xts(temp, format='%m/%d/%y' ) )

    # "prfmdata.csv" file was downloaded from the http://www.crbequityindexes.com/indexdata-form.php
    # for "TR/J CRB Global Commodity Equity Index", "Total Return", "All Dates"
    data$CRB_2 = make.stock.xts( read.xts("prfmdata.csv", format='%m/%d/%Y' ) )

    #*****************************************************************
    # Compare
    #******************************************************************    
    proxy.test(data)    

    proxy.overlay.plot(data)

```

![plot1](https://systematicinvestor.wordpress.com/wp-content/uploads/2013/07/plot1.jpg)

![plot2](https://systematicinvestor.wordpress.com/wp-content/uploads/2013/07/plot2.jpg)

汤姆森路透/杰弗里斯 CRB 指数（CRB_1）看起来更适合商品 ETF。

Yahoo Finance 包含了许多具有长期历史的指数。 just to give you an example，以下是一些主要资产类别的指数列表：

+   股票市场

+   先锋 Total Stock Mkt（VTSMX）

+   先锋 Total Intl Stock（VGTSX）

+   先锋 500 指数（VFINX）

+   先锋新兴市场（VEIEX）

+   固定收益市场

+   先锋 Short-Term Treasury（VFISX）

+   先锋长期国债（VUSTX）

+   先锋总债券市场（VBMFX）

+   先锋高收益企业债（VWEHX）

+   PIMCO 新兴市场债券（PEBIX）

+   先锋通胀保护债（VIPSX）

+   PIMCO 总回报（PTTRX）

+   先锋 REIT（VGSIX）

现在让我们看看一个扩展房地产 ETFs 的示例：

```

    #*****************************************************************
    # Load historical data
    #******************************************************************   
    load.packages('quantmod')  

    tickers = spl('IYR,VGSIX,RWO')
    data = new.env()
    getSymbols(tickers, src = 'yahoo', from = '1970-01-01', env = data, auto.assign = T)   
        for(i in ls(data)) data[[i]] = adjustOHLC(data[[i]], use.Adjusted=T)

    #*****************************************************************
    # Compare
    #******************************************************************    
    proxy.test(data)    

    proxy.overlay.plot(data)

```

![plot3](https://systematicinvestor.wordpress.com/wp-content/uploads/2013/07/plot3.jpg)

![plot4](https://systematicinvestor.wordpress.com/wp-content/uploads/2013/07/plot4.jpg)

先锋房地产投资信托指数（VGSIX）看起来是道琼斯美国房地产指数（IYR）的一个好代理，而道琼斯全球房地产指数（RWO）的表现则有所不同。

所以下次当你面临运行一个长期历史回测的任务时，请考虑用代理来扩展你的短期历史资产。
