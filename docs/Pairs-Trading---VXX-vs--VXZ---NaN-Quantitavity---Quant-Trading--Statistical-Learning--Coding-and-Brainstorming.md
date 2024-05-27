<!--yml

分类：未分类

日期：2024-05-18 13:57:35

-->

# 对冲交易 – VXX 对比 VXZ | 非数值量化 - 对冲交易、统计学习、编程和头脑风暴

> 来源：[`quantlife.wordpress.com/2012/10/18/pairs-trading-vxx-vs-vxz/#0001-01-01`](https://quantlife.wordpress.com/2012/10/18/pairs-trading-vxx-vs-vxz/#0001-01-01)

```
################################################################################################
# Quantitative Trading Strategies - Volatility Trading:
# Date Created: 2012-10-18
# Author:       Nan Zhou, zhounan1983@gmail.com
#
# Use volatility futures, shortdate vs medium dated
# VXX iPath S&P 500 VIX Short-Term Futures ETN (VXX)
# VXZ iPath S&P 500 VIX Mid-Term Futures ETN (VXZ)
#
# Plan is to check for trade entry at the open, and exit the trade at the close:
# IF signal < signalLowLim then in contango and do a carry trade
# IF signal > signalUpperLim then in backwardation so do a reverse carry
# ELSE do nothing

################################################################################################
## Install all required packages:
rm(list=ls())
library("quantmod"); library("PerformanceAnalytics")
par(ask=T); memory.size(max = 4000); options(digits=8, digits.secs=4)

## PLEASE CHANGE THE WORKFOLD TO YOUR WORK FOLD FIRST ##
workfold <- "H:\\My References\\Research\\2012_10_Trading Codes";
# workfold <- "C:\\Dropbox\\Research\\2012-10 VIX Trading Strategies";
setwd(workfold);

################################################################################################
# INPUT OF PARAMETERS
################################################################################################

signalLowLim   <- 0.9
signalUpperLim <- 1.1
symbolLst      <- c("VXX", "VXZ", "^GSPC")
dataSrc        <- "yahoo"
dataSrc        <- "csv"
startDate      <- as.Date("2010-01-01") #Specify what date to get the prices from
hedgeTrainingStartDate <- startDate #Start date for training the hedge ratio
hedgeTrainingEndDate   <- as.Date("2011-01-01") #End date for training the hedge ratio
tradingStartDate       <- as.Date("2011-01-02") #Date to run the strategy from
# tradingEndDate         <- as.Date("2011-12-31") #Date to run the strategy from
tradingEndDate         <- Sys.Date()

#--------------------------------------------------------------
### SECTION 1 - Download Data & Calculate Returns ###

## Download the data:
pnlEnv <- new.env() #Make a new environment for quantmod to store data in

importOHLC <- function(symbolLst = NULL, env = .GlobalEnv, src = "yahoo", format = "%m/%d/%Y",
                        return.class = "xts", from = Sys.Date()-365, end = Sys.Date()){
    if (src == "csv"){
        for (i in 1:length(symbolLst)){
            symbolLst <- toupper(gsub("\\^", "", symbolLst))
            symbol <- symbolLst[i]
            namesData <- c("Open", "High", "Low", "Close", "Volume", "Adj.Close")
            fr     <- read.csv(file = paste(symbol,'csv',sep='.'))
            fr     <- xts(fr[, namesData], as.Date(as.character(fr[, "Date"]), format = format))
            colnames(fr) <- paste(symbol, c("Open", "High", "Low", "Close", "Volume", "Adjusted"), sep = ".")
            fr <- quantmod:::convert.time.series(fr = fr, return.class = return.class)
            fr <- window(fr, start = from, end = end, extend = TRUE)
            assign(symbol, fr, env)
        }
    }
    else{
        getSymbols(symbolLst, env = env, src = src, from = from, end = end)
    }

    return(symbolLst)    
}

importOHLC(symbolLst, env = pnlEnv, src = "csv", format = "%m/%d/%Y", from = startDate, end = Sys.Date())

## Calculate returns for VXX and VXZ:
vxxRet <- (Cl(pnlEnv$VXX)/Op(pnlEnv$VXX))-1
colnames(vxxRet) <- "Ret"
pnlEnv$VXX <- cbind(pnlEnv$VXX,vxxRet)
vxzRet <- (Cl(pnlEnv$VXZ)/Op(pnlEnv$VXZ))-1
colnames(vxzRet) <- "Ret"
pnlEnv$VXZ <- cbind(pnlEnv$VXZ,vxzRet)

#--------------------------------------------------------------
### SECTION 2 - Calculating the hedge ratio ###
## Want to work out a hedge ratio, so that we can remain Vega neutral (the futures contact are trading VEGA)

trainVxx <- window(pnlEnv$VXX$Ret,start=hedgeTrainingStartDate ,end=hedgeTrainingEndDate)
trainVxz <- window(pnlEnv$VXZ$Ret,start=hedgeTrainingStartDate ,end=hedgeTrainingEndDate)
trainData = na.omit(cbind(trainVxx,trainVxz))
colnames(trainData) <- c("VXX","VXZ")

## Simply linearly regress the returns of Vxx with Vxz:
regression <- lm(trainData[,"VXZ"] ~ trainData[,"VXX"]) #Linear Regression
hedgeratio <- regression$coefficient[2]
plot(x=as.vector(trainData[,"VXX"]), y=as.vector(trainData[,"VXZ"]),
     main=paste("Hedge Regression: Y =", regression$coefficient[2], " * X + intercept"),
  	 xlab="Vxx Return", ylab="Vxz Return", pch=19)
abline(regression, col = 2 )

#--------------------------------------------------------------
### SECTION 3 - Generate trading signals ###
tSig <- Op(pnlEnv$VXX)/Op(pnlEnv$VXZ)
colnames(tSig) <- "Signal"
vxxSignal <- apply(tSig,1, function(x) {if(x<signalLowLim) { return (-1) } else { if(x>signalUpperLim) { return(1) } else { return (0) }}})
vxzSignal <- -1 * vxxSignal

strategyRet <- ((vxxSignal * pnlEnv$VXX$Ret) + hedgeratio * (vxzSignal * pnlEnv$VXZ$Ret) )
strategyRet <- window(strategyRet,start=tradingStartDate,end=tradingEndDate, extend = FALSE)
#Normalise the amount of money being invested on each trade so that we can compare to the S&P index later
strategyRet <- strategyRet * 1 / (1+abs(hedgeratio))
colnames(strategyRet) <- "StrategyReturns"

#--------------------------------------------------------------
### SECTION 5 - Performance Analysis ###

## Get the S&P 500 index data:
indexData <- pnlEnv
indexRet  <- (Cl(indexData$GSPC)-lag(Cl(indexData$GSPC),1))/lag(Cl(indexData$GSPC),1)
colnames(indexRet) <- "IndexRet"
pnlVec <- cbind(as.zoo(strategyRet),as.zoo(indexRet)) #Convert to zoo object
colnames(pnlVec) <- c("Vol Carry Trade","S&P500")
pnlVec <- na.omit(pnlVec)

charts.PerformanceSummary(pnlVec,main="Performance of Volatility Carry Trade",geometric=FALSE)
#Lets calculate a table of montly returns by year and strategy
cat("Calander Returns - Note 13.5 means a return of 13.5%\n")
print(table.CalendarReturns(pnlVec))

#Calculate the sharpe ratio
cat("Sharpe Ratio")
print(SharpeRatio.annualized(pnlVec))

#Calculate other statistics
cat("Other Statistics")
print(table.CAPM(pnlVec[,"Vol Carry Trade"],pnlVec[,"S&P500"]))
chart.Boxplot(pnlVec)
layout(rbind(c(1,2),c(3,4)))
chart.Histogram(pnlVec, main = "Plain", methods = NULL)
chart.Histogram(pnlVec, main = "Density", breaks=40, methods = c("add.density", "add.normal"))
chart.Histogram(pnlVec, main = "Skew and Kurt", methods = c("add.centered", "add.rug"))
chart.Histogram(pnlVec, main = "Risk Measures", methods = c("add.risk"))
layout(c(1,1))
```
