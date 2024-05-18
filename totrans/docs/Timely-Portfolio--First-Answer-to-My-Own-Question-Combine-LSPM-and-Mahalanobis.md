<!--yml
category: 未分类
date: 2024-05-18 15:17:46
-->

# Timely Portfolio: First Answer to My Own Question-Combine LSPM and Mahalanobis

> 来源：[http://timelyportfolio.blogspot.com/2011/05/first-answer-to-my-own-question-combine.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/05/first-answer-to-my-own-question-combine.html#0001-01-01)

I first wanted to thank

[http://www.fosstrading.com](http://www.fosstrading.com/)

for the very kind and unexpected mention over the weekend.  You will notice almost all of my code contains some credit to Foss Trading for the examples and great packages.  I hate that I could not join everyone at 

[R/Finance 2011: Applied Finance with R Conference](http://rinfinance.com/)

last weekend.

In my last post

[Another Use of LSPM in Tactical Portfolio Allocation](http://timelyportfolio.blogspot.com/2011/04/another-use-of-lspm-in-tactical.html)

, I expressed a slight bit of frustration with the drawdown experienced with the final system.  Since I got no comments or feedback on improvements, I guess I will have to try to answer my own question, “How do I reduce the drawdown?”  My first thought was to use the techniques shown in my previous set of posts

[Great FAJ Article on Statistical Measure of Financial Turbulence Part 3](http://timelyportfolio.blogspot.com/2011/04/great-faj-article-on-statistical_6197.html)

about

[Mahalanobis distance](http://en.wikipedia.org/wiki/Mahalanobis_distance)

as a measure of financial turbulence.

[![faj abstract](img/83360755bc97c4bdbc31c63f84665b6b.png "faj abstract")](http://www.cfapubs.org/doi/abs/10.2469/faj.v66.n5.3)

The results demonstrate a slight improvement in max drawdown and other downside measures, but does not ultimately satisfy my constant yearning for smaller drawdown.

| If nothing else, maybe you can use my ggplot2 chart of a PerformanceAnalytics table.  I was pretty excited to get this working, and I plan to incorporate many more of these in my testing. [![](img/ed58445cb87e2e0b2bd54b82b8b1b448.png)](https://picasaweb.google.com/lh/photo/5VQD5b1wogWh74y3xF1QLw?feat=embedwebsite) |
| From [TimelyPortfolio](https://picasaweb.google.com/kentonlrussell/TimelyPortfolio02?feat=embedwebsite) |

I blog to record my thoughts and hopefully generate a valuable dialogue with my readers who are probably far smarter and more qualified than me.  Please comment or provide feedback.

R code:

#Please see au.tra.sy blog

[http://www.automated-trading-system.com/](http://www.automated-trading-system.com/)

#for original walkforward/optimize code and

[http://www.fosstrading.com](http://www.fosstrading.com/)

#for other techniques

require(PerformanceAnalytics)

require(quantmod)

require(RQuantLib)

require(reshape2)  #for some fancy ggplot charting

require(ggplot2)

#get bond returns to avoid proprietary data problems

#see previous timelyportfolio blogposts for explanation

#probably need to make this a function since I will be using so much

getSymbols("GS10",src="FRED") #load US Treasury 10y from Fed Fred

GS10pricereturn<-GS10  #set this up to hold price returns

GS10pricereturn[1,1]<-0

colnames(GS10pricereturn)<-"PriceReturn"

#I know I need to vectorize this but not qualified enough yet

#Please feel free to comment to show me how to do this

for (i in 1:(NROW(GS10)-1)) {

  GS10pricereturn[i+1,1]<-FixedRateBondPriceByYield(yield=GS10[i+1,1]/100,issueDate=Sys.Date(),

    maturityDate= advance("UnitedStates/GovernmentBond", Sys.Date(), 10, 3),

    rates=GS10[i,1]/100,period=2)[1]/100-1

}

#interest return will be yield/12 for one month

GS10interestreturn<-lag(GS10,k=1)/12/100

colnames(GS10interestreturn)<-"Interest Return"

#total return will be the price return + interest return

GS10totalreturn<-GS10pricereturn+GS10interestreturn

colnames(GS10totalreturn)<-"Bond Total Return"

#get sp500 returns from FRED

getSymbols("SP500",src="FRED") #load SP500

#unfortunately cannot get substitute for proprietary CRB data

#get data series from csv file

CRB<-as.xts(read.csv("spxcrbndrbond.csv",row.names=1))[,2]

#do a little manipulation to get the data lined up on monthly basis

GS10totalreturn<-to.monthly(GS10totalreturn)[,4]

SP500<-to.monthly(SP500)[,4]

#get monthly format to yyyy-mm-dd with the first day of the month

index(SP500)<-as.Date(index(SP500))

#my CRB data is end of month; could change but more fun to do in R

CRB<-to.monthly(CRB)[,4]

index(CRB)<-as.Date(index(CRB))

#now lets merge to get asset class returns

assetROC<-na.omit(merge(ROC(SP500,type="discrete"),CRB,GS10totalreturn))

# Set Walk-Forward parameters (number of periods)

optim<-12 #1 year = 12 monthly returns

wf<-1 #walk forward 1 monthly returns

numsys<-2

# Calculate number of WF cycles

numCycles = floor((nrow(assetROC)-optim)/wf)

# Define JPT function

# this is now part of LSPM package, but fails when no negative returns

# so I still include this where I can force a negative return

jointProbTable <- function(x, n=3, FUN=median, ...) {

  # Load LSPM

  if(!require(LSPM,quietly=TRUE)) stop(warnings())

  # handle case with no negative returns

  for (sys in 1:numsys) {

    if (min(x[,sys])> -1) x[,sys][which.min(x[,sys])]<- -0.03

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

for (i in 0:(numCycles-1)) {

            # Define cycle boundaries

            start<-1+(i*wf)

            end<-optim+(i*wf)

            # Get returns for optimization cycle and create the JPT

        # specify number of bins; does not seem to drastically affect results

        numbins<-6

            jpt <- jointProbTable(assetROC[start:end,1:numsys],n=rep(numbins,numsys))

            outcomes<-jpt[[1]]

            probs<-jpt[[2]]

            port<-lsp(outcomes,probs)

            # DEoptim parameters (see ?DEoptim)

            np=numsys*10       # 10 * number of mktsys

            imax=1000       #maximum number of iterations

            crossover=0.6       #probability of crossover

            NR <- NROW(port$f)

            DEctrl <- list(NP=np, itermax=imax, CR=crossover, trace=TRUE)

            # Optimize f

            res <- optimalf(port, control=DEctrl)

        # use upper to restrict to a level that you might feel comfortable

            #res <- optimalf(port, control=DEctrl, lower=rep(0,13), upper=rep(0.2,13))

    # these are other possibilities but I gave up after 24 hours

        #maxProbProfit from Foss Trading

        #res<-maxProbProfit(port, 1e-6, 6, probDrawdown, 0.1, DD=0.2, control=DEctrl)

        #probDrawdown from Foss Trading

        #res<-optimalf(port,probDrawdown,0.1,DD=0.2,horizon=6,control=DEctrl)

            # Save leverage amounts as optimal f

        # Examples in the book Ralph Vince Leverage Space Trading Model

        # all in dollar terms which confuses me

        # until I resolve I changed lev line to show optimal f output

        lev<-res$f[1:numsys]

            #lev<-c(res$f[1]/(-jpt$maxLoss[1]/10),res$f[2]/(-jpt$maxLoss[2]/10))

            levmat<-c(rep(1,wf)) %o% lev #so that we can multiply with the wfassetROC

            # Get the returns for the next Walk-Forward period

            wfassetROC <- assetROC[(end+1):(end+wf),1:numsys]

            wflevassetROC <- wfassetROC*levmat #apply leverage to the returns

            if (i==0) fullassetROC<-wflevassetROC else fullassetROC<-rbind(fullassetROC,wflevassetROC)

        if (i==0) levered<-levmat else levered<-rbind(levered,levmat)

}

#not super familiar with xts, but this add dates to levered

levered<-xts(levered,order.by=index(fullassetROC) )

colnames(levered)<-c("sp500 optimal f","crb optimal f")

chart.TimeSeries(levered, legend.loc="topleft", cex.legend=0.6)

#review the optimal f values

#I had to fill the window to my screen to avoid a error from R on margins

par(mfrow=c(numsys,1))

for (i in 1:numsys) {

    chart.TimeSeries(levered[,i],xlab=NULL)

}

#charts.PerformanceSummary(fullassetROC, ylog=TRUE, main="Performance Summary with Optimal f Applied as Allocation")

assetROCAnalyze<-merge(assetROC,fullassetROC)

colnames(assetROCAnalyze)<-c("sp500","crb","US10y","sp500 f","crb f")

charts.PerformanceSummary(assetROCAnalyze,ylog=TRUE,main="Performance Summary with Optimal f Applied as Allocation")

#build a portfolio with sp500 and crb

leveredadjust<-levered

#allow up to 50% allocation in CRB

leveredadjust[,2]<-ifelse(levered[,2]<0.25,0,0.5)

#allow up to 100% allocation in SP500 but portfolio constrained to 1 leverage

leveredadjust[,1]<-ifelse(levered[,1]<0.25,0,1-levered[,2])

colnames(leveredadjust)<-c("sp500 portfolio allocation","crb portfolio allocation")

assetROCadjust<-merge(assetROCAnalyze,leveredadjust[,1:2]*assetROC[,1:2])

colnames(assetROCadjust)<-c("sp500","crb","US10y","sp500 f","crb f","sp500 system component","crb system component")

charts.PerformanceSummary(assetROCadjust,ylog=TRUE)

#review the allocations versus optimal f

#I had to fill the window to my screen to avoid a error from R on margins

par(mfrow=c(numsys,1))

for (i in 1:numsys) {

    chart.TimeSeries(merge(levered[,i],leveredadjust[,i]),xlab=NULL,legend.loc="topleft",main="")

}

#add bonds when out of sp500 or crb

assetROCportfolio<-assetROCadjust[,6]+assetROCadjust[,7]+ifelse(leveredadjust[,1]+leveredadjust[,2] >= 1,0,(1-leveredadjust[,1]-leveredadjust[,2])*assetROC[,3])

assetROCadjust<-merge(assetROCAnalyze,assetROCportfolio)

colnames(assetROCadjust)<-c("sp500","crb","US10y","sp500 f","crb f","system portfolio")

charts.PerformanceSummary(assetROCadjust[,c(1:3,6)],ylog=TRUE,main="Optimal f System Portfolio with Bond Filler")

#see timelyportfolio blog post

[http://timelyportfolio.blogspot.com/2011/04/great-faj-article-on-statistical_6197.html](http://timelyportfolio.blogspot.com/2011/04/great-faj-article-on-statistical_6197.html)

#get Correlations for Mahalanobis filter

#get data from St. Louis Federal Reserve (FRED) to add 20y USTreasury data

getSymbols("GS20",src="FRED") #load 20yTreasury; 20y has gap 86-93; 30y has gap in early 2000s

getSymbols("GS30",src="FRED") #load 30yTreasury to fill 20y gap 86-93

#fill 20y gap from discontinued 20y Treasuries with 30y

GS20["1987-01::1993-09"]<-GS30["1987-01::1993-09"]

assetROC<-merge(assetROC,momentum(GS20)/100)

corrBondsSp<-runCor(assetROC[,4],assetROC[,1],n=7)

corrBondsCrb<-runCor(assetROC[,4],assetROC[,2],n=7)

corrSpCrb<-runCor(assetROC[,2],assetROC[,1],n=7)

#composite measure of correlations between asset classes and roc-weighted correlations

assetCorr<-(corrBondsSp+corrBondsCrb+corrSpCrb+

    (corrBondsSp*corrSpCrb*assetROC[,1])+

    (corrBondsCrb*corrSpCrb*assetROC[,2])-

    assetROC[,4])/6

#sum of ROCs of asset classes

assetROCSum<-assetROC[,1]+assetROC[,2]+assetROC[,4]

#finally the turbulence measure

turbulence<-abs(assetCorr*assetROCSum*100)

colnames(turbulence)<-"Turbulence-correlation"

signal<-ifelse(turbulence>0.8,0,1)

signal<-lag(signal,k=1)

signal[0]<-0

system_perf_turbulence<-assetROCportfolio*signal

perf_compare<-merge(assetROC[,1:2],assetROCportfolio,system_perf_turbulence)

colnames(perf_compare)<-c("SP500","CRB","LSPMportfolio","LSPMportfolio_turbulence")

charts.PerformanceSummary(perf_compare,ylog=TRUE,colorset=c("gray70","goldenrod","cadetblue","darkolivegreen3"),main="Comparison of Original LSPM System and Turbulence LSPM System")

downsideTable<-melt(cbind(rownames(table.DownsideRisk(perf_compare)),table.DownsideRisk(perf_compare)))

colnames(downsideTable)<-c("Statistic","Portfolio","Value")

ggplot(downsideTable, stat="identity", aes(x=Statistic,y=Value,fill=Portfolio)) + geom_bar(position="dodge") + coord_flip()