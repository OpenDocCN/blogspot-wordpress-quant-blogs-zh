<!--yml
category: 未分类
date: 2024-05-18 15:11:52
-->

# Timely Portfolio: Performance with ggplot2

> 来源：[http://timelyportfolio.blogspot.com/2011/09/performance-with-ggplot2.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/09/performance-with-ggplot2.html#0001-01-01)

```
require(quantmod)
require(ggplot2)
require(PerformanceAnalytics)   clientPerf <- read.csv("clientperf.csv",stringsAsFactors=FALSE)
clientPerf[,2:NCOL(clientPerf)] <- lapply(clientPerf[,2:NCOL(clientPerf)],as.numeric)
clientPerf <- as.xts(clientPerf[,2:NCOL(clientPerf)]/100,
	order.by = as.Date(clientPerf[,1],format="%m-%d-%y"))
colnames(clientPerf) <- c("Client","BarclaysAgg","SP500")     returns.cumul <- xts(apply((1+clientPerf),MARGIN=2,FUN=cumprod),order.by=index(clientPerf))
returns.cumul.Melt <- melt(as.data.frame(cbind(index(returns.cumul),
	coredata(returns.cumul))),id.vars=1)
colnames(returns.cumul.Melt) <- c("Date","Portfolio","Growth")
a<-ggplot(returns.cumul.Melt,stat="identity",
	aes(x=Date,y=Growth,colour=Portfolio)) +
	geom_line(lwd=1) + 
	scale_x_date() +
	scale_colour_manual(values=c("cadetblue","darkolivegreen3","gray70","bisque3","purple")) +
	theme_bw() + 
	labs(x = "", y = "") +
	opts(title = "Cumulative Returns",plot.title = theme_text(size = 20, hjust = 0))   returnTable <- table.TrailingPeriods(clientPerf,
	periods=c(12,24,36,NROW(clientPerf)),
	FUNCS="Return.annualized")
rownames(returnTable) <- c(paste(c(1:3)," Year",sep=""),"Since Inception")
returnMelt <- melt(cbind(rownames(returnTable),returnTable*100))
colnames(returnMelt)<-c("Period","Portfolio","Value")
b<-ggplot(returnMelt, stat="identity", 
	aes(x=Period,y=Value,fill=Portfolio)) +
	geom_bar(position="dodge") +
	scale_fill_manual(values=c("cadetblue","darkolivegreen3","gray70")) +
	theme_bw() + 
	labs(x = "", y = "") +	
	opts(title = "Returns (annualized)",plot.title = theme_text(size = 20, hjust = 0))     downsideTable<-table.DownsideRisk(clientPerf)[c(1,3,5,7,8),]
downsideMelt<-melt(cbind(rownames(downsideTable),
	downsideTable))
colnames(downsideMelt)<-c("Statistic","Portfolio","Value")
c<-ggplot(downsideMelt, stat="identity", 
	aes(x=Statistic,y=Value,fill=Portfolio)) +
	geom_bar(position="dodge") + coord_flip() +
	scale_fill_manual(values=c("cadetblue","darkolivegreen3","gray70")) +
	theme_bw() + 
	labs(x = "", y = "") +
	opts(title = "Risk Measures",plot.title = theme_text(size = 20, hjust = 0)) 
	#geom_hline(aes(y = 0))
	#opts(axis.line = theme_segment(colour = "red"))
	#opts(panel.grid.major = theme_line(linetype = "dotted"))   #jpeg(filename="performance ggplot.jpg",quality=100,width=6.5, height = 8,  units="in",res=96)
#pdf("perf ggplot.pdf", width = 8.5, height = 11)   grid.newpage()
pushViewport(viewport(layout = grid.layout(3, 1)))   vplayout <- function(x, y) 
  viewport(layout.pos.row = x, layout.pos.col = y)
print(a, vp = vplayout(1, 1))
print(b, vp = vplayout(2, 1))
print(c, vp = vplayout(3, 1))
#dev.off()
```