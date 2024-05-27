<!--yml

类别：未分类

日期：2024-05-18 15:11:48

-->

# Timely Portfolio: ttrTests：它的伟大论文和惊人的潜力

> 来源：[`timelyportfolio.blogspot.com/2011/09/ttrtests-its-great-thesis-and.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/09/ttrtests-its-great-thesis-and.html#0001-01-01)

我在我的帖子[ttrTests 实验](http://timelyportfolio.blogspot.com/2011/08/ttrtests-experimentation.html)中提到了 ttrTests R 包。直到我花更多时间吸收该包的基础知识——David St. John 的论文[基于移动平均收敛和发散的技术分析](http://math.uic.edu/~dstjohn/thesis.pdf)，我才意识到它的潜力。由于论文的标题特别提到了 MACD，而我在这方面运气不佳，所以我忽略了大部分内容。然而，论文的力量远远超出了 MACD，适用于所有系统性方法，并描述了确保运气不是系统回报来源的测试。在包文档中，有 5 个主要测试的摘要：

> “包含五个主要测试以及其他功能的支持：TTR 策略在过去数据中超越了基准吗？使用自助法构建置信区间，超额回报是否显著？超额回报是否由数据窥探解释？参数’良好’的选择在子样本中是否稳健？这种稳健性是否显著，使用自助法构建置信区间？”

测试揭示了运气、数据窥探、交易成本和参数持久性，跨越了自由度和子周期。我期待在我的博客中记录其力量，并可能与作者合作，将其包括在其他 R 包中，如 quantstrat。

由于我时间不多了，我首先想以与包文档和论文相同的风格将 MACD 应用于每个测试，但这次是在通过 getSymbols 获取的 xts DJI 对象上，而不是包中提供的 spData。

测试的输出非常繁琐，但我希望这套示例能帮助您了解该套餐及其强大的测试。在我的下一两篇帖子中，我将对我的基本自定义 CUD 指标进行更详细的每个测试，并尝试以更易消化和图形化的格式获取繁琐的输出。

[R 代码（点击从 Google Docs 下载）：](https://docs.google.com/leaf?id=0B2qp2r96khJPMDZjNjA3M2UtNDI2OS00NTRjLTg3ZjgtNzVlY2MxZDEzMmUz&hl=en_US)

```
require(ttrTests)
require(quantmod)   #get Dow Jones Industrials from Yahoo! Finance
getSymbols("^DJI",from="1896-01-01",to=Sys.Date())
#convert closing price to vector format which works best with ttrTests
DJI.vector <- as.vector(DJI[,4])   #using the defaults as mentioned in the thesis paper on MACD
#show each of the tests in order of their mention   #quotes are from ttrTests package documentation
#"compares the performance of the TTR with some benchmark"
returnStats(DJI.vector)   #"constructs a confidence interval for this performance"
#"and gives a p-value for the excess return observed in (1)."
nullModel(DJI.vector)   #"constructs a p-value for the ’best’ choice"
#"of parameters within a given domain"
dataSnoop(DJI.vector,bSamples=3,test="RC")
dataSnoop(DJI.vector,bSamples=3,test="SPA")   #"asks whether or not good choices of parameters"
#"were robust across different time periods"
#chose 8 since data is from 1928 will approximate by decade
subperiods(DJI.vector, periods=8)   #and my favorite of all
#"tests if the persistence measure from subperiods()"
#"is statistically significant"
#this takes the longest (about 10 minutes on my i7 laptop)
paramPersist(DJI.vector)
```

由 Pretty R at inside-R.org 创建](http://www.inside-r.org/pretty-r "Created by Pretty R at inside-R.org")
