<!--yml
category: 未分类
date: 2024-05-18 14:32:36
-->

# Longer-history back-tests | Systematic Investor

> 来源：[https://systematicinvestor.wordpress.com/2013/07/12/longer-history-back-tests/#0001-01-01](https://systematicinvestor.wordpress.com/2013/07/12/longer-history-back-tests/#0001-01-01)

One of the important steps of evaluating new trading idea or strategy is to see how it behaved historically (i.e. create back-test and examine the equity curve in different economic and market conditions)

However, creating a long back-test is usually problematic because most ETFs do not have a long price history. One way to alleviate the short price history is to find an appropriate proxy asset/index to extend ETF’s price history.

For example in my last post, [Update: Extending Commodity time series](https://systematicinvestor.wordpress.com/2013/07/04/update-extending-commodity-time-series/), I showed howyou can extend the price history of commodity ETFs with [Thomson Reuters / Jefferies CRB Index](http://www.jefferies.com/Commodities/2cc/389).

I created [two functions in data.proxy.r at github](https://github.com/systematicinvestor/SIT/blob/master/R/data.proxy.r) to help visualize and compute statistics for potential proxy time series:

*   proxy.test function will create a plot and compute summary statistics over the common period for all given series
*   proxy.overlay.plot function will create an overlay plot for all given series (a plot where all shorter series are overlayed over the longest one)

Following is an example of using these functions for commodity ETFs and [Thomson Reuters / Jefferies CRB Index](http://www.jefferies.com/Commodities/2cc/389).

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

[![plot1](img/0dbc902fc06aed0786347627b883ab41.png)](https://systematicinvestor.wordpress.com/wp-content/uploads/2013/07/plot1.jpg)

[![plot2](img/80677b52d12264bb0834979442cdd867.png)](https://systematicinvestor.wordpress.com/wp-content/uploads/2013/07/plot2.jpg)

The [Thomson Reuters / Jefferies CRB Index](http://www.jefferies.com/Commodities/2cc/389) (CRB_1) looks a better fit for commodity ETFs.

Yahoo Finance contains a big collection of indices with long histories. Just to give you an example, following is a list of some indices for major asset classes:

*   Equity Market

*   Vanguard Total Stock Mkt (VTSMX)
*   Vanguard Total Intl Stock (VGTSX)
*   Vanguard 500 Index (VFINX)
*   Vanguard Emerging Mkts (VEIEX)

*   Fixed Income Market

*   Vanguard Short-Term Treasury (VFISX)
*   Vanguard Long-Term Treasury (VUSTX)
*   Vanguard Total Bond Market (VBMFX)
*   Vanguard High-Yield Corporate (VWEHX)
*   PIMCO Emerging Markets Bond (PEBIX)
*   Vanguard Inflation-Protected (VIPSX)
*   PIMCO Total Return (PTTRX)

*   Vanguard REIT (VGSIX)

Now let’s look at an example of extending real estate time ETFs:

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

[![plot3](img/2f1ef9c35da3c895b9a575af3d6385b6.png)](https://systematicinvestor.wordpress.com/wp-content/uploads/2013/07/plot3.jpg)

[![plot4](img/ac8003a69728b413b54b34fbf48a00fc.png)](https://systematicinvestor.wordpress.com/wp-content/uploads/2013/07/plot4.jpg)

The Vanguard REIT (VGSIX) Index looks as a good proxy for the Dow Jones U.S. Real Estate Index (IYR), while Dow Jones Global Real Estate Index (RWO) does behave differently.

So the next time you are faced with a task of running a long history back-test, please have a look at extending your short history assets with proxies.