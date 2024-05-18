<!--yml
category: 未分类
date: 2024-05-18 14:40:31
-->

# Backtesting Classical Technical Patterns | Systematic Investor

> 来源：[https://systematicinvestor.wordpress.com/2012/05/29/backtesting-classical-technical-patterns/#0001-01-01](https://systematicinvestor.wordpress.com/2012/05/29/backtesting-classical-technical-patterns/#0001-01-01)

In the last post, [Classical Technical Patterns](https://systematicinvestor.wordpress.com/2012/05/22/classical-technical-patterns/), I discussed the algorithm and pattern definitions presented in the [Foundations of Technical Analysis by A. Lo, H. Mamaysky, J. Wang (2000)](http://web.mit.edu/alo/www/Papers/1705-1765.pdf) paper. Today, I want to check how different patterns performed historically using SPY.

I will follow the rolling window procedure discussed on pages 14-15 of the [paper](http://web.mit.edu/alo/www/Papers/1705-1765.pdf). Let’s begin by loading the historical data for the SPY and running a rolling window pattern search algorithm.

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

There are many patterns that are found multiple times. Let’s remove the entries that refer to the same pattern and keep only the first occurrence.

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

Now we can visualize the performance of each pattern using the charts from my [presentation](http://www.systematicportfolio.com/RFinance2012) about Seasonality Analysis and Pattern Matching at the [R/Finance](http://www.rinfinance.com/agenda/) conference.

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

[![](img/40911e336bef672ea1112b3067af2efd.png "plot1.png.small")](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/05/plot1-small2.png)

[![](img/7135ed08cb032e1262537ff323c5f044.png "plot2.png.small")](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/05/plot2-small1.png)

[![](img/c3e902541692d1511af5a5830d106424.png "plot3.png.small")](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/05/plot3-small.png)

The Broadening bottoms (BBOT) and Rectangle tops (RTOP) worked historically well for SPY.

To view the complete source code for this example, please have a look at the [bt.patterns.test() function in rfinance2012.r at github](https://github.com/systematicinvestor/SIT/blob/master/R/rfinance2012.r).