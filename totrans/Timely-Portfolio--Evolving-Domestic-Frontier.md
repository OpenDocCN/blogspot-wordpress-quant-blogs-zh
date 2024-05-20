<!--yml
category: 未分类
date: 2024-05-18 15:11:07
-->

# Timely Portfolio: Evolving Domestic Frontier

> 来源：[http://timelyportfolio.blogspot.com/2011/11/evolving-domestic-frontier.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/11/evolving-domestic-frontier.html#0001-01-01)

```
require(quantmod)
require(fPortfolio)
require(reshape)   #############################################################
#get data; unfortunately cannot share since I would violate
#copyright
sp_agg <- read.csv("C:\\Users\\Kent.TLEAVELL_NT\\Documents\\old\\R\\sp_agg.csv",stringsAsFactors=FALSE)
sp_agg <- sp_agg[2:NROW(sp_agg),3:NCOL(sp_agg)]
sp_agg <- sp_agg[,c(1,3,5)]   len <- nchar(sp_agg[,1])
xtsdate <- paste(substr(sp_agg[,1],len-3,len),"-",
	ifelse(len==9,"0",""),substr(sp_agg[,1],1,len-8),"-01",sep="")   sp_agg.xts <- xts(data.matrix(sp_agg[,2:NCOL(sp_agg)]),order.by=as.Date(xtsdate))
sp_agg.xts <- sp_agg.xts/100
#############################################################     #for svg
#require(Cairo)
#CairoSVG("frontier.svg", width=8 ,height=8 )
#jpeg(filename="evolving frontier.jpg",
#	quality=100,width=6, height = 7.5,  units="in",res=96)#############################################################
## spec -
   Spec = portfolioSpec()
   setTargetReturn(Spec) = mean(colMeans(as.timeSeries(sp_agg.xts)))   ## constraints -
   Constraints = "LongOnly"
#get frontiers by 5-year range
from = time(as.timeSeries(sp_agg.xts))[c(1,1,49,109,169,229,289,349,385)]
to = time(as.timeSeries(sp_agg.xts))[c(NROW(sp_agg.xts),48,108,168,228,288,348,NROW(sp_agg.xts)-8,NROW(sp_agg.xts)-8)]   rollFron <- rollingPortfolioFrontier(as.timeSeries(sp_agg.xts),Spec,Constraints,
	from=from,to=to)   #chartcol <- topo.colors(length(rollFron))
chartcol <- 1:length(rollFron)
#hindsight bias; yellow is too hard to read so change
chartcol[length(rollFron)-2] <- "goldenrod"     i=1
frontierPlot(rollFron[[1]],col=rep(chartcol[1],2),xlim=c(0,0.08),ylim=c(-0.01,0.025))
frontierlabels <- frontierPoints(rollFron[[i]])
text(x=frontierlabels[NROW(frontierlabels),1],y=frontierlabels[NROW(frontierlabels),2],
	labels=paste(from[i]," to ",to[i],sep=""),
	pos=4,offset=0.5,cex=0.5,col = chartcol[i])   for (i in 2:(length(rollFron)-3) ) {
	frontierPlot(rollFron[[i]],add=TRUE,col = rep(chartcol[i],2),pch=19,auto=FALSE,
		title=FALSE)
	frontierlabels <- frontierPoints(rollFron[[i]])
	text(x=frontierlabels[NROW(frontierlabels),1],y=frontierlabels[NROW(frontierlabels),2],
		labels=paste(from[i]," to ",to[i],sep=""),
		pos=4,offset=0.5,cex=0.5,col = chartcol[i])
}   i=7
lowerFrontier = frontierPoints(rollFron[[i]], frontier = "both")
points(lowerFrontier,col = rep(chartcol[i],2),pch=19)
frontierlabels <- frontierPoints(rollFron[[i]])
text(x=frontierlabels[1,1],y=frontierlabels[1,2],
	labels=paste(from[i]," to ",to[i],sep=""),
	pos=4,offset=0.5,cex=0.5,col = chartcol[i])     #legend("topright",legend=paste(from,to,sep=" "),pch=19,
#	col=chartcol,cex=0.7)
for (i in 8:length(rollFron)) {
	lowerFrontier = frontierPoints(rollFron[[i]], frontier = "lower")
	points(lowerFrontier,col = rep(chartcol[i],2),pch=19)
	frontierlabels <- frontierPoints(rollFron[[i]],frontier="lower")
	text(x=frontierlabels[1,1],y=frontierlabels[1,2],
		labels=paste(from[i]," to ",to[i],sep=""),
		pos=4,offset=0.5,cex=0.5,col = chartcol[i])
}
#
#frontier <- portfolioFrontier(as.timeSeries(sp_agg.xts))
#frontierPlot(frontier,col=rep(chartcol[length(rollFron)+1],2),add=TRUE,pch=19,auto=FALSE,
#		title=FALSE)   #dev.off()
```