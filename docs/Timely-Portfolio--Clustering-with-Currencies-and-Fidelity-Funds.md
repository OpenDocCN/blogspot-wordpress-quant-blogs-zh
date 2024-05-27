<!--yml

category: 未分类

date: 2024-05-18 15:15:28

-->

# 及时投资组合：货币和忠诚基金聚类

> 来源：[`timelyportfolio.blogspot.com/2011/05/clustering-with-currencies-and-fidelity.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/05/clustering-with-currencies-and-fidelity.html#0001-01-01)

```
#extends post on principal component analysis with MODist
#using example from http://www.rinfinance.com/agenda/2011/StefanoIacus.pdf
#on currency data and fidelity mutual fund data   require(quantmod)   #get currency data from the FED FRED data series
Korea  <-  getSymbols("DEXKOUS",src="FRED",auto.assign=FALSE) #load Korea
Malaysia  <-  getSymbols("DEXMAUS",src="FRED",auto.assign=FALSE) #load Malaysia
Singapore  <-  getSymbols("DEXSIUS",src="FRED",auto.assign=FALSE) #load Singapore
Taiwan  <-  getSymbols("DEXTAUS",src="FRED",auto.assign=FALSE) #load Taiwan
China  <-  getSymbols("DEXCHUS",src="FRED",auto.assign=FALSE) #load China
Japan  <-  getSymbols("DEXJPUS",src="FRED",auto.assign=FALSE) #load Japan
Thailand  <-  getSymbols("DEXTHUS",src="FRED",auto.assign=FALSE) #load Thailand
Brazil  <-  getSymbols("DEXBZUS",src="FRED",auto.assign=FALSE) #load Brazil
Mexico  <-  getSymbols("DEXMXUS",src="FRED",auto.assign=FALSE) #load Mexico
India  <-  getSymbols("DEXINUS",src="FRED",auto.assign=FALSE) #load India
USDOther  <-  getSymbols("DTWEXO",src="FRED",auto.assign=FALSE) #load US Dollar Other Trading Partners
USDBroad  <-  getSymbols("DTWEXB",src="FRED",auto.assign=FALSE) #load US Dollar Broad       #combine all the currencies into one big currency xts
currencies <- merge(Korea, Malaysia, Singapore, Taiwan,
	China, Japan, Thailand, Brazil, Mexico, India,
	USDOther, USDBroad)
currencies <- na.omit(currencies)
colnames(currencies) <- c("Korea", "Malaysia", "Singapore", "Taiwan",
	"China", "Japan", "Thailand", "Brazil", "Mexico", "India",
	"USDOther", "USDBroad")       #use MODist package as described in the fine presentation
#http://www.rinfinance.com/agenda/2011/StefanoIacus.pdf
require(sde)   currencies <- as.zoo(currencies)
d  <-  MOdist(currencies)
cl  <-  hclust( d )
groups  <-  cutree(cl, k=4)
plot(currencies, col=groups, main="Various Asian and American Currencies
	1995-Current")
cmd  <-  cmdscale(d)
colnames(cmd)  <-  c("first coordinate","second coordinate")
plot( cmd, col=groups, main="MODist of Various Asian and American Currencies
	1995-Current" )
text( cmd, labels(d) , col=groups)   #struggling with whether price or percent change works better
#run again with percentage change
currencies <- ROC(currencies,1,type="discrete")
currencies[1,1:NCOL(currencies)] <- 0
currencies <- as.zoo(currencies)
d  <-  MOdist(currencies)
cl  <-  hclust( d )
groups  <-  cutree(cl, k=4)
cmd  <-  cmdscale(d)
colnames(cmd)  <-  c("first coordinate","second coordinate")
plot( cmd, col=groups, main="MODist of Various Asian and American Currencies
	Percentage Change 1995-Current" )
text( cmd, labels(d) , col=groups)     #do the same MODist for some Fidelity Funds
#except just use price change rather than price
tckr<-c("FBGRX","FCNTX","FDGFX","FEQIX","FEXPX",
	"FFTYX","FFIDX","FDGRX","FDEGX","FLCSX",
	"FMCSX","FOCPX","FDVLX","FSLSX","FIVFX",
	"FOSFX","FRESX","FSEMX","FSTMX","FPURX")
start<-"1990-01-01"
end<- format(Sys.Date(),"%Y-%m-%d") # yyyy-mm-dd   # Pull tckr index data from Yahoo! Finance
getSymbols(tckr, from=start, to=end, adjust=TRUE)   fidelity<-na.omit(merge(to.weekly(FBGRX)[,4],to.weekly(FCNTX)[,4],
	to.weekly(FDGFX)[,4] ,to.weekly(FEQIX)[,4],
	to.weekly(FEXPX)[,4] , to.weekly(FFTYX)[,4],
	to.weekly(FFIDX)[,4] , to.weekly(FDGRX)[,4],
	to.weekly(FDEGX)[,4] , to.weekly(FLCSX)[,4],
	to.weekly(FMCSX)[,4] , to.weekly(FOCPX)[,4],
	to.weekly(FDVLX)[,4] , to.weekly(FSLSX)[,4],	
	to.weekly(FIVFX)[,4] , to.weekly(FOSFX)[,4],
	to.weekly(FRESX)[,4] , to.weekly(FSEMX)[,4],
	to.weekly(FSTMX)[,4] , to.weekly(FPURX)[,4]))   colnames(fidelity) <- substr(colnames(fidelity),1,5)   fidelity <- ROC(fidelity,1,type="discrete")
fidelity[1,1:NCOL(fidelity)] <- 0
fidelity <- as.zoo(fidelity)   d  <-  MOdist(fidelity)
cl  <-  hclust( d )
groups  <-  cutree(cl, k=5)
plot(fidelity, col=groups, main="Various Fidelity Mutual Funds
	1998-Current")
cmd  <-  cmdscale(d)
colnames(cmd)  <-  c("first coordinate","second coordinate")
plot( cmd, col=groups, main="MODist of Various Fidelity Mutual Funds
	1995-Current" )
text( cmd, labels(d) , col=groups)   #get plot of eigenvalues since we have not done in any
#previous posts
#using techniques from corrgram package documentation
#get correlation matrix
(fidelity.cor <- cor(fidelity,use="pair"))
#get two largest eigenvectors
(fidelity.eig <- eigen(fidelity.cor)$vectors[,1:2])
e1 <- fidelity.eig[,1]
e2 <- fidelity.eig[,2]
#make the chart
plot(e1,e2,col='white', xlim=range(e1,e2), ylim=range(e1,e2),
	main="Plot of 2 Largest Eigenvectors for Various Fidelity Funds")
arrows(0, 0, e1, e2, cex=0.5, col=groups, length=0.1)
text(e1,e2, rownames(fidelity.cor), cex=0.75, col=groups)
```
