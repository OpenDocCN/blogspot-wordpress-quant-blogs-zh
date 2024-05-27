<!--yml

分类：未分类

日期：2024-05-18 14:32:48

-->

# 加载历史股票数据 | 系统投资者

> 来源：[`systematicinvestor.wordpress.com/2013/06/01/loading-historical-stock-data/#0001-01-01`](https://systematicinvestor.wordpress.com/2013/06/01/loading-historical-stock-data/#0001-01-01)

历史股票数据对于测试您的投资策略至关重要。我用 quantmod 包中的 getSymbols 函数说明了所有的回测示例。例如，以下是几种投资组合分配方法的回测比较：

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

quantmod 包中的 getSymbols 函数可以从 Yahoo Fiance 下载历史股票价格。我经常收到有关加载数据的其他方法的问题。例如，假设您不想每次运行回测时都下载价格，而是将历史价格文件保存在本地并希望使用它们。以下是三种从计算机上保存的文件中加载历史价格的示例：

+   1. 从 Yahoo Fiance 保存的 csv 文件中加载历史股票数据。

+   2. 从您的自定义文件中加载历史股票数据。

+   3. 从一个 csv 文件中加载历史股票数据，其中每一列代表一只股票。

只需在我的原始回测示例中用以下代码替换下面的示例：

```
    # load historical data, getSymbols from quantmod
        getSymbols(tickers, src = 'yahoo', from = '1970-01-01', env = data, auto.assign = T)    

```

对于第一种方法，我创建了一个 getSymbols.sit 函数，该函数从 Yahoo Fiance 保存的 csv 文件中加载历史股票价格。以下是一个示例：

```
    stock.folder = 'c:\\Stocks\\Data\\'

    # if you saved yahoo historical price files localy
    getSymbols.sit(tickers, src = 'yahoo', from = '1980-01-01', env = data, auto.assign = T, stock.folder = stock.folder)

```

对于第二种方法，请使用 read.xts 函数加载您的历史价格文件。您需要确保其中一个列标题被标记为“Close”。以下是一个示例：

```
    stock.folder = 'c:\\Stocks\\Data\\'

    # custom format historical price files
    for(n in tickers) {
        data[[n]] = read.xts(paste(stock.folder, n, '.csv', sep=''), format='%m/%d/%Y')
    } 

```

对于第三种方法，请从一个文件中加载你的历史价格数据。（即每一列代表一只股票）以下是一个示例：

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

请随意使用您的数据，如果您遇到任何问题，请告诉我。
