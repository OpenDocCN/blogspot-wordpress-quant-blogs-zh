<!--yml
category: 未分类
date: 2024-05-18 14:40:40
-->

# Classical Technical Patterns | Systematic Investor

> 来源：[https://systematicinvestor.wordpress.com/2012/05/22/classical-technical-patterns/#0001-01-01](https://systematicinvestor.wordpress.com/2012/05/22/classical-technical-patterns/#0001-01-01)

In my [presentation](http://www.systematicportfolio.com/RFinance2012) about Seasonality Analysis and Pattern Matching at the [R/Finance](http://www.rinfinance.com/agenda/) conference, I used examples that I have previously covered in my blog:

The only subject in my [presentation](http://www.systematicportfolio.com/RFinance2012) that I have not discussed previously was about [Classical Technical Patterns](http://en.wikipedia.org/wiki/Chart_pattern). For example, the [Head and Shoulders](http://en.wikipedia.org/wiki/Head_and_shoulders_%28chart_pattern%29) pattern, most often seen in up-trends and generally regarded as a reversal pattern. Below I implemented the algorithm and pattern definitions presented in the [Foundations of Technical Analysis by A. Lo, H. Mamaysky, J. Wang (2000)](http://web.mit.edu/alo/www/Papers/1705-1765.pdf) paper.

To identify a price pattern I will follow steps as described in the [Foundations of Technical Analysis](http://web.mit.edu/alo/www/Papers/1705-1765.pdf) paper:

*   First, fit a smoothing estimator, a kernel regression estimator, to approximate time series.
*   Next, determine local extrema, tops and bottoms, using fist derivative of the kernel regression estimator.
*   Define classical technical patterns in terms of tops and bottoms.
*   Search for classical technical patterns throughout the tops and bottoms of the kernel regression estimator.

Let’s begin by loading historical prices for SPY:

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

The first step is to fit a smoothing estimator, a [kernel regression estimator](http://en.wikipedia.org/wiki/Kernel_density_estimation), to approximate time series. I used [sm](http://cran.r-project.org/web/packages/sm/index.html) package to fit kernel regression:

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

The second step is to find local extrema, tops and bottoms, using first derivative of the kernel regression estimator. (more details in the paper on page 15):

```

	temp = diff(sign(diff(mhat)))
	# loc - location of extrema, loc.dir - direction of extrema
	loc = which( temp != 0 ) + 1
		loc.dir = -sign(temp[(loc - 1)])

```

I put the logic for the first and second step into the [find.extrema()](https://github.com/systematicinvestor/SIT/blob/master/R/rfinance2012.r) function.

The next step is to define classical technical patterns in terms of tops and bottoms. The [pattern.db()](https://github.com/systematicinvestor/SIT/blob/master/R/rfinance2012.r) function implements the 10 patterns described in the paper on page 12\. For example, let’s have a look at the [Head and Shoulders](http://en.wikipedia.org/wiki/Head_and_shoulders_%28chart_pattern%29) pattern. The [Head and Shoulders](http://en.wikipedia.org/wiki/Head_and_shoulders_%28chart_pattern%29) pattern:

*   is defined by 5 extrema points (E1, E2, E3, E4, E5)
*   starts with a maximum (E1)
*   E1 and E5 are within 1.5 percent of their average
*   E2 and E4 are within 1.5 percent of their average

The R code below that corresponds to the [Head and Shoulders](http://en.wikipedia.org/wiki/Head_and_shoulders_%28chart_pattern%29) pattern is a direct translation, from the pattern description in the paper on page 12, and is very readable:

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

The last step is a function that searches for all defined patterns in the kernel regression representation of original time series.

I put the logic for this step into the [find.patterns()](https://github.com/systematicinvestor/SIT/blob/master/R/rfinance2012.r) function. Below is a simplified version:

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

I put the logic for the entire process in to the [plot.patterns()](https://github.com/systematicinvestor/SIT/blob/master/R/rfinance2012.r) helper function. The [plot.patterns()](https://github.com/systematicinvestor/SIT/blob/master/R/rfinance2012.r) function first call find.extrema() function to determine extrema points, and next it calls find.patterns() function to find and plot patterns. Let’s find classical technical patterns in the last 150 days of SPY history:

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

It is very easy to define you own custom patterns and I encourage everyone to give it a try.

[![](img/5e142b51436062d709ac83a7bc1d3735.png "plot.pattern.matching.png.small")](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/05/plot-pattern-matching-small.png)

To view the complete source code for this example, please have a look at the [pattern.test() function in rfinance2012.r at github](https://github.com/systematicinvestor/SIT/blob/master/R/rfinance2012.r).