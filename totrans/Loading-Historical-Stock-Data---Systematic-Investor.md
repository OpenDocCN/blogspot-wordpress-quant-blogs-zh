<!--yml
category: 未分类
date: 2024-05-18 14:32:48
-->

# Loading Historical Stock Data | Systematic Investor

> 来源：[https://systematicinvestor.wordpress.com/2013/06/01/loading-historical-stock-data/#0001-01-01](https://systematicinvestor.wordpress.com/2013/06/01/loading-historical-stock-data/#0001-01-01)

Historical Stock Data is critical for testing your investment strategies. I illustrated all my back-test examples with getSymbols function from quantmod package. For example, following is a back-test comparison for a few portfolio allocation methods:

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

    tickers = spl('UUP,EMB,HYG')

    data <- new.env()

    # load historical data, getSymbols from quantmod
        getSymbols(tickers, src = 'yahoo', from = '1970-01-01', env = data, auto.assign = T)    

    # prepare data for back test
        for(i in ls(data)) data[[i]] = adjustOHLC(data[[i]], use.Adjusted=T)                            
    bt.prep(data, align='remove.na')

    #*****************************************************************
    # Code Strategies
    #******************************************************************
    obj = portfolio.allocation.helper(data$prices, periodicity = 'months', lookback.len = 250, 
        min.risk.fns = list(EW=equal.weight.portfolio,
                        RP=risk.parity.portfolio,
                        MV=min.var.portfolio,
                        MC=min.corr.portfolio)
    ) 

    models = create.strategies(obj, data)$models

    #*****************************************************************
    # Create Report
    #******************************************************************        
    strategy.performance.snapshoot(models, T)

```

The getSymbols function, from quantmod package, downloads historical stock prices from Yahoo Fiance. I often get questions about alternative ways to load data. For example, let’s say you don’t want to download prices each time you need to run a back-test, instead you are storing historical price files locally and want to use in them instead. Following are 3 examples to load historical prices from files saved on your computer:

*   1\. Load Historical Stock data from the csv files you saved from Yahoo Fiance
*   2\. Load Historical Stock data from your custom files
*   3\. Load Historical Stock from one csv file, where each column represents one stock

Just substitute any of the samples below with following line of code in my original back-test example:

```
    # load historical data, getSymbols from quantmod
        getSymbols(tickers, src = 'yahoo', from = '1970-01-01', env = data, auto.assign = T)    

```

For the first method I created a getSymbols.sit function that loads historical stock prices from csv files you saved from Yahoo Fiance. Here is an example:

```
    stock.folder = 'c:\\Stocks\\Data\\'

    # if you saved yahoo historical price files localy
    getSymbols.sit(tickers, src = 'yahoo', from = '1980-01-01', env = data, auto.assign = T, stock.folder = stock.folder)

```

For the second method, please load your historical price files with read.xts function. You will need to make sure that that one of the column headers is labeled “Close”. Here is an example:

```
    stock.folder = 'c:\\Stocks\\Data\\'

    # custom format historical price files
    for(n in tickers) {
        data[[n]] = read.xts(paste(stock.folder, n, '.csv', sep=''), format='%m/%d/%Y')
    } 

```

For the third method, please load your historical prices from one file. (i.e. each column is one stock) Here is an example:

```
    stock.folder = 'c:\\Stocks\\Data\\'

    # read from one csv file, column headers are tickers
    filename = 'histdata.csv'
    all.data = read.xts(paste(stock.folder, filename, sep=''), format='%m/%d/%Y')
    for(n in names(all.data)) {
        data[[n]] = all.data[,n]
        colnames(data[[n]]) = 'Close'
        data[[n]]$Adjusted = data[[n]]$Open = data[[n]]$High = data[[n]]$Low = data[[n]]$Close
    }

```

Have fun with your data and let me know if you run into any problems.