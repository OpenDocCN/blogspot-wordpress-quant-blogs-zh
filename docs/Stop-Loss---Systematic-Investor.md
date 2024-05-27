<!--yml

类别：未分类

date: 2024-05-18 14:32:19

-->

# 止损 | 系统投资者

> 来源：[`systematicinvestor.wordpress.com/2013/07/30/stop-loss/#0001-01-01`](https://systematicinvestor.wordpress.com/2013/07/30/stop-loss/#0001-01-01)

今天我想分享并展示一个灵活的[止损功能](http://www.investopedia.com/articles/trading/08/trailing-stop-loss.asp)的示例，该功能已添加到[系统投资者工具箱](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/)中。

让我们研究一个简单的[移动平均线交叉](http://www.investopedia.com/university/movingaverage/movingaverages4.asp)策略：

+   一旦快速移动平均线穿越慢速移动平均线，则触发买入

+   一旦快速移动平均线穿越慢速移动平均线，则触发卖出

以下是一个使用 SPY 的 20 日和 50 日移动平均线的示例。

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

    tickers = spl('SPY')	

    data <- new.env()
        getSymbols(tickers, src = 'yahoo', from = '1970-01-01', env = data, auto.assign = T)
        for(i in ls(data)) data[[i]] = adjustOHLC(data[[i]], use.Adjusted=T)		
    bt.prep(data, align='keep.all', dates='1999::')

    #*****************************************************************
    # Code Strategies
    #****************************************************************** 
    prices = data$prices   

    models = list()

    #*****************************************************************
    # Code Strategies
    #****************************************************************** 
    data$weight[] = NA
        data$weight[] = 1
    models$buy.hold = bt.run.share(data, clean.signal=T)

    #*****************************************************************
    # Code Strategies : MA Cross Over
    #****************************************************************** 
    sma.fast = SMA(prices, 20)
    sma.slow = SMA(prices, 50)

    buy.signal = iif(cross.up(sma.fast, sma.slow), 1, NA)

    data$weight[] = NA
        data$weight[] = iif(cross.up(sma.fast, sma.slow), 1, iif(cross.dn(sma.fast, sma.slow), 0, NA))
    models$ma.cross = bt.run.share(data, clean.signal=T, trade.summary = TRUE)

```

接下来，我在 GitHub 上的[bt.stop.r 中的 custom.stop.fn()函数](https://github.com/systematicinvestor/SIT/blob/master/R/bt.stop.r)中处理用户定义的止损函数。让我们看一下以下 3 种不同止损的示例：

```

    #*****************************************************************
    # User Defined Stops
    #****************************************************************** 
    # fixed stop: exit trade once price falls below % from entry price
    fixed.stop <- function(weight, price, tstart, tend, pstop) {
        index = tstart : tend
        if(weight > 0)
            price[ index ] < (1 - pstop) * price[ tstart ]
        else
            price[ index ] > (1 + pstop) * price[ tstart ]
    }

    # trailing stop: exit trade once price falls below % from max price since start of trade
    trailing.stop <- function(weight, price, tstart, tend, pstop) {
        index = tstart : tend
        if(weight > 0) 
            price[ index ] < (1 - pstop) * cummax(price[ index ])
        else
            price[ index ] > (1 + pstop) * cummin(price[ index ])
    }	

    # trailing stop: exit trade once price either
    # - falls below % from max price since start of trade OR
    # - rises above % from entry price
    trailing.stop.profit.target <- function(weight, price, tstart, tend, pstop, pprofit) {
        index = tstart : tend
        if(weight > 0) {
            temp = price[ index ] < (1 - pstop) * cummax(price[ index ])

            # profit target
            temp = temp | price[ index ] > (1 + pprofit) * price[ tstart ]
        } else {
            temp = price[ index ] > (1 + pstop) * cummin(price[ index ])

            # profit target
            temp = temp | price[ index ] < (1 - pprofit) * price[ tstart ]		
        }
        return( temp )	
    }

```

每个用户定义的止损函数都有 4 个必填输入项：

+   weight – 表示仓位信号或权重

+   price – 资产的价格

+   tstart – 交易开启时的指数（时间）

+   tend – 交易关闭时的指数（时间）

此外，您还可以提供其他所需信息。

例如，上述的 fixed.stop 函数将在价格跌至低于进入价格的给定%（pstop）时退出交易，或交易被关闭。带有利润目标的跟踪止损.profit.target 函数将在以下任一情况下退出交易：

+   跟踪止损达到。即价格自交易开始以来跌至给定%（pstop）以下，或

+   达到利润目标。即价格自进入价格以来上涨至给定%（pprofit）以上

以下是将这些止损整合到回测中的示例。请注意，我只使用原始策略的买入规则来开仓，而平仓时则使用止损逻辑。

```

    #*****************************************************************
    # Exit using fixed stop
    #****************************************************************** 
    data$weight[] = NA
        data$weight[] = custom.stop.fn(coredata(buy.signal), coredata(prices), fixed.stop, 
		pstop = 1/100)
    models$ma.cross.fixed.stop = bt.run.share(data, clean.signal=T, trade.summary = TRUE)

    #*****************************************************************
    # Exit using trailing stop
    #****************************************************************** 
    data$weight[] = NA
    	data$weight[] = custom.stop.fn(coredata(buy.signal), coredata(prices), trailing.stop, 
		pstop = 1/100)
    models$ma.cross.trailing.stop = bt.run.share(data, clean.signal=T, trade.summary = TRUE)

    #*****************************************************************
    # Exit using trailing stop or profit target
    #****************************************************************** 		
    data$weight[] = NA
    	data$weight[] = custom.stop.fn(coredata(buy.signal), coredata(prices), trailing.stop.profit.target, 
		pstop = 1/100, pprofit = 1.5/100)
    models$ma.cross.trailing.stop.profit.target = bt.run.share(data, clean.signal=T, trade.summary = TRUE)

    #*****************************************************************
    # Create Report
    #****************************************************************** 	
    strategy.performance.snapshoot(models, T)

```

![plot1](https://systematicinvestor.wordpress.com/wp-content/uploads/2013/07/plot12.jpg)

没有令人兴奋的报告。固定止损很少被触发，类似于买入持有。跟踪止损减少了策略在市场中的时间，并降低了回报。带有利润目标的跟踪止损表现得略好一些。

我们可以在下面的图片中更清楚地看到止损的功能：

```

    #*****************************************************************
    # Create Plot
    #****************************************************************** 	
    dates = '2010::2010'
    # add moving averages to the strategy plot
    extra.plot.fn <- function() {
	plota.lines(sma.fast, col='red')
	plota.lines(sma.slow, col='blue')
    }

    layout(1:4)
    bt.stop.strategy.plot(data, models$ma.cross, dates = dates, layout=T, main = 'MA Cross', extra.plot.fn = extra.plot.fn, plotX = F)
    bt.stop.strategy.plot(data, models$ma.cross.fixed.stop, dates = dates, layout=T, main = 'Fixed Stop', plotX = F)
    bt.stop.strategy.plot(data, models$ma.cross.trailing.stop, dates = dates, layout=T, main = 'Trailing Stop', plotX = F)
    bt.stop.strategy.plot(data, models$ma.cross.trailing.stop.profit.target, dates = dates, layout=T, main = 'Trailing Stop and Profit Target')	

```

![plot2](https://systematicinvestor.wordpress.com/wp-content/uploads/2013/07/plot22.jpg)

阴影绿色区域表示策略投资的时期。在顶部图表中，当快速移动平均线（红线）位于慢速移动平均线（蓝线）之上时，策略做多。

下一个图表（固定止损）之所以完全投入，是因为自从我们进入交易并设定了止损点以来，市场已经起飞，而相对于交易进入价格的%止损从未被触发。

最后两张图表展示了跟踪止损逻辑。一旦我们实施了激进的利润目标，策略就不那么经常进行投资。

在创建您自己的定制止损函数时玩得开心，如果您遇到问题，请告诉我。

要查看这个示例的完整源代码，请查看[bt.stop.ma.cross.test()函数在 github 上的 bt.stop.test.r](https://github.com/systematicinvestor/SIT/blob/master/R/bt.stop.test.r)。
