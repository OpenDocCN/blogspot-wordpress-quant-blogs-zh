<!--yml

分类：未分类

日期：2024-05-18 14:32:27

-->

# 随机振荡器|系统投资者

> 来源：[`systematicinvestor.wordpress.com/2013/07/19/stochastic-oscillator/#0001-01-01`](https://systematicinvestor.wordpress.com/2013/07/19/stochastic-oscillator/#0001-01-01)

当阅读[Dekalog Blog](http://dekalogblog.blogspot.ca/2013/07/my-nn-input-tweak.html)时，我偶然发现了[John Ehlers 论文：有效的交易策略的预测指标](http://www.stockspotter.com/files/PredictiveIndicators.pdf)的链接。John Ehlers 提供了一种不同的平滑价格的方法，并将新滤波器整合到振荡器构造中。幸运的是，也提供了 EasyLanguage 代码，并且我能够将其翻译成 R。

以下是来自 John 的随机振荡器论文和测试的一些结果。

```

############################################################################### 
# Super Smoother filter 2013 John F. Ehlers
# http://www.stockspotter.com/files/PredictiveIndicators.pdf
############################################################################### 
super.smoother.filter <- function(x) {
    a1 = exp( -1.414 * pi / 10.0 )
    b1 = 2.0 * a1 * cos( (1.414*180.0/10.0) * pi / 180.0 )
    c2 = b1
    c3 = -a1 * a1
    c1 = 1.0 - c2 - c3

    x = c1 * (x + mlag(x)) / 2
        x[1] = x[2]

    out = x * NA
        out[] = filter(x, c(c2, c3), method='recursive', init=c(0,0))
    out
}

# Roofing filter 2013 John F. Ehlers
roofing.filter <- function(x) {
    # Highpass filter cyclic components whose periods are shorter than 48 bars
    alpha1 = (cos((0.707*360 / 48) * pi / 180.0 ) + sin((0.707*360 / 48) * pi / 180.0 ) - 1) / cos((0.707*360 / 48) * pi / 180.0 )

    x = (1 - alpha1 / 2)*(1 - alpha1 / 2)*( x - 2*mlag(x) + mlag(x,2))
        x[1] = x[2] = x[3]

    HP = x * NA
    HP[] = filter(x, c(2*(1 - alpha1), - (1 - alpha1)*(1 - alpha1)), method='recursive', init=c(0,0))

    super.smoother.filter(HP)
}

# My Stochastic Indicator 2013 John F. Ehlers
roofing.stochastic.indicator  <- function(x, lookback = 20) {
    Filt = roofing.filter(x)

    HighestC = runMax(Filt, lookback)
        HighestC[1:lookback] = as.double(HighestC[lookback])
    LowestC = runMin(Filt, lookback)
        LowestC[1:lookback] = as.double(LowestC[lookback])
    Stoc = (Filt - LowestC) / (HighestC - LowestC)

    super.smoother.filter(Stoc)
}

```

首先，让我们绘制 John 的随机振荡器与传统振荡器的对比图。

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

    tickers = spl('DG')
    data = new.env()
    getSymbols(tickers, src = 'yahoo', from = '1970-01-01', env = data, auto.assign = T)   
        for(i in ls(data)) data[[i]] = adjustOHLC(data[[i]], use.Adjusted=T)
    bt.prep(data)

    #*****************************************************************
    # Setup
    #*****************************************************************
    prices = data$prices  

    models = list()

    # John Ehlers Stochastic
    stoch = roofing.stochastic.indicator(prices)

    # 14 Day Stochastic
    stoch14 = bt.apply(data, function(x) stoch(HLC(x),14)[,'slowD'])

    #*****************************************************************
    # Create plots
    #******************************************************************           
    dates = '2011:10::2012:9'

    layout(1:3)

    plota(prices[dates], type='l', plotX=F)
    plota.legend('DG')

    plota(stoch[dates], type='l', plotX=F)
        abline(h = 0.2, col='red')
        abline(h = 0.8, col='red')
    plota.legend('John Ehlers Stochastic')

    plota(stoch14[dates], type='l')
        abline(h = 0.2, col='red')
        abline(h = 0.8, col='red')
    plota.legend('Stochastic')

```

![plot1](https://systematicinvestor.wordpress.com/wp-content/uploads/2013/07/plot11.jpg)

接下来，让我们编写如图 6 和 8 所示的交易规则，这些规则来自于[John Ehlers 论文：有效的交易策略的预测指标](http://www.stockspotter.com/files/PredictiveIndicators.pdf)。

```

    #*****************************************************************
    # Code Strategies
    #*****************************************************************
    # Figure 6: Conventional Wisdom is to Buy When the Indicator Crosses Above 20% and 
    # To Sell Short when the Indicator Crosses below 80%
    data$weight[] = NA
        data$weight[] = iif(cross.up(stoch, 0.2), 1, iif(cross.dn(stoch, 0.8), -1, NA))
    models$post = bt.run.share(data, clean.signal=T, trade.summary=T)

    data$weight[] = NA
        data$weight[] = iif(cross.up(stoch, 0.2), 1, iif(cross.dn(stoch, 0.8), 0, NA))
    models$post.L = bt.run.share(data, clean.signal=T, trade.summary=T)

    data$weight[] = NA
        data$weight[] = iif(cross.up(stoch, 0.2), 0, iif(cross.dn(stoch, 0.8), -1, NA))
    models$post.S = bt.run.share(data, clean.signal=T, trade.summary=T)

    # Figure 8: Predictive Indicators Enable You to Buy When the Indicator Crosses Below 20% and 
    # To Sell Short when the Indicator Crosses Above 80%
    data$weight[] = NA
        data$weight[] = iif(cross.dn(stoch, 0.2), 1, iif(cross.up(stoch, 0.8), -1, NA))
    models$pre = bt.run.share(data, clean.signal=T, trade.summary=T)

    data$weight[] = NA
        data$weight[] = iif(cross.dn(stoch, 0.2), 1, iif(cross.up(stoch, 0.8), 0, NA))
    models$pre.L = bt.run.share(data, clean.signal=T, trade.summary=T)

    data$weight[] = NA
        data$weight[] = iif(cross.dn(stoch, 0.2), 0, iif(cross.up(stoch, 0.8), -1, NA))
    models$pre.S = bt.run.share(data, clean.signal=T, trade.summary=T)

    #*****************************************************************
    # Create Report
    #****************************************************************** 		    
    strategy.performance.snapshoot(models, T)

```

![plot2](https://systematicinvestor.wordpress.com/wp-content/uploads/2013/07/plot21.jpg)

看起来大部分利润都来自于多头。

最后，让我们可视化这些策略的信号时机：

```

john.ehlers.custom.strategy.plot <- function(data, models, name, 
	main = name,
	dates = '::',
	layout = NULL		# flag to indicate if layout is already set	
) {
    # John Ehlers Stochastic
    stoch = roofing.stochastic.indicator(data$prices)

    # highlight logic based on weight
    weight = models[[name]]$weight[dates]
    	col = iif(weight > 0, 'green', iif(weight < 0, 'red', 'white'))
    plota.control$col.x.highlight = col.add.alpha(col, 100)
    	highlight = T

    if(is.null(layout)) layout(1:2)

    plota(data$prices[dates], type='l', x.highlight = highlight, plotX = F, main=main)
    plota.legend('Long,Short,Not Invested','green,red,white')

    plota(stoch[dates], type='l', x.highlight = highlight, plotX = F, ylim=c(0,1))        	
       	col = col.add.alpha('red', 100)
        abline(h = 0.2, col=col, lwd=3)
        abline(h = 0.8, col=col, lwd=3)
    plota.legend('John Ehlers Stochastic')        
}

    layout(1:4, heights=c(2,1,2,1))

    john.ehlers.custom.strategy.plot(data, models, 'post.L', dates = '2013::', layout=T,
        main = 'post.L: Buy When the Indicator Crosses Above 20% and Sell when the Indicator Crosses Below 80%')

    john.ehlers.custom.strategy.plot(data, models, 'pre.L', dates = '2013::', layout=T,
	main = 'pre.L: Buy When the Indicator Crosses Below 20% and Sell when the Indicator Crosses Above 80%')

```

![plot3](https://systematicinvestor.wordpress.com/wp-content/uploads/2013/07/plot31.jpg)

作为一种作业，我鼓励你们比较使用 John 的随机振荡器与传统振荡器进行交易。

要查看此示例的完整源代码，请查看[github 上的 john.ehlers.filter.test()函数](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
