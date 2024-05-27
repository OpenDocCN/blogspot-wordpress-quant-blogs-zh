<!--yml

类别：未分类

日期：2024-05-18 14:40:40

-->

# 古典技术图案 | 系统投资者

> 来源：[`systematicinvestor.wordpress.com/2012/05/22/classical-technical-patterns/#0001-01-01`](https://systematicinvestor.wordpress.com/2012/05/22/classical-technical-patterns/#0001-01-01)

在我在[R/Finance](http://www.rinfinance.com/agenda/)会议上关于季节性分析和图案匹配的[演示](http://www.systematicportfolio.com/RFinance2012)中，我使用了之前在我的博客中讨论过的示例：

我[演示文稿](http://www.systematicportfolio.com/RFinance2012)中唯一没有之前讨论过的主题是关于[古典技术图案](http://en.wikipedia.org/wiki/Chart_pattern)。例如，[头肩顶](http://en.wikipedia.org/wiki/Head_and_shoulders_%28chart_pattern%29)图案，最常见于上升趋势，并且通常被视为反转图案。以下是我在[技术分析基础](http://web.mit.edu/alo/www/Papers/1705-1765.pdf)论文中提出的算法和图案定义。

要识别价格图案，我将按照[技术分析基础](http://web.mit.edu/alo/www/Papers/1705-1765.pdf)论文中描述的步骤进行：

+   首先，拟合平滑估计器，即核回归估计器，以逼近时间序列。

+   接下来，使用核回归估计器的一阶导数确定局部极值点，即顶部和底部。

+   根据顶部和底部定义古典技术图案。

+   在核回归估计器的顶部和底部寻找古典技术图案。

让我们开始加载 SPY 的历史价格：

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
	# Find Classical Techical Patterns, based on
	# Pattern Matching. Based on Foundations of Technical Analysis
	# by A.W. LO, H. MAMAYSKY, J. WANG	
	#****************************************************************** 
	plot.patterns(data, 190, ticker)

```

第一步是拟合平滑估计器，即[核回归估计器](http://en.wikipedia.org/wiki/Kernel_density_estimation)，以逼近时间序列。我使用[sm](http://cran.r-project.org/web/packages/sm/index.html)软件包来拟合核回归：

```

	library(sm)
	y = as.vector( last( Cl(data), 190) )
	t = 1:len(y)

	# fit kernel regression with cross-validatio
	h = h.select(t, y, method = 'cv')
		temp = sm.regression(t, y, h=h, display = 'none')

	# find estimated fit
	mhat = approx(temp$eval.points, temp$estimate, t, method='linear')$y

```

第二步是使用核回归估计器的一阶导数找到局部极值点，即顶部和底部。（更多细节请参阅第 15 页的论文）：

```

	temp = diff(sign(diff(mhat)))
	# loc - location of extrema, loc.dir - direction of extrema
	loc = which( temp != 0 ) + 1
		loc.dir = -sign(temp[(loc - 1)])

```

我将第一步和第二步的逻辑放入了[find.extrema()](https://github.com/systematicinvestor/SIT/blob/master/R/rfinance2012.r)函数中。

下一步是根据顶部和底部定义古典技术图案。[pattern.db()](https://github.com/systematicinvestor/SIT/blob/master/R/rfinance2012.r)函数实现了论文第 12 页描述的 10 种图案。例如，让我们看一下[头肩顶](http://en.wikipedia.org/wiki/Head_and_shoulders_%28chart_pattern%29)图案。[头肩顶](http://en.wikipedia.org/wiki/Head_and_shoulders_%28chart_pattern%29)图案：

+   由 5 个极值点（E1、E2、E3、E4、E5）定义

+   以最大值（E1）开始

+   E1 和 E5 的值与其平均值相差不超过 1.5%。

+   E2 和 E4 的值与其平均值相差不超过 1.5%。

下面的 R 代码对应于[头肩顶图](http://en.wikipedia.org/wiki/Head_and_shoulders_%28chart_pattern%29)模式，是直接翻译自论文中第 12 页的模式描述，非常易读：

```

	#****************************************************************** 	
	# Head-and-shoulders (HS)
	#****************************************************************** 	
	pattern = list()
	pattern$len = 5
	pattern$start = 'max'
	pattern$formula = expression({
		avg.top = (E1 + E5) / 2
		avg.bot = (E2 + E4) / 2

		# E3 > E1, E3 > E5
		E3 > E1 &
		E3 > E5 &

		# E1 and E5 are within 1.5 percent of their average
		abs(E1 - avg.top) < 1.5/100 * avg.top &
		abs(E5 - avg.top) < 1.5/100 * avg.top &

		# E2 and E4 are within 1.5 percent of their average
		abs(E2 - avg.bot) < 1.5/100 * avg.bot &
		abs(E4 - avg.bot) < 1.5/100 * avg.bot
		})
	patterns$HS = pattern		

```

最后一步是一个函数，它在原始时间序列的核回归表示中搜索所有定义的模式。

我将这一步的逻辑放入了[find.patterns()](https://github.com/systematicinvestor/SIT/blob/master/R/rfinance2012.r)函数中。以下是一个简化版本：

```

find.patterns <- function
(
	obj, 	# extrema points
	patterns = pattern.db() 
) 
{
	data = obj$data
	extrema.dir = obj$extrema.dir
	data.extrema.loc = obj$data.extrema.loc
	n.index = len(data.extrema.loc)

	# search for patterns
	for(i in 1:n.index) {

		for(pattern in patterns) {

			# check same sign
			if( pattern$start * extrema.dir[i] > 0 ) {

				# check that there is suffcient number of extrema to complete pattern
				if( i + pattern$len - 1 <= n.index ) {

					# create enviroment to check pattern: E1,E2,...,En; t1,t2,...,tn
					envir.data = c(data[data.extrema.loc][i:(i + pattern$len - 1)], 
					data.extrema.loc[i:(i + pattern$len - 1)])									
						names(envir.data) = c(paste('E', 1:pattern$len, sep=''), 
							paste('t', 1:pattern$len, sep=''))
					envir.data = as.list(envir.data)					

					# check if pattern was found
					if( eval(pattern$formula, envir = envir.data) ) {
						cat('Found', pattern$name, 'at', i, '\n')
					}
				}
			}		
		}	
	}

}

```

我将整个过程的逻辑放入了[plot.patterns()](https://github.com/systematicinvestor/SIT/blob/master/R/rfinance2012.r)辅助函数中。[plot.patterns()](https://github.com/systematicinvestor/SIT/blob/master/R/rfinance2012.r)函数首先调用 find.extrema()函数来确定极值点，然后调用 find.patterns()函数来查找并绘制模式。让我们在 SPY 历史的最后 150 天中找到经典的技术模式：

```

	#*****************************************************************
	# Load historical data
	#****************************************************************** 
	load.packages('quantmod')
	ticker = 'SPY'

	data = getSymbols(ticker, src = 'yahoo', from = '1970-01-01', auto.assign = F)
		data = adjustOHLC(data, use.Adjusted=T)

	#*****************************************************************
	# Find Classical Techical Patterns, based on
	# Pattern Matching. Based on Foundations of Technical Analysis
	# by A.W. LO, H. MAMAYSKY, J. WANG	
	#****************************************************************** 
	plot.patterns(data, 150, ticker)

```

定义您自己的自定义模式非常容易，我鼓励每个人都尝试一下。

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/05/plot-pattern-matching-small.png)

要查看此示例的完整源代码，请查看[GitHub 上的 rfinance2012.r 中的 pattern.test()函数](https://github.com/systematicinvestor/SIT/blob/master/R/rfinance2012.r)。
