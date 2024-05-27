<!--yml

分类：未分类

日期：2024-05-18 14:37:06

-->

# 周末阅读 - 十月的黄金 | Systematic Investor

> 来源：[`systematicinvestor.wordpress.com/2012/09/29/weekend-reading-gold-in-october/#0001-01-01`](https://systematicinvestor.wordpress.com/2012/09/29/weekend-reading-gold-in-october/#0001-01-01)

[首页](https://systematicinvestor.wordpress.com/ "前往首页")

[R](https://systematicinvestor.wordpress.com/category/r/)

> 周末阅读 - 十月的黄金

## 周末阅读 - 十月的黄金

我最近看到了马克·哈尔伯特（Mark Hulbert）的 [“金交易者的早期万圣节”](http://www.marketwatch.com/story/an-early-halloween-for-gold-traders-2012-09-26) 文章。今年我在 [R/Finance](https://systematicinvestor.wordpress.com/2012/05/15/rfinance-2012-presentation/) 上讨论了这种季节性分析。

使用 [Systematic Investor Toolbox](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/) 进行季节性分析非常容易。

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
    ticker = 'GLD'

    data = getSymbols(ticker, src = 'yahoo', from = '1970-01-01', auto.assign = F)
        data = adjustOHLC(data, use.Adjusted=T)

    #*****************************************************************
    # Look at the Month of the Year Seasonality
    #****************************************************************** 
    month.year.seasonality(data, ticker)

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/09/plot1-small3.png)

这证实了十月对黄金来说历史上是糟糕的，但我们只使用了 8 年的历史数据，因为 GLD 只在 2004 年开始交易。

为了得到更全面的图片，德国联邦银行有很长时间的黄金价格历史数据。我发现这个数据源在 [Wikiposit](http://wikiposit.org/w?filter=Finance/Commodities/) 中使用。

我创建了一个辅助函数，用于从 [GitHub 的 data.r](https://github.com/systematicinvestor/SIT/blob/master/R/data.r) 下载 [德国联邦银行](http://www.bundesbank.de/Navigation/EN/Statistics/Time_series_databases/Macro_economic_time_series/its_list_node.html?listId=www_s331_b01015_3) 网站的价格。

```

    #*****************************************************************
    # Load long series of gold prices from Bundes Bank
    #****************************************************************** 
    data = bundes.bank.data.gold()

    #*****************************************************************
    # Look at the Month of the Year Seasonality
    #****************************************************************** 
    month.year.seasonality(data, 'GOLD', lookback.len = nrow(data))

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/09/plot2-small2.png)

对于使用较长时间序列的黄金来说，十月历史上也是糟糕的。

接下来，我建议查看十月黄金的每日表现，以获得更清晰的图片。您可能希望使用 [Seasonality Tool](http://www.systematicportfolio.com/tools) 进行此目的。请阅读关于如何使用 [Seasonality Tool](http://www.systematicportfolio.com/tools) 的案例研究，以获取关于 [Historical Seasonality Analysis: What company in DOW 30 is likely to do well in January?](https://systematicinvestor.wordpress.com/2011/12/30/historical-seasonality-analysis-what-company-in-dow-30-is-likely-to-do-well-in-january/) 的帖子。

要查看此示例的完整源代码，请查看 [GitHub 的 bt.test.r 中的 bt.october.gold.test() 函数](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
