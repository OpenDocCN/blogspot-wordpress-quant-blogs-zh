<!--yml

类别: 未分类

日期: 2024-05-18 14:35:39

-->

# 金融动荡实例 | Systematic Investor

> 来源：[`systematicinvestor.wordpress.com/2012/12/01/financial-turbulence-example/#0001-01-01`](https://systematicinvestor.wordpress.com/2012/12/01/financial-turbulence-example/#0001-01-01)

今天，我想要介绍由 Mark Kritzman 和 Yuanzhen Li 在[Skulls, Financial Turbulence, and Risk Management](http://www.cfapubs.org/doi/abs/10.2469/faj.v66.n5.3)论文中介绍的金融动荡指数概念。[Timely Portfolio](http://timelyportfolio.blogspot.ca)发布了一系列关于金融动荡的帖子：[第一部分](http://timelyportfolio.blogspot.ca/2011/04/great-faj-article-on-statistical.html)，[第二部分](http://timelyportfolio.blogspot.ca/2011/04/great-faj-article-on-statistical_26.html)，[第三部分](http://timelyportfolio.blogspot.ca/2011/04/great-faj-article-on-statistical_6197.html)。

例如，我将计算[G10 货币](http://www.invescopowershares.com/products/overview.aspx?ticker=DBV)的等权重指数的金融动荡指数。首先，我创建了一个助手函数[github 上的 get.G10()函数数据](https://github.com/systematicinvestor/SIT/blob/master/R/data.r)来从[FRED](http://research.stlouisfed.org/fred2/)下载 G10 货币的历史数据。

```

get.G10 <- function() {
	# FRED acronyms for daily FX rates
map = '
FX          FX.NAME        
DEXUSAL     U.S./Australia 
DEXUSUK     U.S./U.K.      
DEXCAUS     Canada/U.S.    
DEXNOUS     Norway/U.S.    
DEXUSEU     U.S./Euro      
DEXJPUS     Japan/U.S.     
DEXUSNZ     U.S./NewZealand
DEXSDUS     Sweden/U.S.    
DEXSZUS     Switzerland/U.S.
'

	map = matrix(scan(text = map, what='', quiet=T), nc=2, byrow=T)
		colnames(map) = map[1,]
		map = data.frame(map[-1,], stringsAsFactors=F)

	# convert all quotes to be vs U.S.
	convert.index = grep('DEXUS',map$FX, value=T)	

	#*****************************************************************
	# Load historical data
	#****************************************************************** 
	load.packages('quantmod')

	# load fx from fred
	data.fx <- new.env()
	getSymbols(map$FX, src = 'FRED', from = '1970-01-01', env = data.fx, auto.assign = T)		
		for(i in convert.index) data.fx[[i]] = 1 / data.fx[[i]]

	# extract fx where all currencies are available
	bt.prep(data.fx, align='remove.na')
	fx = bt.apply(data.fx, '[')

	return(fx)
}

```

接下来，让我们计算 G10 货币的金融动荡指数。

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

	fx = get.G10()
		nperiods = nrow(fx)

	#*****************************************************************
	# Rolling estimate of the Financial Turbulence for G10 Currencies
	#****************************************************************** 
	turbulence = fx[,1] * NA
	ret = coredata(fx / mlag(fx) - 1)

	look.back = 252

	for( i in (look.back+1) : nperiods ) {
		temp = ret[(i - look.back + 1):(i-1), ]

		# measures turbulence for the current observation
		turbulence[i] = mahalanobis(ret[i,], colMeans(temp), cov(temp))

		if( i %% 200 == 0) cat(i, 'out of', nperiods, '\n')
	}	

	#*****************************************************************
	# Plot 30 day average of the Financial Turbulence for G10 Currencies
	#****************************************************************** 	
	plota(EMA( turbulence, 30), type='l', 
		main='30 day average of the Financial Turbulence for G10 Currencies')

```

![plot1](https://systematicinvestor.wordpress.com/2012/12/01/financial-turbulence-example/plot1-5/)

在 2008-2009 年期间，该指数出现了大幅上升。如果在这些时期监控金融动荡指数并在这些时期减少或对冲头寸，你将能够减少亏损并晚上睡得更安稳。

要查看此示例的完整源代码，请参考[github 上 bt.financial.turbulence.test()函数的 bt.test.r](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
