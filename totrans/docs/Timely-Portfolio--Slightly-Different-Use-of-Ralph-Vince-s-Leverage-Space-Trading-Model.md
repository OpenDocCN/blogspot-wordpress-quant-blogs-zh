<!--yml
category: 未分类
date: 2024-05-18 15:17:55
-->

# Timely Portfolio: Slightly Different Use of Ralph Vince’s Leverage Space Trading Model

> 来源：[http://timelyportfolio.blogspot.com/2011/04/slightly-different-use-of-ralph-vinces.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/04/slightly-different-use-of-ralph-vinces.html#0001-01-01)

In honor of the press release [Dow Jones Indexes To Develop, Co-Brand Index Family With LSP Partners](http://press.djindexes.com/index.php/dow-jones-indexes-to-develop-co-brand-index-family-with-lsp-partners/) two days ago, I thought I would show another slightly different use of Ralph Vince’s *The Leverage Space Trading Model.*

Using the R LSPM package, we can build a monthly system around the probProfit calculation.  This particular system will enter long when the short term (12 month) probProfit exceeds the longer term (36 month) probProfit.  It exits when the short term falls below the longer term.

Feel free to substitute any index.  Some of my favorites are German Dax GDAXI, Japan Nikkei N225, Korea Kospi KS11, and Signapore Straits Times STI for international testing.  Additional US testing might look at NDX, RUT, CYC, XBD, HGX, REI, DJUSBK, OSX or anything that you can think of to break it.

The results are not fantastic, but the considerable drawdown reductions is nice.  Let me know how you would improve.

R code:

#Please see au.tra.sy blog [http://www.automated-trading-system.com/](http://www.automated-trading-system.com/)
#for original code and [http://www.fosstrading.com](http://www.fosstrading.com) for some of the
#other techniques

require(PerformanceAnalytics)
require(PApages)
require(quantmod)
require(LSPM)

tckr<-"^GSPC"

start<-"1929-01-01"
end<- format(Sys.Date(),"%Y-%m-%d") # yyyy-mm-dd

# Pull tckr index data from Yahoo! Finance
getSymbols(tckr, from=start, to=end)

GSPC<-adjustOHLC(GSPC,use.Adjusted=T)

GSPC<-to.monthly(GSPC)
rtn<-monthlyReturn(GSPC[,4])
# Define JPT function
jointProbTable <- function(x, n=3, FUN=median, ...) {
  # handle case with no negative returns; use -0.01
  for (sys in 1:numsys) {
      if (min(x[,sys])> -1) x[,sys][which.min(x[,sys])]<- -0.01
  }
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

# I know there are prettier ways to accomplish
# but I have to live within my limits

numsys<-1
numbins<-12

# Set Walk-Forward parameters (number of periods) for short
optim<-9 # 9 monthly returns
wf<-1 #walk forward 1 month; we'll set horizon separately
# Calculate number of WF cycles
numCycles = floor((nrow(rtn)-optim)/wf)

for (i in 0:(numCycles-1)) {
            # Define cycle boundaries
            start<-1+(i*wf)
            end<-optim+(i*wf)
            # Get returns for optimization cycle and create the JPT
            jpt <- jointProbTable(rtn[start:end,1:numsys],n=rep(numbins,numsys))
            outcomes<-jpt[[1]]
            probs<-jpt[[2]]
            port<-lsp(outcomes,probs)
            profitProb<-probProfit(port,target=0,horizon=6)
        profitProbWF<-c(rep(1,wf)) %o% profitProb
        maxLossWF<-c(rep(1,wf)) %o% jpt$maxLoss
        #make xts
        profitProbWF<-xts(profitProbWF,order.by=index(rtn[(end+1):(end+wf)]))
        maxLossWF<-xts(maxLossWF,order.by=index(rtn[(end+1):(end+wf)]))

            if (i==0) profitProbHistory<-profitProbWF else profitProbHistory<-rbind(profitProbHistory,profitProbWF)
            if (i==0) maxLossHistory<-maxLossWF else maxLossHistory<-rbind(maxLossHistory,maxLossWF)       
}

# Set Walk-Forward parameters (number of periods) for long
optim<-30 # 30 monthly returns
wf<-1 #walk forward 1 month; we'll set horizon separately
# Calculate number of WF cycles
numCycles = floor((nrow(rtn)-optim)/wf)

for (i in 0:(numCycles-1)) {
            # Define cycle boundaries
            start<-1+(i*wf)
            end<-optim+(i*wf)
            # Get returns for optimization cycle and create the JPT
            jpt <- jointProbTable(rtn[start:end,1:numsys],n=rep(numbins,numsys))
            outcomes<-jpt[[1]]
            probs<-jpt[[2]]
            port<-lsp(outcomes,probs)
            profitProb<-probProfit(port,target=0,horizon=3)
        profitProbWF<-c(rep(1,wf)) %o% profitProb
        maxLossWF<-c(rep(1,wf)) %o% jpt$maxLoss
        #make xts
        profitProbWFlong<-xts(profitProbWF,order.by=index(rtn[(end+1):(end+wf)]))
        maxLossWFlong<-xts(maxLossWF,order.by=index(rtn[(end+1):(end+wf)]))

            if (i==0) profitProbHistorylong<-profitProbWFlong else profitProbHistorylong<-rbind(profitProbHistorylong,profitProbWFlong)
            if (i==0) maxLossHistorylong<-maxLossWFlong else maxLossHistorylong<-rbind(maxLossHistorylong,maxLossWFlong)       
}

signalshortterm<-profitProbHistory
#adjust the long term with maxLoss to hopefully reduce drawdown
signallongterm<-profitProbHistorylong - maxLossHistorylong

chartSeries(signalshortterm,TA="addTA(signallongterm,on=1)", theme="white", name="Short and Long Term Probability of Profit")

# Create the signals and enter when long term is < short term
sigup <- ifelse(signallongterm < signalshortterm,1,0)

# no need for lag since signal generated from previous months]
# sigup <- lag(sigup,1) # Note k=1 implies a move *forward*

# Replace missing signals with no position
# (generally just at beginning of series)
sigup[is.na(sigup)] <- 0

#Calculate equity curves
eq_up <- cumprod(1+(rtn)*sigup)

perf_compare<-merge(sigup*rtn,rtn[(optim+1):NROW(rtn)])
colnames(perf_compare)<-c("LSPM probProfit System",tckr)

charts.PerformanceSummary(perf_compare,ylog=TRUE,legend.loc="topleft",main="LSPM probProfit System Performance Comparison")