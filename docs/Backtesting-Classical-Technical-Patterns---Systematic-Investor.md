<!--yml

类别：未分类

日期：2024 年 05 月 18 日 14:40:31

-->

# 对经典技术模式进行回测 | Systematic Investor

> 来源：[`systematicinvestor.wordpress.com/2012/05/29/backtesting-classical-technical-patterns/#0001-01-01`](https://systematicinvestor.wordpress.com/2012/05/29/backtesting-classical-technical-patterns/#0001-01-01)

在上一篇文章中，[经典技术模式](https://systematicinvestor.wordpress.com/2012/05/22/classical-technical-patterns/)，我讨论了[《技术分析基础》（2000 年，A. Lo，H. Mamaysky，J. Wang）](http://web.mit.edu/alo/www/Papers/1705-1765.pdf)中提出的算法和模式定义。今天，我想检查不同模式在历史上的表现如何，使用 SPY。

我将按照[论文](http://web.mit.edu/alo/www/Papers/1705-1765.pdf)第 14-15 页讨论的滚动窗口程序进行操作。让我们首先加载 SPY 的历史数据，并运行滚动窗口模式搜索算法。

```

###############################################################################
# Load Systematic Investor Toolbox (SIT)
###############################################################################
con = gzcon(url('http://www.systematicportfolio.com/sit.gz', 'rb'))
    source(con)
close(con)

	#*****************************************************************
	# Load historical data
	#****************************************************************** 
	load.packages('quantmod')
	ticker = 'SPY'

	data = getSymbols(ticker, src = 'yahoo', from = '1970-01-01', auto.assign = F)
		data = adjustOHLC(data, use.Adjusted=T)

	#*****************************************************************
	# Search for all patterns over a rolling window
	#****************************************************************** 
	load.packages('sm') 
	history = as.vector(coredata(Cl(data)))

	window.L = 35
	window.d = 3
	window.len = window.L + window.d

	patterns = pattern.db()

	found.patterns = c()

	for(t in window.len : (len(history)-1)) {
		ret = history[(t+1)]/history[t]-1

		sample = history[(t - window.len + 1):t]		
		obj = find.extrema( sample )	

		if(len(obj$data.extrema.loc) > 0) {
			out =  find.patterns(obj, patterns = patterns, silent=F, plot=F)  

			if(len(out)>0) found.patterns = rbind(found.patterns,cbind(t,out,t-window.len+out, ret))
		}
		if( t %% 10 == 0) cat(t, 'out of', len(history), '\n')
	}
	colnames(found.patterns) = spl('t,start,end,tstart,tend,ret')	

```

有许多模式出现多次。让我们删除指向相同模式的条目，并仅保留第一次出现的条目。

```

	#*****************************************************************
	# Clean found patterns
	#****************************************************************** 	
	# remove patterns that finished after window.L
	found.patterns = found.patterns[found.patterns[,'end'] <= window.L,]

	# remove the patterns found multiple times, only keep first one
	pattern.names = unique(rownames(found.patterns))
	all.patterns = c()
	for(name in pattern.names) {
		index = which(rownames(found.patterns) == name)
		temp = NA * found.patterns[index,]

		i.count = 0
		i.start = 1
		while(i.start < len(index)) {
			i.count = i.count + 1
			temp[i.count,] = found.patterns[index[i.start],]
			subindex = which(found.patterns[index,'tstart'] > temp[i.count,'tend'])			

			if(len(subindex) > 0) {
				i.start = subindex[1]
			} else break		
		} 
		all.patterns = rbind(all.patterns, temp[1:i.count,])		
	}	

```

现在我们可以使用我的 [演示文稿](http://www.systematicportfolio.com/RFinance2012) 中的图表来可视化每个模式的表现，该演示文稿是关于季节性分析和模式匹配的，这是在 [R/Finance](http://www.rinfinance.com/agenda/) 大会上。

```

	#*****************************************************************
	# Plot
	#****************************************************************** 	
	# Frequency for each Pattern
	frequency = tapply(rep(1,nrow(all.patterns)), rownames(all.patterns), sum)
	layout(1)
	barplot.with.labels(frequency/100, 'Frequency for each Pattern')

	# Summary for each Pattern
	all.patterns[,'ret'] = history[(all.patterns[,'t']+20)] / history[all.patterns[,'t']] - 1
	data_list = tapply(all.patterns[,'ret'], rownames(all.patterns), list)
	group.seasonality(data_list, '20 days after Pattern')

	# Details for BBOT pattern
	layout(1)
	name = 'BBOT'
	index = which(rownames(all.patterns) == name)	
	time.seasonality(data, all.patterns[index,'t'], 20, name)	

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/05/plot1-small2.png)

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/05/plot2-small1.png)

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/05/plot3-small.png)

[宽基底（BBOT）和矩形顶部（RTOP）在历史上对 SPY 都表现不错。

要查看此示例的完整源代码，请查看 [github 上的 rfinance2012.r 中的 bt.patterns.test() 函数](https://github.com/systematicinvestor/SIT/blob/master/R/rfinance2012.r)。
