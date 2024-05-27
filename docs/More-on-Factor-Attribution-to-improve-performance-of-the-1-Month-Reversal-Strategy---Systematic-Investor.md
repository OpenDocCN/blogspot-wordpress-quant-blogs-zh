<!--yml

分类：未分类

日期：2024-05-18 14:39:09

-->

# 更多关于因子归因以提高 1 个月反转策略的性能 | 系统投资者

> 来源：[`systematicinvestor.wordpress.com/2012/07/27/more-on-factor-attribution-to-improve-performance-of-the-1-month-reversal-strategy/#0001-01-01`](https://systematicinvestor.wordpress.com/2012/07/27/more-on-factor-attribution-to-improve-performance-of-the-1-month-reversal-strategy/#0001-01-01)

在我的上篇文章[因子归因以提高 1 个月反转策略的性能](https://systematicinvestor.wordpress.com/2012/07/17/factor-attribution-to-improve-performance-of-the-1-month-reversal-strategy/)中，我讨论了如何使用[因子归因](https://systematicinvestor.wordpress.com/2012/07/04/example-of-factor-attribution/)来提高[1 个月反转策略](https://systematicinvestor.wordpress.com/2012/07/13/1-month-reversal-strategy/)的性能。今天我想更深入地研究这个策略，并针对每个部门进行研究，同时进行部门中性的回测。

加载历史价格、加载 Fama/French 因子和运行因子归因的初始步骤与原始[文章](https://systematicinvestor.wordpress.com/2012/07/17/factor-attribution-to-improve-performance-of-the-1-month-reversal-strategy/)相同，所以我这里不再重复。这个示例的完整源代码位于[github 上的 bt.fa.sector.one.month.test()函数中](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)供您参考。创建部门和部门中性的回测的新功能位于下面的 bt.make.quintiles.sector()函数中：

```

bt.make.quintiles.sector <- function(
	sector,		# sector data
	position.score,	# position.score is a factor to form Quintiles sampled at the period.ends
	data,		# back-test object
	period.ends,	
	n.quantiles = 5,
	start.t = 2,	# first index at which to form Quintiles
	prefix = ''	
) 
{
	#*****************************************************************
	# Re-organize sectors into matrix, assume that sectors are constant in time
	#****************************************************************** 
	temp = factor(sector)
	sector.names = levels(temp)	
		n.sectors = len(sector.names)
	sectors = matrix(unclass(temp), nr=nrow(position.score), nc=ncol(position.score), byrow=T)

	#*****************************************************************
	# Create Quantiles
	#****************************************************************** 
	position.score = coredata(position.score)
	quantiles = weights = position.score * NA			

	for( s in 1:n.sectors) {
		for( t in start.t:nrow(weights) ) {
			index = sectors[t,] == s
			n = sum(index)

			# require at least 3 companies in each quantile
			if(n > 3*n.quantiles) {			
				factor = as.vector(position.score[t, index])
				ranking = ceiling(n.quantiles * rank(factor, na.last = 'keep','first') / count(factor))

				quantiles[t, index] = ranking
				weights[t, index] = 1/tapply(rep(1,n), ranking, sum)[ranking]			
			}
		}
	}
	quantiles = ifna(quantiles,0)

	#*****************************************************************
	# Create Q1-QN spread for each Sector
	#****************************************************************** 
	long = weights * NA
	short = weights * NA
	models = list()

	for( s in 1:n.sectors) {
		long[] = 0
		long[quantiles == 1 & sectors == s] = weights[quantiles == 1 & sectors == s]
		long = long / rowSums(long,na.rm=T)

		short[] = 0
		short[quantiles == n.quantiles & sectors == s] = weights[quantiles == n.quantiles & sectors == s]
		short = short / rowSums(short,na.rm=T)

		data$weight[] = NA
			data$weight[period.ends,] = long - short
		models[[ paste(prefix,'spread.',sector.names[s], sep='') ]]	= bt.run(data, silent = T)	
	}

	#*****************************************************************
	# Create Sector - Neutral Q1-QN spread
	#****************************************************************** 		
	long[] = 0
	long[quantiles == 1] = weights[quantiles == 1]
	long = long / rowSums(long,na.rm=T)

	short[] = 0
	short[quantiles == n.quantiles] = weights[quantiles == n.quantiles]
	short = short / rowSums(short,na.rm=T)

	data$weight[] = NA
		data$weight[period.ends,] = long - short
	models$spread.sn = bt.run(data, silent = T)	

	return(models)
}

```

下面我进行了比较，基于 1 个月回报（one.month）和因子归因回归的残差（last.e_s）的总体策略和部门中性的版本。在所有情况下，残差策略的表现优于基础策略，而且部门中性的版本相比总体策略具有更好的风险调整系数。

![plot1.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/07/plot1-small3.png)

![plot2.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/07/plot2-small3.png)

在研究了两种策略的每个部门的表现后，我惊讶地发现，在两种情况下能源、材料和公用事业的表现都低于平均水平，而金融和消费品在两种情况下表现都非常出色。查看部门回测图表，我认为选择每月前几个部门的动量策略会做得很好。你可以尝试将这个想法作为家庭作业来实现。

![plot3.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/07/plot3-small1.png)

![plot4.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/07/plot4-small1.png)

要查看这个示例的完整源代码，请查看[bt.fa.sector.one.month.test()函数在 github 上的 bt.test.r](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
