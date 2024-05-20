<!--yml
category: 未分类
date: 2024-05-18 14:32:03
-->

# 7Twelve Back-test | Systematic Investor

> 来源：[https://systematicinvestor.wordpress.com/2013/08/15/7twelve-back-test/#0001-01-01](https://systematicinvestor.wordpress.com/2013/08/15/7twelve-back-test/#0001-01-01)

I recently came across the [The 7Twelve Portfolio](http://www.7twelveportfolio.com/index.html) strategy. I like the catchy name and the strategy report, [“An Introduction to 7Twelve.”](http://www.7twelveportfolio.com/Downloads/7Twelve-Model-Intro.pdf) Following is some additional info about the [The 7Twelve Portfolio](http://www.7twelveportfolio.com/index.html) strategy that I found useful:

Today I want to show how to back-test the [The 7Twelve Portfolio](http://www.7twelveportfolio.com/index.html) strategy using the [Systematic Investor Toolbox](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/).

Let’s start by loading historical data

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

Next, let’s make the [The 7Twelve Portfolio](http://www.7twelveportfolio.com/index.html) strategy with annual/ quarterly and monthly rebalancing.

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

[![plot1](img/dbd90fc45d472237f32c0ec38757bc80.png)](https://systematicinvestor.wordpress.com/wp-content/uploads/2013/08/plot11.jpg)

The strategy does better than the Vanguard 500 Index benchmark, but still suffers a huge draw-down in 2008-2009 period.

How would you make it a better strategy? Please share your ideas.

To view the complete source code for this example, please have a look at the [bt.7twelve.strategy.test() function in bt.test.r at github](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r).