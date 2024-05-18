<!--yml
category: 未分类
date: 2024-05-18 14:45:59
-->

# Periodic Table of Investment Returns | Systematic Investor

> 来源：[https://systematicinvestor.wordpress.com/2011/11/17/periodic-table-of-investment-returns/#0001-01-01](https://systematicinvestor.wordpress.com/2011/11/17/periodic-table-of-investment-returns/#0001-01-01)

To get a better sense of historical data, I like to examine a Periodic Table of Investment Returns. For an example of a Periodic Table, have a look at the [Single Country Index Returns Periodic Table for 2001-2010](http://us.ishares.com/content/stream.jsp?url=/content/en_us/repository/resource/single_country_periodic_table.pdf&mimeType=application/pdf) published by iShares.

I can easily create a similar table with the following R code, using the historical data from the [Black-Litterman Model](https://systematicinvestor.wordpress.com/2011/11/16/black-litterman-model/) post.

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

[![](img/8b666ceb31ba8cac703aa56e537d4d20.png "plot1.png.small")](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/11/plot1-small6.png)

The Canadian and Australian markets outperformed US and Japanese markets in most years.

Here is a slightly different version of Periodic table:

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

[![](img/8cc9ee063e3e3015abfc6ff42118aa6c.png "plot2.png.small")](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/11/plot2-small5.png)

To view the complete source code for this example, please have a look at the [aa.periodic.table.test() function in aa.test.r at github](https://github.com/systematicinvestor/SIT/blob/master/R/aa.test.r).