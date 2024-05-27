<!--yml

分类：未分类

日期：2024-05-18 14:32:44

-->

# 更新：延长商品时间序列 | 系统投资者

> 来源：[`systematicinvestor.wordpress.com/2013/07/04/update-extending-commodity-time-series/#0001-01-01`](https://systematicinvestor.wordpress.com/2013/07/04/update-extending-commodity-time-series/#0001-01-01)

首页([`systematicinvestor.wordpress.com/ "访问主页")`](https://systematicinvestor.wordpress.com/)

R 语言([`systematicinvestor.wordpress.com/category/r/`](https://systematicinvestor.wordpress.com/category/r/))

> 更新：延长商品时间序列

## 更新：延长商品时间序列

我在 2012 年展示了一个[延长商品时间序列](https://systematicinvestor.wordpress.com/2012/11/22/extending-commodity-time-series/)的例子。从那时起，我用来获取[汤姆森路透/杰富瑞 CRB 指数](http://www.jefferies.com/cositemgr.pl/html/ProductsServices/SalesTrading/Commodities/ReutersJefferiesCRB/IndexData/index.shtml)数据的网站不再工作了。但是有几个替代方案：

这两组序列之间有一个差异。我没有找到差异的原因，但老实说，我没有仔细寻找。所以我欢迎任何见解或反馈。

汤姆森路透/杰富瑞 CRB 指数([`www.jefferies.com/Commodities/2cc/389`](http://www.jefferies.com/Commodities/2cc/389))的时间序列更适合 DBC 和 GSG etf。

现在让我们并排放置 CRB 指数替代品、DBC 和 GSG 商品 ETF 的图表，以直观检查它们的相似性。

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

    bt.prep(data, align='remove.na')

    #*****************************************************************
    # Compare
    #******************************************************************    	
    plota.matplot(scale.one(data$prices))

```

![plot1](https://systematicinvestor.wordpress.com/wp-content/uploads/2013/07/plot1.png)
