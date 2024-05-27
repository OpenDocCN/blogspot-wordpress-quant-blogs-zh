<!--yml

分类：未分类

日期：2024-05-18 15:11:39

-->

# Timely Portfolio：ttrTests 这是一个测试 测试 3：Data Snoopy

> 来源：[`timelyportfolio.blogspot.com/2011/09/ttrtests-this-is-test-test-3data-snoopy.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/09/ttrtests-this-is-test-test-3data-snoopy.html#0001-01-01)

这不是投资建议。这只是一个例子，如果你追求讨论的内容，可能会损失很多钱。读者对自己的收益或损失负责。如果你是一个不太可能的赢家，我会很乐意听到你的故事。

当我们决定采用一个定量系统来指导我们的投资时，我们有多种选择，但都充满了潜在的运气：投资选择、系统类型、系统、时间框架、系统参数或参数以及资金管理。为了真正对您的选择的持久性有些信心，我认为应该尽可能地对每个选择进行严格测试。[`math.uic.edu/~dstjohn/thesis.pdf`](http://math.uic.edu/~dstjohn/thesis.pdf)、[`ageconsearch.umn.edu/bitstream/19039/1/cp05pa01.pdf`](http://ageconsearch.umn.edu/bitstream/19039/1/cp05pa01.pdf) 和 [`www.ssc.wisc.edu/~bhansen/718/White2000.pdf`](http://www.ssc.wisc.edu/~bhansen/718/White2000.pdf) 都提供了一些测试的非常好的讨论。我的帖子 [ttrTests This is a Test--Test 1 和 Test 2](http://timelyportfolio.blogspot.com/2011/09/ttrtests-this-is-test-test-1-and-test-2.html)、[ttrTests：Its Great Thesis and Incredible Potential](http://timelyportfolio.blogspot.com/2011/09/ttrtests-its-great-thesis-and.html) 和 [ttrTests Experimentation](http://timelyportfolio.blogspot.com/2011/08/ttrtests-experimentation.html) 提供了对这些远非简单的统计测试的简单应用。

我将对我的简单 CUD 指标的参数选择应用 dataSnoop 测试和汉森（Hansen）的优越预测能力（SPA）测试，以检查运气。

我不想这样做，但我想不出一个简单的方法来描述 dataSnoop 测试的输出，所以希望你能阅读 [`math.uic.edu/~dstjohn/thesis.pdf`](http://math.uic.edu/~dstjohn/thesis.pdf) 的第 51-57 页。 这是论文对应用于 MACD 系统时测试的描述。 ![clip_image001](http://math.uic.edu/~dstjohn/thesis.pdf)

[`math.uic.edu/~dstjohn/thesis.pdf`](http://math.uic.edu/~dstjohn/thesis.pdf) 第 55 页

我的 CUD 指标的 P 值不太好。

> CUD：观察到的均值 'l'、'c' 和 'u' 的 P 值分别为：0.4 0.4 0.97

测试的观察值如下图所示。

[R 代码（点击从 Google Docs 下载）：](https://docs.google.com/leaf?id=0B2qp2r96khJPMzFlZTMyNTUtNjhhZS00NmMyLWI0MGMtOTc5NDEwNjQ4YWQx&hl=en_US)

```
#let's define our silly countupdown function
#as a sample of a custom ttr rule
CUD <- function(x,params=50,...) {
	#CUD takes the n-period sum of 1 (up days) and -1 (down days)
	temp <- ifelse(runSum(ifelse(ROC(x,1,type="discrete") > 0,1,-1),params)>=0,1,0)
	#replace NA with 0 at beginning of period
	temp[is.na(temp)] <- 0
	temp
}   require(ttrTests)
require(quantmod)
require(lattice)
require(reshape2)
require(PerformanceAnalytics)   #defaults functions is overridden by ggplot2 and plyr if loaded
#and will cause problems if you want to use ttrTests concurrently   tckrs <- c("GSPC","RUT","N225","GDAXI","DJUBS")   #use 1 or GSPC but adjust however you would like
i=1
getSymbols(paste("^",tckrs[i],sep=""),from="1896-01-01",to=Sys.Date())
test_price <- as.vector(get(tckrs[i])[,4])   #run dataSnoop to test for luck
#by checking all parameters across multiple bootstrap samples
#this takes a long time, so for experimenting change bSamples to
#something smaller than 100
#if you are planning to use this for commercial purposes
#make sure you see the warning in the documentation
#on Dr. Halbert White's patent and his paper
#http://www.ssc.wisc.edu/~bhansen/718/White2000.pdf   #don't get me started on patents of this sort   #crit can be "sharpe", "return", or "adjust"
#will choose "sharpe" but feel free to try them all
snoop <- dataSnoop(x=test_price, ttr = CUD, start = 20, nSteps = 30, stepSize = 10,
	bSamples=100, crit="sharpe",
	restrict = FALSE, burn = 0, short = FALSE, condition = NULL,
	silent = TRUE, TC = 0.001, loud = TRUE, alpha = 0.025,
	begin = 1, percent = 1, file = "", benchmark = "hold")   #make output slightly more usable with some naming
#believe I got this right
names(snoop) <- c("details","V1","V2",
	"V3","p1.for.l","p2.for.c","p3.for.u")   #jpeg(filename="dataSnoop values.jpg",
	quality=100,width=6.25, height = 6.25,  units="in",res=96)
plot(snoop$V3,
	type="l", col=2,
	main="ttrTests dataSnoop V1,V2,and V3 on CUD",
	xlab="Bootstrap Sample", ylab="Values")
points(snoop$V2, type="l", col=3)
points(snoop$V1, col=4)
legend("topright",legend=c("V1","V2","V3"),col=c(4,3,2),pch=19,lty=1)
#dev.off()
```

[由 Pretty R 在 inside-R.org 创建](http://www.inside-r.org/pretty-r "由 Pretty R 在 inside-R.org 创建")
