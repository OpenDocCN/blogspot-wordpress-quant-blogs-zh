<!--yml

类别：未分类

日期：2024-05-18 14:33:57

-->

# 集群投资组合配置 | 系统化投资者

> 来源：[`systematicinvestor.wordpress.com/2013/02/12/cluster-portfolio-allocation/#0001-01-01`](https://systematicinvestor.wordpress.com/2013/02/12/cluster-portfolio-allocation/#0001-01-01)

今天，我想继续讨论聚类主题，并展示在集群投资组合配置方法中如何确定投资组合权重。 集群投资组合配置方法的一个例子是[集群风险平价](http://cssanalytics.wordpress.com/)（Varadi，Kapler，2012）。

集群投资组合配置方法有 3 个步骤：

+   创建集群

+   在每个集群内分配资金

+   在所有集群中分配资金

我将使用“等权重”和“风险平价”投资组合配置方法分别说明以下所有 3 个步骤。 让我们从加载 10 个主要资产类别的历史价格开始。

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
	# Load historical data for ETFs
	#****************************************************************** 
	load.packages('quantmod')

	tickers = spl('GLD,UUP,SPY,QQQ,IWM,EEM,EFA,IYR,USO,TLT')

	data <- new.env()
	getSymbols(tickers, src = 'yahoo', from = '1900-01-01', env = data, auto.assign = T)
		for(i in ls(data)) data[[i]] = adjustOHLC(data[[i]], use.Adjusted=T)

	bt.prep(data, align='remove.na')

	#*****************************************************************
	# Setup
	#****************************************************************** 
	# compute returns
	ret = data$prices / mlag(data$prices) - 1

	# setup period
	dates = '2012::2012'
	ret = ret[dates]

```

接下来，让我们计算“普通”投资组合配置（即无集群）

```

	fn.name = 'equal.weight.portfolio'				
	fn = match.fun(fn.name)

	# create input assumptions
	ia = create.historical.ia(ret, 252) 

	# compute allocation without cluster, for comparison
	weight = fn(ia)

```

接下来，让我们创建集群并计算每个集群内的投资组合配置

```

	# create clusters
	group = cluster.group.kmeans.90(ia)
	ngroups = max(group)

	weight0 = rep(NA, ia$n)

	# store returns for each cluster
	hist.g = NA * ia$hist.returns[,1:ngroups]

	# compute weights within each group	
	for(g in 1:ngroups) {
		if( sum(group == g) == 1 ) {
			weight0[group == g] = 1
			hist.g[,g] = ia$hist.returns[, group == g, drop=F]
		} else {
			# create input assumptions for the assets in this cluster
			ia.temp = create.historical.ia(ia$hist.returns[, group == g, drop=F], 252) 

			# compute allocation within cluster
			w0 = fn(ia.temp)

			# set appropriate weights
			weight0[group == g] = w0

			# compute historical returns for this cluster
			hist.g[,g] = ia.temp$hist.returns %*% w0
		}
	}

```

接下来，让我们计算跨所有集群的投资组合配置，并计算最终的投资组合权重。

```

	# create GROUP input assumptions
	ia.g = create.historical.ia(hist.g, 252) 

	# compute allocation across clusters
	group.weights = fn(ia.g)

	# mutliply out group.weights by within group weights
	for(g in 1:ngroups)
		weight0[group == g] = weight0[group == g] * group.weights[g]

```

最后，让我们创建报告并比较投资组合配置。

```

	#*****************************************************************
	# Create Report
	#****************************************************************** 			
	load.packages('RColorBrewer')
	col = colorRampPalette(brewer.pal(9,'Set1'))(ia$n)

	layout(matrix(1:2,nr=2,nc=1))
	par(mar = c(0,0,2,0))
	index = order(group)

	pie(weight[index], labels = paste(colnames(ret), round(100*weight,1),'%')[index], col=col, main=fn.name)

	pie(weight0[index], labels = paste(colnames(ret), round(100*weight0,1),'%')[index], col=col, main=paste('Cluster',fn.name))	

```

![equal.weight.portfolio.plot.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2013/02/equal-weight-portfolio-plot-small.png)

最大的区别在于“等权重”投资组合配置方法中最为明显。 集群版本首先将 25％分配给每个集群，然后在每个集群内均匀分配。 普通版本在所有资产之间均匀分配。 下面的“风险平价”版本工作方式类似，但是不是平等的权重，而是侧重于风险均等分配。 例如，UUP 获得了更大的分配，因为它的风险远低于其他任何资产。

![risk.parity.portfolio.plot.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2013/02/risk-parity-portfolio-plot-small.png)

下周，我将展示如何对集群投资组合配置方法进行回测。

要查看此示例的完整源代码，请查看[github 上的 bt.test.r 中的 bt.cluster.portfolio.allocation.test()函数](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
