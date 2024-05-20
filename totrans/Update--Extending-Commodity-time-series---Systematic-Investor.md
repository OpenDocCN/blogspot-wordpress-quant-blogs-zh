<!--yml
category: 未分类
date: 2024-05-18 14:32:44
-->

# Update: Extending Commodity time series | Systematic Investor

> 来源：[https://systematicinvestor.wordpress.com/2013/07/04/update-extending-commodity-time-series/#0001-01-01](https://systematicinvestor.wordpress.com/2013/07/04/update-extending-commodity-time-series/#0001-01-01)

[Home](https://systematicinvestor.wordpress.com/ "Go to homepage")

>

[R](https://systematicinvestor.wordpress.com/category/r/)

> Update: Extending Commodity time series

## Update: Extending Commodity time series

I showed an example of [Extending Commodity time series](https://systematicinvestor.wordpress.com/2012/11/22/extending-commodity-time-series/) back in 2012\. Since then, the web site that I used to get the [Thomson Reuters/Jefferies CRB Index](http://www.jefferies.com/cositemgr.pl/html/ProductsServices/SalesTrading/Commodities/ReutersJefferiesCRB/IndexData/index.shtml) data is no longer working. But there are a few alternatives:

There is a difference between these two series. I did not found a reason for the discrepancy, but truthfully, I did not look very hard. So I welcome any insights or feedback.

The [Thomson Reuters / Jefferies CRB Index](http://www.jefferies.com/Commodities/2cc/389) time series is better fit for the DBC and GSG etfs.

Now let’s plot the CRB index alternatives and DBC and GSG Commodity ETFs side by side to visual check the similarity.

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

[![plot1](img/ab6e7c3e949936baa23996af38abc5a5.png)](https://systematicinvestor.wordpress.com/wp-content/uploads/2013/07/plot1.png)