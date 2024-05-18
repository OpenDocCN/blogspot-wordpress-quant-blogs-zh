<!--yml
category: 未分类
date: 2024-05-18 14:30:27
-->

# Capturing Intraday data, Backup plan | Systematic Investor

> 来源：[https://systematicinvestor.wordpress.com/2014/04/01/capturing-intraday-data-backup-plan/#0001-01-01](https://systematicinvestor.wordpress.com/2014/04/01/capturing-intraday-data-backup-plan/#0001-01-01)

[Home](https://systematicinvestor.wordpress.com/ "Go to homepage")

>

[R](https://systematicinvestor.wordpress.com/category/r/)

> Capturing Intraday data, Backup plan

## Capturing Intraday data, Backup plan

In the [Capturing Intraday data](https://systematicinvestor.wordpress.com/2014/03/11/capturing-intraday-data/) post, I outlined steps to setup your own process to capture Intraday data. But what do you do if you missed some data points due for example internet being down or due to power outage your server was re-started. To fill up the gaps in the Intraday data, you could get up to 10 day historical Intraday data from Google finance.

I created a wrapper function for Google finance, [getSymbol.intraday.google() function in data.r at github](https://github.com/systematicinvestor/SIT/blob/master/R/data.r), to download historical Intrday quotes. For example,

```

##############################################################################
# Load Systematic Investor Toolbox (SIT)
# https://systematicinvestor.wordpress.com/systematic-investor-toolbox/
###############################################################################
setInternet2(TRUE)
con = gzcon(url('http://www.systematicportfolio.com/sit.gz', 'rb'))
    source(con)
close(con)

    #*****************************************************************
    # Load Intraday data
    #****************************************************************** 
	data = getSymbol.intraday.google('GOOG', 'NASDAQ', 60, '5d')
	last(data, 10)
	plota(data, type='candle', main='Google Intraday prices')

```

```

> last(data, 10)
                       Open    High     Low    Close Volume
2014-03-28 15:52:00 1119.10 1119.61 1119.10 1119.610   4431
2014-03-28 15:53:00 1119.30 1119.30 1118.75 1118.805   3954
2014-03-28 15:54:00 1119.31 1119.45 1119.18 1119.340   5702
2014-03-28 15:55:00 1119.17 1119.40 1119.00 1119.340   8907
2014-03-28 15:56:00 1119.19 1119.35 1119.18 1119.190  11882
2014-03-28 15:57:00 1119.30 1119.30 1119.02 1119.270   6298
2014-03-28 15:58:00 1119.25 1119.35 1119.15 1119.265  10542
2014-03-28 15:59:00 1119.38 1119.49 1118.82 1119.250  29496
2014-03-28 16:00:00 1120.15 1120.15 1119.15 1119.380  71518
2014-03-28 16:01:00 1120.15 1120.15 1120.15 1120.150      0

```

[![plot1](img/eb7622b8525a9f3ff231455a64f2598e.png)](https://systematicinvestor.wordpress.com/wp-content/uploads/2014/03/plot12.png)

So if your Intraday capture process failed, you can rely on Google fiance data to fill up the gaps.