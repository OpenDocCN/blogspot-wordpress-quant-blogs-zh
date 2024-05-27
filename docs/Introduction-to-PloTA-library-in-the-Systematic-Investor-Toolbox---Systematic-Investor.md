<!--yml

类别：未分类

日期：2024-05-18 14:38:35

-->

# Systematic Investor Toolbox 中 PloTA 库的介绍 | Systematic Investor

> 来源：[`systematicinvestor.wordpress.com/2011/10/04/introduction-to-plota-library-in-the-systematic-investor-toolbox/#0001-01-01`](https://systematicinvestor.wordpress.com/2011/10/04/introduction-to-plota-library-in-the-systematic-investor-toolbox/#0001-01-01)

PloTA（plot + ta）库在 Systematic Investor Toolbox 中是一个简单的绘图接口，用于绘制时间序列和技术分析图。我创建它是为了替代[quantmod](http://www.quantmod.com/)包中的绘图功能。它设计成模仿默认的绘图接口，并且与[xts](http://cran.r-project.org/web/packages/xts/index.html)对象一起工作。PloTA 实现以下方法：

+   plota – 主要绘图方法

+   plota2Y – 添加第二个 Y 轴到现有绘图

+   plota.lines – 绘制线条

+   plota.candle – 绘制蜡烛图

+   plota.ohlc – 绘制开/高/低/收

+   plota.hl – 绘制高/低

+   plota.volume – 绘制交易量

+   plota.scale.volume – 缩放交易量

+   plota.grid – 添加网格

+   plota.legend – 绘制图例

+   plota.layout – 指定绘图布局

+   plota.theme.blue.red – 颜色主题

+   plota.theme.green.orange – 颜色主题

+   plota.theme.gray.orange – 颜色主题

要开始使用 PloTA，请先加载 Systematic Investor Toolbox：

```

###############################################################################
# Load Systematic Investor Toolbox (SIT)
# https://systematicinvestor.wordpress.com/systematic-investor-toolbox/
###############################################################################
setInternet2(TRUE)
con = gzcon(url('http://www.systematicportfolio.com/sit.gz', 'rb'))
    source(con)
close(con)

```

接下来让我们加载[quantmod](http://www.quantmod.com/)包，并下载 SPY 和 IBM 的价格历史记录：

```

load.packages('quantmod')

# download sample data from Yahoo
data.spy = getSymbols('SPY', from = '1980-01-01', auto.assign = FALSE)
data.ibm = getSymbols('IBM', from = '1980-01-01', auto.assign = FALSE)

```

接下来我将展示几个 PloTA 库的简单用法。

要创建一个简单的 SPY 图表：

```

y = data.spy['2011:01:01::2011:02:01']
highlight = which(Cl(y) < 127)

png(filename = 'plot1.png', width = 500, height = 500, units = 'px', pointsize = 12, bg = 'white')

layout(c(1,1,2))
plota(y, type = 'candle', main = 'SPY', plotX = F, x.highlight = highlight)
	y = plota.scale.volume(y)
plota(y, type = 'volume', x.highlight = highlight)

dev.off()

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/10/plot1.png)

要创建一个带有 RSI 和图例的 SPY 简单图表：

```

y = data.spy['2010:01:01::2011:02:01']

layout(c(1,1,2,3))
plota(y, type = 'candle', plotX = F)
	plota.legend('SPY', 'blue', y)

y = plota.scale.volume(y)
plota(y, type = 'volume', plotX = F)
	plota.legend('Volume', 'blue', Vo(y))

rsi = RSI(Cl(y),2)
plota(rsi, type = 'l', y.highlight = c(c(Inf,80),c(20,-Inf)))
	abline(h = 20, col = 'red')
	abline(h = 80, col = 'red')
	plota.legend('RSI(2)', 'black', rsi)

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/10/plot2.png)

要创建带有第二个 Y 轴的图表：

```

y = data.spy['2010:01:01::2011:02:01']

# to plot second Y axis, free some space on left side
# e.g. set LeftMargin=3
plota(y, type = 'ohlc', LeftMargin=3)

y0 = y;
y = data.ibm['2010:10:15::2011:02:01']
plota2Y(y, ylim = range(OHLC(y)),las=1, col='red', col.axis = 'red')
	plota.ohlc(y, col = 'red')
	plota.legend('SPY(rhs),IBM(lhs)', 'blue,red', list(y0,y))

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/10/plot3.png)

要在同一图中绘制每日和每月：

```

y = data.spy['2010:01:01::2011:02:01']

plota(y, type = 'candle')
	y1 = to.monthly(y)
		index(y1) = as.Date(index(y1))
	plota.ohlc(y1, col = 'pink')
	plota.candle(y)
	plota.legend('Daily,Monthly', 'red,pink')

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/10/plot42.png)

要绘制每日、每周和每月：

```

y = data.spy['2010:01:01::2011']

layout(c(1,2,3))
plota(y, type = 'candle', plotX = F)
	plota.legend('Daily', 'blue', y)

plota(y, ylim = range(OHLC(y)), plotX = F)
	y1 = to.weekly(y)
		index(y1) = as.Date(index(y1))
	plota.candle(y1)
	plota.legend('Weekly', 'blue', y1)

plota(y, ylim = range(OHLC(y)))
	y1 = to.monthly(y)
		index(y1) = as.Date(index(y1))
	plota.candle(y1)
	plota.legend('Monthly', 'blue', y1)

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/10/plot5.png)

我会在未来的文章中展示更多关于 PloTA 的示例。

要查看此示例的完整源代码，请查看[plota.r 中的 plota.test()函数在 github 上](https://github.com/systematicinvestor/SIT/blob/master/R/plota.r)。
