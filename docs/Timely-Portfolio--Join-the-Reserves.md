<!--yml

类别：未分类

日期：2024-05-18 15:12:47

-->

# 及时投资组合：加入储备

> 来源：[`timelyportfolio.blogspot.com/2011/07/join-reserves.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/07/join-reserves.html#0001-01-01)

大多数人忘记，由 10 万亿美元的外汇储备所引起的巨大宏观失衡只是一个 14 年的现象，但其影响已经并且将继续是深远的。购买行为开始于 1997 年亚洲金融危机之后，亚洲中央银行选择持续进行一种不同于伯南克的量化宽松政策，其规模远超伯南克的 QE1 和 QE2。记得格林斯潘的“谜题”以及美联储利率上升无法推动长期利率曲线走高。这些被人为抑制的利率说服了货币经理和机构寻求在新产品如 CDO 中取得更高回报，并激励了美国消费者对住房需求的额外增长。这些都是 2008 年崩溃的重要因素。

利率是一种非常有效的负反馈机制，有助于控制经济的周期性。当非市场力量抑制利率的正常运作时，宏观失衡可能会造成严重后果。不幸的是，似乎我们还没有吸取教训。

对我来说，所有最近媒体和公众对政治辩论的关注给我们的无能政治家一种控制的错觉，并使我们忘记市场，主要是亚洲中央银行的买家，决定了美国财政和货币政策的界限。我只希望美国能以某种方式维持我们视为理所当然的非常脆弱的信心。

[R 代码（点击下载）：](https://docs.google.com/leaf?id=0B2qp2r96khJPYTVlOWQxNTAtNmRlOC00Y2RkLThhOGUtMTZhMGExZWFlZmFm&hl=en_US)

```
#get reserve data from IMF
require(ggplot2)   url = "http://www.imf.org/external/np/sta/cofer/eng/cofer.csv"   cofer <- read.csv (url, skip=5)
cofer <- cofer[c(7:17),c(1,3:18)]
rownames(cofer) <- cofer[,1]
cofer <- cofer[,2:NCOL(cofer)]
#erase commas
col2cvt <- 1:NCOL(cofer)
cofer[,col2cvt] <- lapply(cofer[,col2cvt],
	function(x){as.numeric(gsub(",", "", x))}) 
#erase spaces
rownames(cofer) <- gsub(" ", "", rownames(cofer))
#get numeric
col2cvt <- 1:NCOL(cofer)
cofer[,col2cvt] <- lapply(cofer[,col2cvt],
	function(x){as.numeric(x)}) 
#get data frame and invert
cofer <- as.data.frame(t(cofer))
#convert years to dates to use
datestoformat <- rownames(cofer)
datestoformat <- as.Date(paste(substr(datestoformat,2,5),"-12-31",sep=""))
#prepare for ggplot
rownames(cofer) <- 1:NROW(cofer)
cofer <- cbind(datestoformat,cofer)
cofer_melt <- melt(cofer,id.vars=1)
colnames(cofer_melt) <- c("Date","Country","Amount")   #get area chart
jpeg(filename="oecd cofer reserves area chart.jpg",quality=100,
	width=6.25, height = 6.25,  units="in",res=96)
ggplot(cofer_melt,
	aes(x=Date,y=Amount,fill=Country)) + geom_area() +
	scale_fill_hue(l=40, c=65) + 
	opts(title="OECD Cofer Foreign Currency Reserves",
		panel.background = theme_rect(colour="gray"))
dev.off()
```

[由 Pretty R 在 inside-R.org 创建](http://www.inside-r.org/pretty-r "由 Pretty R 在 inside-R.org 创建")
