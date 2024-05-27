<!--yml

分类：未分类

日期：2024-05-18 14:36:16

-->

# 体制检测 | 系统投资者

> 来源：[`systematicinvestor.wordpress.com/2012/11/01/regime-detection/#0001-01-01`](https://systematicinvestor.wordpress.com/2012/11/01/regime-detection/#0001-01-01)

体制检测在你试图决定部署哪种策略时非常有用。例如，有些时期（体制）趋势跟踪策略表现得更好，而有些时期均值回归策略表现得更好。今天我想向你展示一种检测市场体制的方法。

为了检测市场体制，我将在模拟数据集（即牛市/熊市环境）上拟合一个隐马尔可夫体制切换模型。我将使用[Markov Regime Switching Models in MATLAB](http://blogs.mathworks.com/pick/2011/02/25/markov-regime-switching-models-in-matlab/)帖子中的优秀示例并将其适应到 R 中。

使用体制切换模型识别市场状态背后的想法是，市场回报可能已经被抽取自 2 个或更多不同的分布。作为一个基本案例，例如，我们可能假设市场回报是来自一个正态分布 N(mu, sigma)的样本，即。

```

Returns = mu + e, e ~ N(0, sigma)

```

接下来我们可能假设市场回报来自两个正态分布（即牛市期间的回报可能~ N(mu.Bull, sigma.Bull)和熊市期间的回报可能是 N(mu.Bear, sigma.Bear)即。

```

Returns = mu + e, e ~ N(0, sigma) 
mu = mu.Bull for Bull regime and mu.Bear for Bear regime and
sigma= sigma.Bull for Bull regime and sigma.Bear for Bear regime

```

幸运的是，我们不必手动拟合体制，CRAN 上有[RHmm 包用于隐马尔可夫模型](http://r-forge.r-project.org/projects/rhmm/)，它使用 Baum-Welch 算法来拟合隐马尔可夫模型。

接下来，遵循[Markov Regime Switching Models in MATLAB](http://blogs.mathworks.com/pick/2011/02/25/markov-regime-switching-models-in-matlab/)帖子中的步骤。

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
	# Generate data as in the post
	#****************************************************************** 
	bull1 = rnorm( 100, 0.10, 0.15 )
	bear  = rnorm( 100, -0.01, 0.20 )
	bull2 = rnorm( 100, 0.10, 0.15 )
	true.states = c(rep(1,100),rep(2,100),rep(1,100))
	returns = c( bull1, bear,  bull2 )

	# find regimes
	load.packages('RHmm')

	y=returns
	ResFit = HMMFit(y, nStates=2)
	VitPath = viterbi(ResFit, y)

	#Forward-backward procedure, compute probabilities
	fb = forwardBackward(ResFit, y)

	# Plot probabilities and implied states
	layout(1:2)
	plot(VitPath$states, type='s', main='Implied States', xlab='', ylab='State')

	matplot(fb$Gamma, type='l', main='Smoothed Probabilities', ylab='Probability')
		legend(x='topright', c('State1','State2'),  fill=1:2, bty='n')

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/10/plot1-small4.png)

第一个图表显示了由模型确定的状态（1/2)。第二个图表显示了处于每个状态的概率。

接下来，让我们生成一些附加数据，看看模型是否能够识别体制。

```

	#*****************************************************************
	# Add some data and see if the model is able to identify the regimes
	#****************************************************************** 
	bear2  = rnorm( 100, -0.01, 0.20 )
	bull3 = rnorm( 100, 0.10, 0.10 )
	bear3  = rnorm( 100, -0.01, 0.25 )
	y = c( bull1, bear,  bull2, bear2, bull3, bear3 )
	VitPath = viterbi(ResFit, y)$states

	#*****************************************************************
	# Plot regimes
	#****************************************************************** 
	load.packages('quantmod')
	data = xts(y, as.Date(1:len(y)))

	layout(1:3)
		plota.control$col.x.highlight = col.add.alpha(true.states+1, 150)
	plota(data, type='h', plotX=F, x.highlight=T)
		plota.legend('Returns + True Regimes')
	plota(cumprod(1+data/100), type='l', plotX=F, x.highlight=T)
		plota.legend('Equity + True Regimes')

		plota.control$col.x.highlight = col.add.alpha(VitPath+1, 150)
	plota(data, type='h', x.highlight=T)
		plota.legend('Returns + Detected Regimes')				

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/10/plot2-small4.png)

前 300 个观测值用于校准此模型，接下来的 300 个观测值用于了解模型如何描述新信息。在这个玩具示例中，这个模型表现得相当好。

要查看这个示例的完整源代码，请查看[bt.regime.detection.test()函数在 bt.test.r at github](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
