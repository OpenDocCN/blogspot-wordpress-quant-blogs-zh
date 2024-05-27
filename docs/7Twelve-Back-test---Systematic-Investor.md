<!--yml

类别: 未分类

日期: 2024-05-18 14:32:03

-->

# 7Twelve 回测 | Systematic Investor

> 来源：[`systematicinvestor.wordpress.com/2013/08/15/7twelve-back-test/#0001-01-01`](https://systematicinvestor.wordpress.com/2013/08/15/7twelve-back-test/#0001-01-01)

最近我了解了[7Twelve 投资组合](http://www.7twelveportfolio.com/index.html)策略。我喜欢这个引人注目的名字和策略报告，[“7Twelve 简介”](http://www.7twelveportfolio.com/Downloads/7Twelve-Model-Intro.pdf)。以下是我发现有用的有关[7Twelve 投资组合](http://www.7twelveportfolio.com/index.html)策略的一些额外信息：

今天我想展示如何使用[Systematic Investor Toolbox](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/)来对[7Twelve 投资组合](http://www.7twelveportfolio.com/index.html)策略进行回测。

让我们从加载历史数据开始

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

    tickers = spl('VFINX,VIMSX,NAESX,VDMIX,VEIEX,VGSIX,FNARX,QRAAX,VBMFX,VIPSX,OIBAX,BIL') 

    data <- new.env()
    getSymbols(tickers, src = 'yahoo', from = '1970-01-01', env = data, auto.assign = T)

    #--------------------------------   
    # BIL     30-May-2007 
    # load 3-Month Treasury Bill from FRED
    TB3M = quantmod::getSymbols('DTB3', src='FRED', auto.assign = FALSE)		
    TB3M[] = ifna.prev(TB3M)	
    TB3M = processTBill(TB3M, timetomaturity = 1/4, 261)	
    #--------------------------------       	

    # extend	
    data$BIL = extend.data(data$BIL, TB3M, scale=T)	

    for(i in ls(data)) data[[i]] = adjustOHLC(data[[i]], use.Adjusted=T)		

    bt.prep(data, align='remove.na')

```

接下来，让我们使用年度/季度和月度再平衡来制定[7Twelve 投资组合](http://www.7twelveportfolio.com/index.html)策略。

```

    #*****************************************************************
    # Code Strategies
    #****************************************************************** 
    models = list()

    # Vanguard 500 Index Investor (VFINX)
    data$weight[] = NA
        data$weight$VFINX[] = 1
    models$VFINX  = bt.run.share(data, clean.signal=F) 

    #*****************************************************************
    # Code Strategies
    #****************************************************************** 	
    obj = portfolio.allocation.helper(data$prices, periodicity = 'years',
        min.risk.fns = list(EW=equal.weight.portfolio)
    ) 	
    models$year = create.strategies(obj, data)$models$EW

    obj = portfolio.allocation.helper(data$prices, periodicity = 'quarters',
        min.risk.fns = list(EW=equal.weight.portfolio)
    ) 	
    models$quarter = create.strategies(obj, data)$models$EW

    obj = portfolio.allocation.helper(data$prices, periodicity = 'months',
        min.risk.fns = list(EW=equal.weight.portfolio)
    ) 	
    models$month = create.strategies(obj, data)$models$EW

    #*****************************************************************
    # Create Report
    #****************************************************************** 
    strategy.performance.snapshoot(models, T)

```

![plot1](https://systematicinvestor.wordpress.com/wp-content/uploads/2013/08/plot11.jpg)

该策略优于 Vanguard 500 指数基准，但在 2008-2009 年期间仍然遭受了巨大的回撤。

你会如何使它成为更好的策略？请分享你的想法。

要查看此示例的完整源代码，请查看 GitHub 上的[bt.7twelve.strategy.test()函数在 bt.test.r 中的代码](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
