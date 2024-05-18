<!--yml
category: 未分类
date: 2024-05-18 15:12:05
-->

# Timely Portfolio: Modest Modeest for Moving Average

> 来源：[http://timelyportfolio.blogspot.com/2011/08/modest-modeest-for-moving-average.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/08/modest-modeest-for-moving-average.html#0001-01-01)

```
require(modeest)
require(quantmod)
require(PerformanceAnalytics)   getSymbols("^GSPC",from="1896-01-01",to=Sys.Date())
GSPC.monthly <- to.monthly(GSPC)[,4]
index(GSPC.monthly) <- as.Date(index(GSPC.monthly))   #width will represent number of months for mode
width = 10
for (i in width:NROW(GSPC.monthly)) {
	#not real proud of this code
	#please feel free to comment with improvements
	m.default <- mlv(GSPC.monthly[(i-width):i])
	m.lientz <- mlv(GSPC.monthly[(i-width):i], method = "lientz", bw=0.01)
	m.hrm <- mlv(GSPC.monthly[(i-width):i], method = "hrm", bw=0.01)
	m.hsm <- mlv(GSPC.monthly[(i-width):i], method = "hsm",tie.action = "mean")
	m.grenander <- mlv(GSPC.monthly[(i-width):i], method = "grenander", p = 0.5)
	m.parzen <- mlv(GSPC.monthly[(i-width):i], method = "parzen", kernel = "gaussian")
	m.tsybakov <- mlv(GSPC.monthly[(i-width):i], method = "tsybakov")
	m.asselin <- mlv(GSPC.monthly[(i-width):i], method = "asselin")
	m.vieu <- mlv(GSPC.monthly[(i-width):i], method = "vieu")   m.all <- c(as.numeric(m.default[1]), as.numeric(m.lientz[1]),
		as.numeric(m.hrm[1]), as.numeric(m.hsm[1]), as.numeric(m.grenander[1]),
		as.numeric(m.parzen[1]), as.numeric(m.tsybakov[1]),
		as.numeric(m.asselin[1]), as.numeric(m.vieu[1]))
	ifelse(i==width, m.hist <- m.all, m.hist <- rbind(m.hist,m.all))
}   m.xts <- as.xts(as.data.frame(m.hist),order.by=index(GSPC.monthly[(width):NROW(GSPC.monthly),]))
m.xts <- merge(m.xts,runMean(GSPC.monthly,n=10),runMedian(GSPC.monthly,n=10))
colnames(m.xts) <- c("default","lientz","hrm","hsm","grenander","parzen",
	"tsybakov","asselin","vieu","mean","median")
GSPC.mode <- merge(GSPC.monthly,m.xts)   #there has to be a much cleaner way to accomplish this
signal <- GSPC.mode[,2:NCOL(GSPC.mode)]
ret <- GSPC.mode[,2:NCOL(GSPC.mode)]
for (i in 1:NCOL(signal)) {
	signal[,i] <- ifelse(GSPC.mode[,1] > GSPC.mode[,i+1],1,0)
	ret[,i] <- lag(signal[,i],k=1) * ROC(GSPC.mode[,1],type="discrete",n=1)
}
ret <- merge(ret,
	ROC(GSPC.mode[,1],type="discrete",n=1))   #jpeg(filename="modeest performance summary.jpg",
#	quality=100,width=6.25, height = 6.25,  units="in",res=96)
charts.PerformanceSummary(ret,ylog=TRUE,lwd=c(rep(2,9),rep(4,3)),
	main="Modeest System Comparison with Mean and Median")
#dev.off()   t(table.AnnualizedReturns(ret))   #jpeg(filename="modeest risk return.jpg",
#	quality=100,width=6.25, height = 6.25,  units="in",res=96)
chart.RiskReturnScatter(ret)
#dev.off()
```