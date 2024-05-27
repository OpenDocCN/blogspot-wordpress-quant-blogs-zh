<!--yml

类别：未分类

日期：2024-05-18 14:48:54

-->

# 使用 plot.table 函数可视化表格 | Systematic Investor

> 来源：[`systematicinvestor.wordpress.com/2011/10/07/visualizing-tables-with-plot-table/#0001-01-01`](https://systematicinvestor.wordpress.com/2011/10/07/visualizing-tables-with-plot-table/#0001-01-01)

Systematic Investor Toolbox 中的 plot.table 函数是一个灵活的表格绘制例程。plot.table 有一个简单的接口，并接受以下参数：

+   plot.matrix – 你要绘制的数据的矩阵

+   smain – 在(顶部，左侧)单元格中绘制的文本；默认值为空字符串

+   highlight – 布尔值，用于表示你是否想根据每个单元格的数值进行着色，或者一个颜色矩阵，为每个单元格提供颜色

+   colorbar – 一个布尔标志，用于表示你是否想要绘制颜色条

以下是一些使用 plot.table 函数创建摘要报告的示例。

首先，让我们加载 Systematic Investor Toolbox：

```

# load Systematic Investor Toolbox
setInternet2(TRUE)
source(gzcon(url('https://github.com/systematicinvestor/SIT/raw/master/sit.gz', 'rb')))

```

创建基本 plot.table 的命令：

```

# define row and column titles
mrownames = spl('row one,row two,row 3')
mcolnames = spl('col 1,col 2,col 3,col 4')

# create temp matrix with data you want to plot
temp = matrix(NA, len(mrownames), len(mcolnames))
	rownames(temp) = mrownames
	colnames(temp) = mcolnames
	temp[,] = matrix(1:12,3,4)

# plot temp, display current date in (top, left) cell
plot.table(temp, format(as.Date(Sys.time()), '%d %b %Y'))

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/10/plot1-small.png)

创建带颜色条的 plot.table 的命令：

```

# generate 1,000 random numbers from Normal(0,1) distribution
data =  matrix(rnorm(1000), nc=10)
	colnames(data) = paste('data', 1:10, sep='')

# compute Pearson correlation of data and format it nicely
temp = compute.cor(data, 'pearson')
	temp[] = plota.format(100 * temp, 0, '', '%')

# plot temp with colorbar, display Correlation in (top, left) cell
plot.table(temp, smain='Correlation', highlight = TRUE, colorbar = TRUE)

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/10/plot2-small.png)

接下来，我想展示一个更实际的 plot.table 函数示例。我想创建一个报告页面，将显示 2010:2011 年 IBM 的图表以及来自[雅虎财经 Key Statistics 网页](http://finance.yahoo.com/q/ks?s=ibm)的估值指标表格。

```

# Load quantmod package to download price history for IBM
load.packages('quantmod')

Symbol = 'IBM'

# download IBM price history from Yahoo
data = getSymbols(Symbol, from = '1980-01-01', auto.assign = FALSE)

# download Key Statistics from yahoo
url = paste('http://finance.yahoo.com/q/ks?s=', Symbol, sep = '')
txt = join(readLines(url))

# extract Valuation Measures table from this page
temp = extract.table.from.webpage(txt, 'Market Cap', hasHeader = F)
	temp = rbind(c('', Symbol), temp)	# add header row

# prepare IBM data for 2010:2011 and compute 50 days moving average
y = data['2010::2011']
sma50 = SMA(Cl(y), 50)

# plote candles and volume and table
layout(c(1,1,2,3,3))

plota(y, type = 'candle', main = Symbol, plotX = F)
	plota.lines(sma50, col='blue')
	plota.legend(c(Symbol,'SMA 50'), 'green,blue', list(y,sma50))

y = plota.scale.volume(y)
plota(y, type = 'volume')

plot.table(temp)

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/10/plot3-small.png)

我将在未来的文章中展示更多关于 plot.table 的例子。

要查看此例的完整源代码，请查看[plot.table.test()函数](https://github.com/systematicinvestor/SIT/blob/master/R/plot.table.r)中的 plot.table.r 文件。
