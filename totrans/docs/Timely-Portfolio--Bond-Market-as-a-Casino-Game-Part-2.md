<!--yml
category: 未分类
date: 2024-05-18 15:19:00
-->

# Timely Portfolio: Bond Market as a Casino Game Part 2

> 来源：[http://timelyportfolio.blogspot.com/2011/04/bond-market-as-casino-game-part-2.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/04/bond-market-as-casino-game-part-2.html#0001-01-01)

Before starting Part 2, please see [Bonds as a Casino Game Part 1](http://timelyportfolio.blogspot.com/2011/04/bond-market-as-casino-game-part-1.html).   For the Monte Carlo random simulation purists, please ignore some unimportant technicalities in my simulation.

To spoil the fun, here is the conclusion:

> Any way you look at it, the US Bond Market has been a wonderfully profitable game, but the game is changing, and past performance in no way predicts similar future returns.  Please lower your expectations for your bond investments.

Given the probabilities and average outcomes that we have experienced in the Barclays Capital U.S. Aggregate Bond Index since 1980, let’s see what happens if we turn the bond market into a game, and play it in 10,000 30 year games with Microsoft Excel (sorry R, we’ll use you later).

The results demonstrate how attractive this game is to play with the worst case of 10,000 trials still offering a 5.6% annualized return.  The chart below shows 200 of the 10,000 trials (Excel limits to 255), the actual Barclays Aggregate results, and the average of 10,000 trials.

Most interesting to me is how the game seems to be changing to less favorable as the actual approaches the average.  This is also clearly visible in the pivot table by decade as expected returns diminish with lower interest rates.

Although using just two buckets is helpful and eases the analysis, we can use more buckets/bins with [Ralph Vince’s *Leverage Space Trading Model*](http://www.amazon.com/gp/product/0470455950/ref=as_li_qf_sp_asin_il_tl?ie=UTF8&tag=timelyp-20&linkCode=as2&camp=1789&creative=9325&creativeASIN=0470455950) and the R LSPM package from [Foss Trading](http://www.fosstrading.com).

Any way you look at it, the US Bond Market has been a wonderfully profitable game, but the game is changing, and past performance in no way predicts similar future returns.  Please lower your expectations for your bond investments.

R code:

#Please see au.tra.sy blog [http://www.automated-trading-system.com/](http://www.automated-trading-system.com/)
#for original code and [http://www.fosstrading.com](http://www.fosstrading.com)
#I take no credit for the majority of this code
#I simply changed a couple of things to use xts return series
#and to do simulations of bonds

require(xts)
require(PerformanceAnalytics)

numbins<-10
# get data series from csv file and limit to 1980 to 2010
rtn<-as.xts(read.csv("lbustruu.csv",row.names=1))["1980::"]
# Calculate number of WF cycles
numCycles = floor((nrow(rtn)-optim)/wf)
# Define JPT function
jointProbTable <- function(x, n=3, FUN=median, ...) {
  # Load LSPM
  if(!require(LSPM,quietly=TRUE)) stop(warnings())

  # Function to bin data
  quantize <- function(x, n, FUN=median, ...) {
    if(is.character(FUN)) FUN <- get(FUN)
    bins <- cut(x, n, labels=FALSE)
    res <- sapply(1:NROW(x), function(i) FUN(x[bins==bins[i]], ...))
  }
  # Allow for different values of 'n' for each system in 'x'
  if(NROW(n)==1) {
    n <- rep(n,NCOL(x))
  } else
  if(NROW(n)!=NCOL(x)) stop("invalid 'n'")
  # Bin data in 'x'
  qd <- sapply(1:NCOL(x), function(i) quantize(x[,i],n=n[i],FUN=FUN,...))
  # Aggregate probabilities
  probs <- rep(1/NROW(x),NROW(x))
  res <- aggregate(probs, by=lapply(1:NCOL(qd), function(i) qd[,i]), sum)
  # Clean up output, return lsp object
  colnames(res) <- colnames(x)
  res <- lsp(res[,1:NCOL(x)],res[,NCOL(res)])
  return(res)
}
# Get returns and create the JPT
jpt <- jointProbTable(rtn,n=numbins)
outcomes<-jpt[[1]]
probs<-jpt[[2]]
port<-lsp(outcomes,probs)

# Analyze drawdowns
# Use LSPM to get Probability of Drawdown > 5%
drawdownProb<-probDrawdown(port,DD=.05,horizon=12)
# Display probability of 5% drawdown over 1 year
actualDraw<-sum(table.Drawdowns(rtn)$Length)/NROW(rtn)
#plot bar chart of expected vs actual
barplot(rbind(drawdownProb,actualDraw),beside=TRUE,main="Expected vs. Actual Drawdown > 5%",names.arg=c("Expected", "Actual"))

# Analyze gains
# Use LSPM to get Probability of Profit > 5%
profitProb<-probProfit(port,target=.05,horizon=12)
# Get rolling 12 month period returns
yearReturns<-apply.rolling(rtn,width=12,by=1,FUN="Return.annualized")
# Get actual percentage of 12 month returns > 5%
actualProb<-NROW(yearReturns[which(yearReturns$calcs>.05),1])/NROW(yearReturns)
#plot bar chart of expected vs actual
barplot(rbind(profitProb,actualProb),beside=TRUE,main="Expected vs. Actual 12 month > 5%",names.arg=c("Expected", "Actual"))