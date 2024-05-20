<!--yml
category: 未分类
date: 2024-05-18 14:04:43
-->

# Support Vector Machine RSI System – Quantum Financier

> 来源：[https://quantumfinancier.wordpress.com/2010/06/26/support-vector-machine-rsi-system/#0001-01-01](https://quantumfinancier.wordpress.com/2010/06/26/support-vector-machine-rsi-system/#0001-01-01)

Better late than never, as promised, the R code for the SVM system discussed in a [previous post](https://quantumfinancier.wordpress.com/2010/06/10/svm-classification-using-rsi-from-various-lengths/).

For the record this code is based on the [random forest system created by Max Dama.](http://www.maxdama.com/2009/05/decision-tree-bagging-system-r-code.html) I thought that it would make it easier for common reader to compare and evaluate. I also want to state that this isn’t anywhere close to optimal programming, I did that I long time ago and I was only starting with R at the time.

Here is the system :

`SVMClassifModel = function(data, targets, returns, lookback = 252, ktype = "C-svc", crossvalid = 10, C = 10) {
# Construct a predictive model using support vector machine
# Input data must be lagged one period to avoid look-ahead bias
# Print predictions and confidence, accuracy, equity curves plot, and performance statistics v.s. benchmark`

# Libraries
require(kernlab)
require(quantmod)

# Make sure targets is a factor (for classification)
targets = as.factor(targets)
data$targets = as.factor(data$targets)

# Generate indexes for backtest
idx = data.frame(targets = lookback:(nrow(data)-1))

# Isolate index to be used later
inx = index(returns[idx$targets])

# Prediction function to be used for backtesting
pred1pd = function(t) {
# Train model
model = trainSVM(data[(t-lookback):t, ], ktype, C, crossvalid)
# Prediction
pred = predict(model, data[t+1, -1], type="prob")
# Print for user inspection
print(pred)
}

# backtest by looping over the calendar previously generated
preds = sapply(idx$targets, pred1pd)
# print output
print(preds)
print(max.col(preds))
preds = data.frame(t(rbind(mle = max.col(t(preds)), preds)))
print(preds)
print(summaryStats((returns[idx$targets] * (preds$mle*2-3)), returns[idx$targets], comp = TRUE))

#Equity curves
equity = xts(cumprod((returns[idx$targets] * (preds$mle*2-3))+1), inx)
Benchmark = xts(cumprod(returns[idx$targets] + 1), inx)

# y axis values range
yrngMin = abs(min(equity, Benchmark))
yrngMax = abs(max(equity, Benchmark))

# Plot curves
chartSeries(equity, log.scale = TRUE, name='Equity Curves', yrange=c(yrngMin, yrngMax))
addTA(Benchmark, on=1, col='gold')
}

trainSVM = function(data, ktype, C, crossvalid) {
# Return a trained svm model
trainedmodel = ksvm(targets ~ ., data = data, type = ktype, kernel="rbfdot", kpar=list(sigma=0.05), C = C, prob.model = TRUE, cross = crossvalid)
}

featureGen = function(sym, returns) {
# Return a data frame to be used as input by the SVM system

# Targets vector
targets = coredata(returns)
targets[targets>=0] = 1
targets[targets<0] = -1
targets = as.factor(targets)

#RSIs
rsi2 = RSI(Cl(sym), 2 )
rsi3 = RSI(Cl(sym), 3 )
rsi4 = RSI(Cl(sym), 4 )
rsi5 = RSI(Cl(sym), 5 )
rsi6 = RSI(Cl(sym), 6 )
rsi7 = RSI(Cl(sym), 7 )
rsi8 = RSI(Cl(sym), 8 )
rsi9 = RSI(Cl(sym), 9 )
rsi10 = RSI(Cl(sym), 10 )
rsi11 = RSI(Cl(sym), 11 )
rsi12 = RSI(Cl(sym), 12 )
rsi13 = RSI(Cl(sym), 13 )
rsi14 = RSI(Cl(sym), 14 )
rsi15 = RSI(Cl(sym), 15 )
rsi16 = RSI(Cl(sym), 16 )
rsi17 = RSI(Cl(sym), 17 )
rsi18 = RSI(Cl(sym), 18 )
rsi19 = RSI(Cl(sym), 19 )
rsi20 = RSI(Cl(sym), 20 )
rsi21 = RSI(Cl(sym), 21 )
rsi22 = RSI(Cl(sym), 22 )
rsi23 = RSI(Cl(sym), 23 )
rsi24 = RSI(Cl(sym), 24 )
rsi25 = RSI(Cl(sym), 25 )
rsi26 = RSI(Cl(sym), 26 )
rsi27 = RSI(Cl(sym), 27 )
rsi28 = RSI(Cl(sym), 28 )
rsi29 = RSI(Cl(sym), 29 )
rsi30 = RSI(Cl(sym), 30 )

# lagged RSIs to correspond RSI with target period
rsi2 = Lag(rsi2, 1)
rsi3 = Lag(rsi3, 1)
rsi4 = Lag(rsi4, 1)
rsi5 = Lag(rsi5, 1)
rsi6 = Lag(rsi6, 1)
rsi7 = Lag(rsi7, 1)
rsi8 = Lag(rsi8, 1)
rsi9 = Lag(rsi9, 1)
rsi10 = Lag(rsi10, 1)
rsi11 = Lag(rsi11, 1)
rsi12 = Lag(rsi12, 1)
rsi13 = Lag(rsi13, 1)
rsi14 = Lag(rsi14, 1)
rsi15 = Lag(rsi15, 1)
rsi16 = Lag(rsi16, 1)
rsi17 = Lag(rsi17, 1)
rsi18 = Lag(rsi18, 1)
rsi19 = Lag(rsi19, 1)
rsi20 = Lag(rsi20, 1)
rsi21 = Lag(rsi21, 1)
rsi22 = Lag(rsi22, 1)
rsi23 = Lag(rsi23, 1)
rsi24 = Lag(rsi24, 1)
rsi25 = Lag(rsi25, 1)
rsi26 = Lag(rsi26, 1)
rsi27 = Lag(rsi27, 1)
rsi28 = Lag(rsi28, 1)
rsi29 = Lag(rsi29, 1)
rsi30 = Lag(rsi30, 1)

# Data frame
data = data.frame(targets, rsi2, rsi3, rsi4, rsi5, rsi6, rsi7, rsi8, rsi9, rsi10, rsi11, rsi12, rsi13, rsi14, rsi15, rsi16, rsi17, rsi18, rsi19, rsi20, rsi21, rsi22, rsi23, rsi24, rsi25, rsi26, rsi27, rsi28, rsi29, rsi30)
# names(data) = c("targets", "data")

# Results
return(data)
}

summaryStats = function(x, bmk, comp = FALSE) {
#Required library
require(PerformanceAnalytics)

#Compute stats of interest for strategy
cumRetx = Return.cumulative(x)
annRetx = Return.annualized(x, scale=252)
sharpex = SharpeRatio.annualized(x, scale=252)
winpctx = length(x[x > 0])/length(x[x != 0])
annSDx = sd.annualized(x, scale=252)
maxDDx = maxDrawdown(x)
avDDx = mean(Drawdowns(x))

if(comp == TRUE) {
#Compute stats of interest for benchmark
cumRetbmk = Return.cumulative(bmk)
annRetbmk = Return.annualized(bmk, scale=252)
sharpebmk = SharpeRatio.annualized(bmk, scale=252)
winpctbmk = length(bmk[bmk > 0])/length(bmk)
annSDbmk = sd.annualized(bmk, scale=252)
maxDDbmk = maxDrawdown(bmk)
avDDbmk = mean(Drawdowns(bmk))
#Return result vectors
Benchmark = c(cumRetbmk, annRetbmk, sharpebmk, winpctbmk, annSDbmk, maxDDbmk, avDDbmk)
Strategy = c(cumRetx, annRetx, sharpex, winpctx, annSDx, maxDDx, avDDx)
nms = c("Cumulative Return", "Annualized Return", "Annualized Sharpe Ratio", "Winning Percentage", "Annualized Volatility", "Maximum Drawdown", "Average Drawdown")
result = data.frame(Strategy, Benchmark, row.names = nms)
} else {
#Return result vectors
nms = c("Cumulative Return", "Annualized Return", "Annualized Sharpe Ratio", "Winning Percentage", "Annualized Volatility", "Maximum Drawdown", "Average Drawdown")
Strategy = c(cumRetx, annRetx, sharpex, winpctx, annSDx, maxDDx, avDDx)
result = data.frame(Strategy, row.names = nms)
}
return(result)
}

Here is the harness used to use the system. Don’t forget to change the first two line of the code and replace with your directory.

> For example:
> setwd(“C:\Users\John Doe\Documents”)
> source(“SVM System”)

`setwd("INPUT DIRECTORY")
source("NAME OF THE RSI SYSTEM FILE IN THE FOLDER")
require(quantmod)
require(PerformanceAnalytics)`

# Load data with quantmod
getSymbols('SPY', from='2000-06-01')
returns = dailyReturn(Cl(SPY), type='log')

# Generate data frame of data and targets
data = featureGen(SPY, returns)
targets = coredata(returns)
targets[targets>=0] = 1
targets[targets<0] = -1
targets = as.factor(targets)

# Run the system
SVMClassifModel(data[30:nrow(data),], targets[30:length(targets)], returns, lookback = 252, ktype = "C-svc", crossvalid = 10, C = 60)

Lastly I would like to know if anyone has a better idea to share code. This is not very good way and I would like to improve it. I also welcome suggestions to make the code more efficient. I also want to make clear that I do not think that this is a good system and I know that it could be improved by adding predictors and all, it is only to give an example to follow-up on the post mentioned above.

QF