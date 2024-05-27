<!--yml

分类：未分类

日期：2024 年 05 月 18 日 14:30:27

-->

# 获取实时数据，备份计划 | Systematic Investor

> 来源：[`systematicinvestor.wordpress.com/2014/04/01/capturing-intraday-data-backup-plan/#0001-01-01`](https://systematicinvestor.wordpress.com/2014/04/01/capturing-intraday-data-backup-plan/#0001-01-01)

[首页](https://systematicinvestor.wordpress.com/ "转到首页")

[R](https://systematicinvestor.wordpress.com/category/r/)

> 获取实时数据，备份计划

## 获取实时数据，备份计划

在 [获取实时数据](https://systematicinvestor.wordpress.com/2014/03/11/capturing-intraday-data/) 文章中，我概述了建立自己的流程来捕获实时数据的步骤。但是如果由于例如网络中断或由于停电导致服务器重新启动而导致错过了一些数据点，你该怎么办呢？为填补实时数据中的空白，你可以从 Google Finance 获取多达 10 天的历史实时数据。

我创建了一个 Google Finance 的包装函数，[getSymbol.intraday.google() 函数在 data.r 上的 github](https://github.com/systematicinvestor/SIT/blob/master/R/data.r)，用于下载历史实时报价。例如，

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

![plot1](https://systematicinvestor.wordpress.com/wp-content/uploads/2014/03/plot12.png)

所以，如果你的实时捕获过程失败了，你可以依靠 Google Finance 的数据来填补这些空白。
