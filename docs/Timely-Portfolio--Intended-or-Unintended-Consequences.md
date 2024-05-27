<!--yml

分类：未分类

日期：2024-05-18 14:59:48

-->

# Timely Portfolio：有意图或无意图的后果

> 来源：[`timelyportfolio.blogspot.com/2013/05/intended-or-unintended-consequences.html#0001-01-01`](http://timelyportfolio.blogspot.com/2013/05/intended-or-unintended-consequences.html#0001-01-01)

自 2000 年以来，美国 10 年期国债收益率似乎温和，波动性低，总体呈下降趋势。

```
require(latticeExtra)
require(quantmod)

US10y <- getSymbols("^TNX", from = "2000-01-01", auto.assign = FALSE)[, 
    4]

asTheEconomist(xyplot(US10y, scales = list(y = list(rot = 1)), 
    main = "US 10y Yield Since 2000")) 
```

然而，如果我们绘制 252 天或 1 年内的利率变化，我们可能会怀疑利率是否像我们最初推测的那样温和。尽管这可能看起来是美国联邦储备银行积极货币宽松的可以接受的预期后果，但我担心我们将面临历史上正常的无意图后果。

```
p1 <- asTheEconomist(xyplot(US10y - lag(US10y, 252), 
    scales = list(y = list(rot = 0)), main = "US 10y Yield - Yearly Change"))
p1 
```

如果我们使用一些先锋美国债券基金（vbmfx 和 vustx）作为美国债券市场的代理[逼近零界限 - 债券](http://timelyportfolio.blogspot.com/2013/01/approaching-zero-bound-bonds.html)，我们会发现现在市场与过去 4 年不同。

```
require(directlabels)
require(reshape2)

getSymbols("VUSTX", from = "1990-01-01") 
```

```
## [1] "VUSTX" 
```

```
getSymbols("VBMFX", from = "1990-01-01") 
```

```
## [1] "VBMFX" 
```

```
 bonds.tr <- merge(ROC(VUSTX[, 6], 250), ROC(VBMFX[, 
    6], 250))
colnames(bonds.tr) <- c("VanguardLongTsy", "VanguardTotBnd")
bond.funds.melt <- melt(as.data.frame(cbind(as.Date(index(bonds.tr)), 
    coredata(bonds.tr))), id.vars = 1)
colnames(bond.funds.melt) <- c("date", "fund", "totret250")
bond.funds.melt$date <- as.Date(bond.funds.melt$date)

p2 <- direct.label(xyplot(bonds.tr, screens = 1, ylim = c(-0.35, 
    0.35), scales = list(y = list(rot = 0)), col = theEconomist.theme()$superpose.line$col, 
    par.settings = theEconomist.theme(box = "transparent"), 
    lattice.options = theEconomist.opts(), xlab = NULL, 
    main = "Vanguard Bond Funds 250 Day Total Return"), 
    list("last.points", hjust = 1, cex = 1.2))
p2 
```

```
 p3 <- asTheEconomist(horizonplot(totret250 ~ date | 
    fund, origin = 0, horizonscale = 0.05, data = bond.funds.melt, 
    strip = TRUE, strip.left = FALSE, par.strip.text = list(cex = 1.1), 
    layout = c(1, 2), main = "Vanguard Bond Funds 250 Day Total Return"))
p3 
```

```
 # print(p2,position=c(0,0.4,1,1),more=TRUE)
# print(update(p3,main=NULL),position=c(0,0,1,0.5)) 
```

### 与日本的比较

为了参考，让我们看看最近在媒体上受到较多关注的一个国家。我们可以将美国的收益率添加到我的最爱图表中，来自[日本 - JGB 收益率更多格子图](http://timelyportfolio.blogspot.com/2013/05/japan-jgb-yieldsmore-lattice-charts.html)。大部分差异在于曲线的短端，其中美国自 2012 年以来仍然接近最低点，而日本则接近 7 年期的最高点。

```
url <- "http://www.mof.go.jp/english/jgbs/reference/interest_rate/"
filenames <- paste("jgbcme",c("","_2010","_2000-2009","_1990-1999","_1980-1989","_1974-1979"),".csv",sep="")

#load all data and combine into one jgb data.frame
jgb <- read.csv(paste(url,filenames[1],sep=""),stringsAsFactors=FALSE)
for (i in 2:length(filenames)) {
  jgb <- rbind(jgb,read.csv(paste(url,"/historical/",filenames[i],sep=""),stringsAsFactors=FALSE))
}

#now clean up the jgb data.frame to make a jgb xts
jgb.xts <- as.xts(data.matrix(jgb[,2:NCOL(jgb)]),order.by=as.Date(jgb[,1]))
colnames(jgb.xts) <- paste0(gsub("X","JGB",colnames(jgb.xts)))

#get Yen from the Fed
#getSymbols("DEXJPUS",src="FRED")

xtsMelt <- function(data) {
  require(reshape2)

  #translate xts to time series to json with date and data
  #for this behavior will be more generic than the original
  #data will not be transformed, so template.rmd will be changed to reflect

  #convert to data frame
  data.df <- data.frame(cbind(format(index(data),"%Y-%m-%d"),coredata(data)))
  colnames(data.df)[1] = "date"
  data.melt <- melt(data.df,id.vars=1,stringsAsFactors=FALSE)
  colnames(data.melt) <- c("date","indexname","value")
  #remove periods from indexnames to prevent javascript confusion
  #these . usually come from spaces in the colnames when melted
  data.melt[,"indexname"] <- apply(matrix(data.melt[,"indexname"]),2,gsub,pattern="[.]",replacement="")
  return(data.melt)
  #return(df2json(na.omit(data.melt)))

}

jgb.melt <- xtsMelt(jgb.xts["2012::",])
jgb.melt$date <- as.Date(jgb.melt$date)
jgb.melt$value <- as.numeric(jgb.melt$value)
jgb.melt$indexname <- factor(
  jgb.melt$indexname,
  levels = colnames(jgb.xts)
)
jgb.melt$maturity <- as.numeric(
  substr(
    jgb.melt$indexname,
    4,
    length( jgb.melt$indexname ) - 4
  )
)
jgb.melt$country <- rep( "Japan", nrow( jgb.melt ))

#now get the US bonds from FRED
USbondssymbols <- paste0("DGS",c(1,2,3,5,7,10,20,30))

ust.xts <- xts()
for (i in 1:length( USbondssymbols ) ) {
  ust.xts <- merge( 
    ust.xts,
    getSymbols( 
     USbondssymbols[i],
     auto.assign = FALSE,
     src = "FRED"
    )
  )
}

ust.melt <- na.omit( xtsMelt( ust.xts["2012::",] ) )

ust.melt$date <- as.Date(ust.melt$date)
ust.melt$value <- as.numeric(ust.melt$value)
ust.melt$indexname <- factor(
  ust.melt$indexname,
  levels = colnames(ust.xts)
)
ust.melt$maturity <- as.numeric(
  substr(
    ust.melt$indexname,
    4,
    length( ust.melt$indexname ) - 4
  )
)
ust.melt$country <- rep( "US", nrow( ust.melt ))

bonds.melt <- rbind( jgb.melt, ust.melt )

p4 <- xyplot(
  value ~ date | maturity,
  groups = country,
  data = bonds.melt,
  type = "l",
  col = c(brewer.pal(9,"Blues")[5],brewer.pal(9,"Blues")[7]),
  layout = c( length( unique( bonds.melt$maturity ) ), 1 ),
  panel = function(x, y, subscripts, col, ...) {
    panel.abline(
      h = c( 
        sapply( by( y, bonds.melt[subscripts,"country"], summary ), min ),
        sapply( by( y, bonds.melt[subscripts,"country"], summary ), max )
      ),
      #if(!col){
      col = col[1:length(unique(bonds.melt[subscripts,"country"]))]
      #} else col = trellis.par.get()$superpose.line$col[1:length(unique(bonds.melt[subscripts,"country"]))]
    )
    panel.xyplot( x = x, y = y, subscripts = subscripts, col = col, ... )
    panel.text(
      x = x[ length(unique(x)) / 2],
      y = mean(
        c(
          sapply( by( y, bonds.melt[subscripts,"country"], summary ), max )[1],
          sapply( by( y, bonds.melt[subscripts,"country"], summary ), min )[2]
        )
      ),
      labels = paste0(unique(bonds.melt$maturity)[panel.number()],"y"),
      cex = 0.8,
      #font = 2,
      col = "black",
      adj = c(0.5,0.5)
    )
  },
  scales = list( 
    x = list(
      draw = FALSE
      #tck = c(1,0),
      #alternating = 1,
      #at = min(bonds.melt$date),
      #labels = format(min(bonds.melt$date),"%Y")
    ),
    y = list( tck = c(1,0), lwd = c(0,1) )
  ),
  strip = FALSE,
  par.settings = list(axis.line = list(col = 0)),
  xlab = NULL,
  ylab = "Yield",
  main = "JGB and US Yields by Maturity Since Jan 2012"
)
p4 <- p4 + layer(
  panel.abline(
    h = pretty(bonds.melt$value,4),
    lty = 3
  )
)
p4 
```

### 复制

Gist 源代码：

[`gist.github.com/timelyportfolio/5665790`](https://gist.github.com/timelyportfolio/5665790)
