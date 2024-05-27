<!--yml

类别：未分类

date: 2024-05-18 14:32:11

-->

# 基于日历的板块策略 | Systematic Investor

> 来源：[`systematicinvestor.wordpress.com/2013/08/05/calendar-based-sector-strategy/#0001-01-01`](https://systematicinvestor.wordpress.com/2013/08/05/calendar-based-sector-strategy/#0001-01-01)

我最近接触到了 [Kaeppel's Sector Seasonality Strategy](http://www.cxoadvisory.com/2785/calendar-effects/kaeppels-sector-seasonality-strategy/)，该策略在 [Kaeppel's Corner: Sector Seasonality](http://www.optionetics.com/marketdata/article.aspx?aid=13623) 中有描述，并在 [Kaeppel's Corner: Get Me Back, Clarence](http://www.optionetics.com/marketdata/article.aspx?aid=18343) 中进行了更新。

今天我想展示如何使用 [Systematic Investor Toolbox](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/) 对 [Kaeppel's Sector Seasonality Strategy](http://www.cxoadvisory.com/2785/calendar-effects/kaeppels-sector-seasonality-strategy/) 进行回测。以下是策略规则：

+   在十月份结束时购买 Fidelity Select Technology (FSPTX)。

+   在一月份结束时，从 FSPTX 切换到 Fidelity Select Energy (FSENX)。

+   在五月份结束时，从 FSENX 切换到现金。

+   在八月份结束时，从现金切换到 Fidelity Select Gold (FSAGX)。

+   在九月份结束时，从 FSAGX 切换到现金。

+   通过在十月份结束时从现金切换到 FSPTX 来重复。

让我们开始加载历史数据。

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

    tickers = spl('FSPTX,FSENX,FSAGX,VFINX,BIL') 

    data <- new.env()
        getSymbols(tickers, src = 'yahoo', from = '1970-01-01', env = data, auto.assign = T)

    #--------------------------------   
    # BIL     30-May-2007 
    # load 3-Month Treasury Bill from FRED
    TB3M = getSymbols('DTB3', src='FRED', auto.assign = FALSE)		
    TB3M[] = ifna.prev(TB3M)	
    TB3M = processTBill(TB3M, timetomaturity = 1/4, 261)	
    #--------------------------------       	

    # extend BIL with 3-Month Treasury Bills
    data$BIL = extend.data(data$BIL, TB3M, scale=T)	

        for(i in ls(data)) data[[i]] = adjustOHLC(data[[i]], use.Adjusted=T)						
    bt.prep(data, align='remove.na')

```

接下来，让我们创建 2 个基准策略：

+   Vanguard 500 Index Investor (VFINX)

+   从十月份结束到五月份结束持有 VFINX，否则持有现金（VFINX/Cash）。

```

    #*****************************************************************
    # Code Strategies
    #****************************************************************** 
    prices = data$prices 
    dates = data$dates	

    models = list()

    # find period ends
    period.ends = endpoints(prices, 'months')
        period.ends = period.ends[period.ends > 0]	

    months = date.month(dates[period.ends])

    #*****************************************************************
    # Code Strategies
    #****************************************************************** 
    # Vanguard 500 Index Investor (VFINX)
    data$weight[] = NA
        data$weight$VFINX[] = 1
    models$VFINX  = bt.run.share(data, clean.signal=F) 

    # VFINX from the October[10] close through the May[5] close and cash otherwise (VFINX /Cash)
    data$weight[] = NA
        data$weight$VFINX[period.ends] = iif( months >= 10 | months <= 5, 1, 0)
        data$weight$BIL[period.ends] = iif( !(months >= 10 | months <= 5), 1, 0)
    models$VFINX_Cash  = bt.run.share(data, clean.signal=F) 	

```

最后，让我们创建 [Kaeppel's Sector Seasonality Strategy](http://www.cxoadvisory.com/2785/calendar-effects/kaeppels-sector-seasonality-strategy/) 并生成报告。

```

    #*****************************************************************
    # Calendar-based sector strategy
    #****************************************************************** 	
    # Buy Fidelity Select Technology (FSPTX) at the October close.
    # Switch from FSPTX to Fidelity Select Energy (FSENX) at the January close.
    # Switch from FSENX to cash at the May close.
    # Switch from cash to Fidelity Select Gold (FSAGX) at the August close.
    # Switch from FSAGX to cash at the September close.
    # Repeat by switching from cash to FSPTX at the October close.
    data$weight[] = NA
        # Buy Fidelity Select Technology (FSPTX) at the October close.
        data$weight$FSPTX[period.ends] = iif( months >= 10 | months < 1, 1, 0)

        # Switch from FSPTX to Fidelity Select Energy (FSENX) at the January close.
        data$weight$FSENX[period.ends] = iif( months >= 1 & months < 5, 1, 0)

        # Switch from cash to Fidelity Select Gold (FSAGX) at the August close.
        data$weight$FSAGX[period.ends] = iif( months >= 8 & months < 9, 1, 0)

        # Rest time in Cash
        data$weight$BIL[period.ends] = 1 - rowSums(data$weight[period.ends], na.rm = T)
    models$Sector  = bt.run.share(data, clean.signal=F) 	

    #*****************************************************************
    # Create Report
    #****************************************************************** 
    strategy.performance.snapshoot(models, T)

```

![plot1](https://systematicinvestor.wordpress.com/wp-content/uploads/2013/08/plot1.jpg)

从 1998 年到 2000 年，技术方面的暴露肯定产生了很大的差异。但从 2002 年以来观察策略的表现，策略仍然优于我们的基准。

![plot2](https://systematicinvestor.wordpress.com/wp-content/uploads/2013/08/plot2.jpg)

要查看此示例的完整源代码，请查看 [GitHub 上的 bt.test.r 中的 bt.calendar.based.sector.strategy.test() 函数](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
