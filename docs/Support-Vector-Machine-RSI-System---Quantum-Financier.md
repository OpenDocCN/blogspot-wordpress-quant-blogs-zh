<!--yml

类别：未分类

日期：2024-05-18 14:04:43

-->

# 支持向量机 RSI 系统-量子金融家

> 来源：[`quantumfinancier.wordpress.com/2010/06/26/support-vector-machine-rsi-system/#0001-01-01`](https://quantumfinancier.wordpress.com/2010/06/26/support-vector-machine-rsi-system/#0001-01-01)

宁愿晚一点，就像承诺的那样，在[先前的帖子](https://quantumfinancier.wordpress.com/2010/06/10/svm-classification-using-rsi-from-various-lengths/)中讨论的 SVM 系统的 R 代码。

供记录，此代码基于[Max Dama 创建的随机森林系统。](http://www.maxdama.com/2009/05/decision-tree-bagging-system-r-code.html) 我认为这将使普通读者更容易比较和评估。我还想声明这与最佳编程方式相去甚远，我很久之前就写过了，当时我才刚开始学习 R。

这就是系统：

`SVMClassifModel = function(data, targets, returns, lookback = 252, ktype = "C-svc", crossvalid = 10, C = 10) {

# 使用支持向量机构建预测模型

# 输入数据必须滞后一期，以避免前瞻性偏差

# 打印预测结果和置信度、准确度、资产曲线图以及性能统计与基准对比`

# 库

require(kernlab)

require(quantmod)

# 确保目标是一个因子（用于分类）

targets = as.factor(targets)

data$targets = as.factor(data$targets)

# 生成回测指数

idx = data.frame(targets = lookback:(nrow(data)-1))

# 隔离后续使用的指数

inx = index(returns[idx$targets])

# 用于回测的预测函数

pred1pd = function(t) {

# 训练模型

model = trainSVM(data[(t-lookback):t, ], ktype, C, crossvalid)

# 预测

pred = predict(model, data[t+1, -1], type="prob")

# 用户检查打印

打印预测结果

}

# 循环遍历先前生成的日历进行回测

preds = sapply(idx$targets, pred1pd)

# 打印输出

打印预测结果

打印(max.col(preds))

preds = data.frame(t(rbind(mle = max.col(t(preds)), preds)))

打印预测结果

打印摘要统计信息((returns[idx$targets] * (preds$mle*2-3)), returns[idx$targets], comp = TRUE))

#资产曲线

equity = xts(cumprod((returns[idx$targets] * (preds$mle*2-3))+1), inx)

Benchmark = xts(cumprod(returns[idx$targets] + 1), inx)

# y 轴值范围

yrngMin = abs(min(equity, Benchmark))

yrngMax = abs(max(equity, Benchmark))

# 绘制曲线

chartSeries(equity, log.scale = TRUE, name='Equity Curves', yrange=c(yrngMin, yrngMax))

addTA(Benchmark, on=1, col='gold')

}

trainSVM = function(data, ktype, C, crossvalid) {

# 返回一个训练好的支持向量机模型

trainedmodel = ksvm(targets ~ ., data = data, type = ktype, kernel="rbfdot", kpar=list(sigma=0.05), C = C, prob.model = TRUE, cross = crossvalid)

}

特征生成函数(sym, returns) {

# 返回一个数据框，供支持向量机系统使用

# 目标向量

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

# 延迟的 RSI 以对应于目标周期的 RSI

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

# 数据框

data = data.frame(targets, rsi2, rsi3, rsi4, rsi5, rsi6, rsi7, rsi8, rsi9, rsi10, rsi11, rsi12, rsi13, rsi14, rsi15, rsi16, rsi17, rsi18, rsi19, rsi20, rsi21, rsi22, rsi23, rsi24, rsi25, rsi26, rsi27, rsi28, rsi29, rsi30)

# names(data) = c("目标", "数据")

# 结果

返回数据

}

summaryStats = function(x, bmk, comp = FALSE) {

#所需库

require(PerformanceAnalytics)

#计算策略的感兴趣的统计数据

cumRetx = Return.cumulative(x)

annRetx = Return.annualized(x, scale=252)

sharpex = SharpeRatio.annualized(x, scale=252)

winpctx = length(x[x > 0])/length(x[x != 0])

annSDx = sd.annualized(x, scale=252)

maxDDx = maxDrawdown(x)

avDDx = mean(Drawdowns(x))

if(comp == TRUE) {

#计算基准的统计数据

cumRetbmk = Return.cumulative(bmk)

annRetbmk = Return.annualized(bmk, scale=252)

sharpebmk = SharpeRatio.annualized(bmk, scale=252)

winpctbmk = length(bmk[bmk > 0])/length(bmk)

annSDbmk = sd.annualized(bmk, scale=252)

maxDDbmk = maxDrawdown(bmk)

avDDbmk = mean(Drawdowns(bmk))

#返回结果向量

Benchmark = c(cumRetbmk, annRetbmk, sharpebmk, winpctbmk, annSDbmk, maxDDbmk, avDDbmk)

Strategy = c(cumRetx, annRetx, sharpex, winpctx, annSDx, maxDDx, avDDx)

nms = c("累积回报", "年化回报", "年化夏普比率", "获胜百分比", "年化波动率", "最大回撤", "平均回撤")

result = data.frame(Strategy, Benchmark, row.names = nms)

} else {

#返回结果向量

nms = c("累积回报", "年化回报", "年化夏普比率", "获胜百分比", "年化波动率", "最大回撤", "平均回撤")

策略 Strategy = c(累积回报, 年回报, 夏普比率, 胜率, 年标准差, 最大回撤, 平均回撤)

结果 = 数据框(策略, 行名 = nms)

]}

返回(结果)

]}

这里是要使用的系统 harness。别忘了修改代码的第一行，将其替换为你的目录。

> 例如:
> 
> 设置工作目录 setwd("C:\Users\John Doe\Documents")
> 
> 源("SVM 系统")

`setwd("INPUT DIRECTORY")`

源("RSI 系统文件名")

需要(quantmod)

需要(PerformanceAnalytics)

# 使用 quantmod 加载数据

获取 SPY 数据 getSymbols('SPY', from='2000-06-01')

返回值 returns = dailyReturn(Cl(SPY), type='log')

# 生成数据框 data 和目标值 targets

数据 = featureGen(SPY, returns)

目标值 targets = coredata(returns)

目标值 targets[targets>=0] = 1

目标值 targets[targets<0] = -1

目标值 targets = as.factor(targets)

# 运行系统

SVMClassifModel(数据[30:nrow(数据),], 目标值[30:length(目标值)], 返回值, lookback = 252, ktype = "C-svc", crossvalid = 10, C = 60)

最后我想知道是否有人有更好的方法可以分享代码。这并不是一个很好的方法，我希望能改进它。我也欢迎建议来提高代码的效率。我还想明确指出，我认为这不是一个很好的系统，我知道通过添加预测因子等可以改进，这只是为了提供一个例子，以便在上面的帖子中跟进。

量化因子 QF
