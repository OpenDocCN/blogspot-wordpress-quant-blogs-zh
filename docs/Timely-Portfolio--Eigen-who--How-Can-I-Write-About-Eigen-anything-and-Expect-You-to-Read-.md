<!--yml

分类：未分类

日期：2024-05-18 15:15:33

-->

# 及时投资组合：Eigen-谁？我怎么才能写关于 Eigen-任何东西并期望你阅读？

> 来源：[`timelyportfolio.blogspot.com/2011/05/eigen-who-how-can-i-write-about-eigen.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/05/eigen-who-how-can-i-write-about-eigen.html#0001-01-01)

```
#explain basics of principal component analysis
#by showing the various methods of charting eigenvalues
#of currency data   #give specific credit to Michael Friendly
#and his paper http://www.math.yorku.ca/SCS/Papers/corrgram.pdf
#another example of similar techniques used for both
#baseball and finance   #for additional information on principal component analysis (PCA)
#see http://en.wikipedia.org/wiki/Principal_component_analysis   require(quantmod)   #get currency data from the FED FRED data series
Korea <- getSymbols("DEXKOUS",src="FRED",auto.assign=FALSE) #load Korea
Malaysia <- getSymbols("DEXMAUS",src="FRED",auto.assign=FALSE) #load Malaysia
Singapore <- getSymbols("DEXSIUS",src="FRED",auto.assign=FALSE) #load Singapore
Taiwan <- getSymbols("DEXTAUS",src="FRED",auto.assign=FALSE) #load Taiwan
China <- getSymbols("DEXCHUS",src="FRED",auto.assign=FALSE) #load China
Japan <- getSymbols("DEXJPUS",src="FRED",auto.assign=FALSE) #load Japan
Thailand <- getSymbols("DEXTHUS",src="FRED",auto.assign=FALSE) #load Thailand
Brazil <- getSymbols("DEXBZUS",src="FRED",auto.assign=FALSE) #load Brazil
Mexico <- getSymbols("DEXMXUS",src="FRED",auto.assign=FALSE) #load Mexico
India <- getSymbols("DEXINUS",src="FRED",auto.assign=FALSE) #load India
USDOther <- getSymbols("DTWEXO",src="FRED",auto.assign=FALSE) #load US Dollar Other Trading Partners
USDBroad <- getSymbols("DTWEXB",src="FRED",auto.assign=FALSE) #load US Dollar Broad   #combine all the currencies into one big currency xts
currencies<-merge(Korea, Malaysia, Singapore, Taiwan,
	China, Japan, Thailand, Brazil, Mexico, India,
	USDOther, USDBroad)
currencies<-na.omit(currencies)
colnames(currencies)<-c("Korea", "Malaysia", "Singapore", "Taiwan",
	"China", "Japan", "Thailand", "Brazil", "Mexico", "India",
	"USDOther", "USDBroad")
#get daily percent changes
currencies<-currencies/lag(currencies)-1       #using fAssets
require(fAssets)
assetsCorEigenPlot(as.timeSeries(currencies))       #using techniques from corrgram package documentation
#get correlation matrix
(currencies.cor <- cor(currencies,use="pair"))
#get two largest eigenvectors
(currencies.eig<-eigen(currencies.cor)$vectors[,1:2])
e1 <- currencies.eig[,1]
e2 <- currencies.eig[,2]
#make the chart
plot(e1,e2,col='white', xlim=range(e1,e2), ylim=range(e1,e2),
	main="Plot of 2 Largest Eigenvectors for Various Asian 
	and American Currencies (corrgram)")
arrows(0, 0, e1, e2, cex=0.5, col="red", length=0.1)
text(e1,e2, rownames(currencies.cor), cex=0.75)
#run an interesting corrgram chart
require(corrgram) #do not need for previous eigenvector plot
df1 <- data.frame(cbind(index(currencies),coredata(currencies)))
corrgram(df1, order=TRUE, 
          main="Currency data PC2/PC1 order",
          lower.panel=panel.shade, upper.panel=panel.pie,
          text.panel=panel.txt)       #using techniques from SciViews package
#do principal component analysis
require(SciViews)
(currencies.pca <- pcomp(~Korea + Malaysia + Singapore + Taiwan +
	China + Japan + Thailand + Brazil + Mexico + India +
	USDOther + USDBroad,
	data = currencies))
#make the chart
plot(currencies.pca, which = "correlations",
	main="Plot of 2 Largest Eigenvectors for Various Asian 
	and American Currencies (SciViews)")
#more SciViews fun
#summary(currencies.pca)
#screeplot(currencies.pca)
#currencies.ldg<-loadings(currencies.pca)
#(currencies.cor <- correlation(currencies.pca))
#plot(currencies.pca, which = "scores", cex = 0.8)
#pairs(currencies.pca)         #compare 2 largest eigenvectors from the sciview and corrgram
cbind(loadings(currencies.pca)[,1],e1,loadings(currencies.pca)[,2],e2)
```
