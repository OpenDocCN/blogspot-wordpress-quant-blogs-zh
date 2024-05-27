<!--yml

category: 未分类

date: 2024-05-18 14:42:01

-->

# 投资组合优化：使用 GNU MathProg 语言指定约束 | 系统投资者

> 来源：[`systematicinvestor.wordpress.com/2012/03/14/portfolio-optimization-specify-constraints-with-gnu-mathprog-language/#0001-01-01`](https://systematicinvestor.wordpress.com/2012/03/14/portfolio-optimization-specify-constraints-with-gnu-mathprog-language/#0001-01-01)

我之前描述了一些投资组合构建的例子：

我创建了许多辅助函数来简化约束的制定（例如，最低/最高投资约束，权重必须总和为 1 的全投资约束等）。

+   new.constraints

+   add.constraints

+   add.variables

然而，即使有了这些函数的帮助，描述约束的过程也不简单且用户友好。幸运的是，有一种使用[GNU MathProg 语言](http://en.wikibooks.org/wiki/GLPK/GMPL_%28MathProg%29)指定线性约束的替代方法。MathProg 类似于 AMPL 的一个子集。要了解更多关于[GNU MathProg 语言](http://en.wikibooks.org/wiki/GLPK/GMPL_%28MathProg%29)的信息，我推荐阅读以下资源：

让我们先用辅助函数来指定约束，解决一个简单的投资组合构建问题。

```

###############################################################################
# Load Systematic Investor Toolbox (SIT)
# https://systematicinvestor.wordpress.com/systematic-investor-toolbox/
###############################################################################
con = gzcon(url('http://www.systematicportfolio.com/sit.gz', 'rb'))
    source(con)
close(con)

	#*****************************************************************
	# Load packages
	#****************************************************************** 
	load.packages('quantmod,quadprog,corpcor')

	#--------------------------------------------------------------------------
	# Create historical input assumptions
	#--------------------------------------------------------------------------
	tickers = dow.jones.components()
	ia = aa.test.create.ia.custom(tickers, dates = '2000::2010')	

	#--------------------------------------------------------------------------
	# Create Constraints & Solve QP problem
	#--------------------------------------------------------------------------
	n = ia$n		

	# 0 <= x.i <= 1 
	constraints = new.constraints(n, lb = 0, ub = 1)

	# SUM x.i = 1
	constraints = add.constraints(rep(1, n), 1, type = '=', constraints)		

	# Solve QP problem
	x = min.var.portfolio(ia, constraints)	

	# plot weights
	barplot(100*x, las=2, main='Minimum Variance Portfolio')

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/03/plot1-small2.png)

现在让我们创建一个 GNU MathProg 语言模型，以施加相同的约束。请将以下模型描述复制并保存在“model1.mod”文件中：

```

###############################################################################
set SYMBOLS ;

# set min/max weights for individual stocks
var weight{i in SYMBOLS} >= 0, <= 1 ;

# objective function, NOT USED
minimize alpha : sum{i in SYMBOLS} weight[i] ;

# weights must sum to 1 (fully invested)
subject to fully_invested : sum{i in SYMBOLS} weight[i] = 1 ;

data;

set SYMBOLS :=  AA AXP BA BAC CAT CSCO CVX DD DIS GE HD HPQ IBM INTC JNJ JPM KFT KO MCD MMM MRK MSFT PFE PG T TRV UTX VZ WMT XOM ;
###############################################################################

```

接下来，让我们使用这个模型来寻找最小方差的投资组合。

```

	#*****************************************************************
	# Load packages
	#****************************************************************** 
	# load Rglpk to read GNU MathProg files
	load.packages('Rglpk')

	#--------------------------------------------------------------------------
	# Read GNU MathProg model/Setup constraints/Solve QP problem
	#--------------------------------------------------------------------------	
	model.file = 'model1.mod'

	# read model
	model = Rglpk.read.model(model.file,type = 'MathProg') 	

	# convert GNU MathProg model to constraint used in solve.QP
	constraints = Rglpk.create.constraints(model)$constraints	

	# Solve QP problem
	x = min.var.portfolio(ia, constraints)	

	# plot weights
	barplot(100*x, las=2, main='Minimum Variance Portfolio using GNU MathProg model')

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/03/plot2-small2.png)

接下来，让我们描述来自[最小投资和资产数量投资组合基数约束](https://systematicinvestor.wordpress.com/2011/10/20/minimum-investment-and-number-of-assets-portfolio-cardinality-constraints/)文章的问题。请将以下模型描述复制并保存在“model2.mod”文件中：

```

###############################################################################
set SYMBOLS ;

# set min/max weights for individual stocks
var weight{i in SYMBOLS} >= 0, <= 1 ;

# add binary, 1 if held, 0 if not held
var held{SYMBOLS} binary;

# objective function, NOT USED
minimize alpha : sum{i in SYMBOLS} weight[i] ;

# weights must sum to 1 (fully invested)
subject to fully_invested : sum{i in SYMBOLS} weight[i] = 1 ;

# min weight constraint for individual asset
subject to MinWgt {i in SYMBOLS} : weight[i] >= 0.025 * held[i];

# max weight constraint for individual asset
subject to MaxWgt {i in SYMBOLS} : weight[i] <= .20 * held[i] ;

# number of stocks in portfolio
subject to MaxAssetsLB : 0 <= sum {i in SYMBOLS} held[i] ;
subject to MaxAssetsUB : sum {i in SYMBOLS} held[i] <= 6 ;

data;

set SYMBOLS :=  AA AXP BA BAC CAT CSCO CVX DD DIS GE HD HPQ IBM INTC JNJ JPM KFT KO MCD MMM MRK MSFT PFE PG T TRV UTX VZ WMT XOM ;
###############################################################################

```

接下来，让我们使用这个模型来寻找最小方差的投资组合。

```

	#--------------------------------------------------------------------------
	# Read GNU MathProg model/Setup constraints/Solve QP problem
	#--------------------------------------------------------------------------	
	model.file = 'model2.mod'

	# read model
	model = Rglpk.read.model(model.file,type = 'MathProg') 	

	# convert GNU MathProg model to constraint used in solve.QP
	constraints = Rglpk.create.constraints(model)$constraints	

	# Solve QP problem
	x = min.var.portfolio(ia, constraints)	

	# plot weights
	barplot(100*x, las=2, main='Minimum Variance Portfolio using GNU MathProg model \n with Minimum Investment and Number of Assets Constraints')

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/03/plot3-small2.png)

我还在[130/30 投资组合构建](https://systematicinvestor.wordpress.com/2011/10/18/13030-porfolio-construction/)文章中描述了另一个有趣的投资组合构建问题。请将以下模型描述复制并保存在“model3.mod”文件中：

```

###############################################################################
set SYMBOLS ;

# set min/max weights for individual stocks
var long {i in SYMBOLS} >= 0, <= 0.8 ;
var short{i in SYMBOLS} >= 0, <= 0.5 ;

# add binary, 1 if long, 0 if short
var islong{SYMBOLS} binary;

# objective function, NOT USED
minimize alpha : sum{i in SYMBOLS} long[i] ;

# weights must sum to 1 (fully invested)
subject to fully_invested : sum{i in SYMBOLS} (long[i] - short[i]) = 1 ;

# leverage is 1.6 = longs + shorts
subject to leverage : sum{i in SYMBOLS} (long[i] + short[i]) = 1.6 ;

# force long and short to be mutually exclusive (only one of them is greater then 0 for each i)
subject to long_flag  {i in SYMBOLS} : long[i]  <= islong[i] ;
subject to short_flag {i in SYMBOLS} : short[i] <= (1 - islong[i]) ;

data;

set SYMBOLS :=  AA AXP BA BAC CAT CSCO CVX DD DIS GE HD HPQ IBM INTC JNJ JPM KFT KO MCD MMM MRK MSFT PFE PG T TRV UTX VZ WMT XOM ;
###############################################################################

```

接下来，让我们使用这个模型来寻找最小方差的投资组合。

```

	#--------------------------------------------------------------------------
	# Read GNU MathProg model/Setup constraints/Solve QP problem
	#--------------------------------------------------------------------------	
	model.file = 'model3.mod'

	# read model
	model = Rglpk.read.model(model.file,type = 'MathProg') 	

	# convert GNU MathProg model to constraint used in solve.QP
	constraints = Rglpk.create.constraints(model)$constraints	

	# Solve QP problem, modify Input Assumptions to include short positions
	x = min.var.portfolio(aa.test.ia.add.short(ia), constraints)	

	# Compute total weight = longs - short
	x = x[1:ia$n] - x[-c(1:ia$n)]

	# plot weights
	barplot(100*x, las=2, main='Minimum Variance Portfolio using GNU MathProg model \n with 130:30 Constraints')

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/03/plot4-small2.png)

另一个有趣的投资组合构建问题是如何限制投资组合的换手率，或者限制最小的交易规模和交易次数。以下模型将交易规模限制在 5%到 20%之间，且交易次数不超过 8 次。请复制并保存以下模型描述在“model4.mod”文件中：

```

###############################################################################
set SYMBOLS ;

param CurWgt{SYMBOLS} ;

# set min/max weights for individual stocks
var weight{i in SYMBOLS} >= 0, <= 1 ;

# TradePos[i] - TradeNeg[i] = CurWgt[i] - weight[i]
var TradePos{i in SYMBOLS} >= 0 ;
var TradeNeg{i in SYMBOLS} >= 0 ;

# Only one of TradePos or TradeNeg is > 0
var TradeFlag{SYMBOLS} binary;

# add binary, 1 if traded, 0 if not traded
var trade{SYMBOLS} binary;

# objective function, NOT USED
minimize alpha : sum{i in SYMBOLS} weight[i] ;

# weights must sum to 1 (fully invested)
subject to fully_invested : sum{i in SYMBOLS} weight[i] = 1 ;

# setup Trades for individual asset
subject to TradeRange {i in SYMBOLS} : (CurWgt[i] - weight[i]) = (TradePos[i] - TradeNeg[i]) ;

# Only one of TradePos or TradeNeg is > 0
subject to TradeFlagPos {i in SYMBOLS} : TradePos[i] <= 100 * TradeFlag[i];
subject to TradeFlagNeg {i in SYMBOLS} : TradeNeg[i] <= 100 * (1 - TradeFlag[i]);

# min trade size constraint for individual asset
subject to MinTradeSize {i in SYMBOLS} : (TradePos[i] + TradeNeg[i]) >= 0.05 * trade[i];
subject to MaxTradeSize {i in SYMBOLS} : (TradePos[i] + TradeNeg[i]) <= .20 * trade[i] ; 

# number of trades in portfolio
subject to MaxTrade : sum {i in SYMBOLS} trade[i] <= 8 ;

data;

set SYMBOLS :=  AA AXP BA BAC CAT CSCO CVX DD DIS GE ;

param : CurWgt:=
AA	0.1
AXP	0.1
BA	0.1
BAC	0.1
CAT	0.1
CSCO	0.1
CVX	0.1
DD	0.1
DIS	0.1
GE	0.1
; 
###############################################################################

```

接下来，让我们使用这个模型来寻找最小方差的投资组合。

```

	#--------------------------------------------------------------------------
	# Read GNU MathProg model/Setup constraints/Solve QP problem
	#--------------------------------------------------------------------------	
	model.file = 'model4.mod'

	# reduce problem size
	ia = aa.test.create.ia.custom(tickers[1:10], dates = '2000::2010')

	# read model
	model = Rglpk.read.model(model.file,type = 'MathProg') 	

	# convert GNU MathProg model to constraint used in solve.QP
	constraints = Rglpk.create.constraints(model)$constraints	

	# Solve QP problem
	x = min.var.portfolio(ia, constraints)	

	# plot weights
	barplot(100*x, las=2, main='Minimum Variance Portfolio using GNU MathProg model \n with Turnover Constraints')

```

![plot5.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/03/plot5-small.png)

将 BA 和 GE 保持不变为 10%，其他 8 只股票的交易规模至少为 5%，且不超过 20%。

请让我知道在投资组合构建过程中您想要施加的其他类型的约束。

要查看这个示例的完整源代码，请查看[GitHub 上的 aa.gmpl.r 文件中的 portopt.mathprog.test()函数](https://github.com/systematicinvestor/SIT/blob/master/R/aa.gmpl.r)。
