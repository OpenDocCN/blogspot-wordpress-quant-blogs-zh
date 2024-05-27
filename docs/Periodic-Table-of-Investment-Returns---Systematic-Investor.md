-

分类：未分类

日期：2024-05-18 14:45:59

-

# 投资回报周期表 | 系统投资者

> 来源：[`systematicinvestor.wordpress.com/2011/11/17/periodic-table-of-investment-returns/#0001-01-01`](https://systematicinvestor.wordpress.com/2011/11/17/periodic-table-of-investment-returns/#0001-01-01)

为了更好地了解历史数据，我喜欢查看投资回报周期表。作为一个周期表的例子，请查看 iShares 发布的[2001-2010 年单一国家指数回报周期表](http://us.ishares.com/content/stream.jsp?url=/content/en_us/repository/resource/single_country_periodic_table.pdf&mimeType=application/pdf)。

我可以用以下 R 代码轻松地创建一个类似的表格，使用来自[Black-Litterman 模型](https://systematicinvestor.wordpress.com/2011/11/16/black-litterman-model/)文章的历史数据。

```

# load Systematic Investor Toolbox
setInternet2(TRUE)
source(gzcon(url('https://github.com/systematicinvestor/SIT/raw/master/sit.gz', 'rb')))

	#--------------------------------------------------------------------------
	# Get Historical Data
	#--------------------------------------------------------------------------
	# Country's IA are based on monthly data
	ia = aa.test.create.ia.country()
		hist.returns = ia$hist.returns

	# convert returns to prices
	hist.prices = cumprod(1 + hist.returns)

	# extract annual prices
	period.ends = endpoints(hist.prices, 'years')
		hist.prices = hist.prices[period.ends, ]

	# compute simple returns
	hist.returns = na.omit( ROC(hist.prices, type = 'discrete') )
		hist.returns = hist.returns['2000::2010']

	#--------------------------------------------------------------------------
	# Create Periodic table
	#--------------------------------------------------------------------------
	# create temp matrix with data you want to plot
	temp = t(coredata(hist.returns))
		colnames(temp) = format(index(hist.returns), '%Y')
		rownames(temp) = 1:ia$n
			rownames(temp)[1] = ' Best '
			rownames(temp)[ia$n] = ' Worst '

	# highlight each column
	col = plota.colors(ia$n)
	highlight = apply(temp,2, function(x) col[order(x, decreasing = T)] )

	# sort each column
	temp[] = apply(temp,2, sort, decreasing = T)

	# format data as percentages
	temp[] = plota.format(100 * temp, 0, '', '%')	

	# plot temp and legend
	plot.table(temp, highlight = highlight)			
	plota.legend(ia$symbols,col,cex=1.5)

```

![元素周期表](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/11/plot1-small6.png)

加拿大和澳大利亚市场在大多数年份的表现优于美国和日本市场。

这里是一个稍微不同版本的元素周期表：

```

	#--------------------------------------------------------------------------
	# Create Periodic table, another version
	#--------------------------------------------------------------------------
	# create temp matrix with data you want to plot
	temp = t(coredata(hist.returns))
		colnames(temp) = format(index(hist.returns), '%Y')

	# format data as percentages
	temp[] = plota.format(100 * temp, 0, '', '%')

	# highlight each column separately
	highlight = apply(temp,2, function(x) plot.table.helper.color(t(x)) )

	# plot temp with colorbar
	plot.table(temp, highlight = highlight, colorbar = TRUE)

```

![投资回报周期表](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/11/plot2-small5.png)

要查看这个例子的完整源代码，请查看 GitHub 上的[aa.periodic.table.test()函数](https://github.com/systematicinvestor/SIT/blob/master/R/aa.test.r)。
