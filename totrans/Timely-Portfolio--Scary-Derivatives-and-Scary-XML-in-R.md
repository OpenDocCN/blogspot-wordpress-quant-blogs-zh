<!--yml
category: 未分类
date: 2024-05-18 15:13:17
-->

# Timely Portfolio: Scary Derivatives and Scary XML in R

> 来源：[http://timelyportfolio.blogspot.com/2011/07/scary-derivatives-and-scary-xml-in-r.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/07/scary-derivatives-and-scary-xml-in-r.html#0001-01-01)

I need some new R skills, and there is no better motivation to learn XML in R than one of the scariest financial datasets out there—the US Department of the Treasury Office of the Comptroller of the Currency (OCC) Quarterly Derivatives Report. I’ll move to the even scarier global [BIS derivatives data](http://www.bis.org/publ/otc_hy1105.htm) in a later post to avoid inducing nightmares and sleepless nights.

The massive damage caused in 2008-2009 by the sliver of derivatives called credit default swaps seems like a faint warning siren when we see that they only represent < 7% of total derivatives exposure.  Interest rate and currency derivatives, also where I think the next disaster occurs, are more than 10 times larger than these credit contracts at $226 Trillion.  While some take comfort in

> “Bilateral Netting: A legally enforceable arrangement between a bank and a counterparty that creates a single legal obligation covering all included individual contracts. This means that a bank‟s receivable or payable, in the event of the default or insolvency of one of the parties, would be the net sum of all positive and negative fair values of contracts included in the bilateral netting arrangement.”

bilateral netting does not work so well when your counterparty fails like Lehman Brothers.

I know there must be a better way to read Microsoft Excel XML spreadsheets in R, but these were my two most elegant methods.  Please let me know how I could have done better.

[R code (click to download):](https://docs.google.com/leaf?id=0B2qp2r96khJPODIzYjViNGUtYjQyYi00NTkyLWIyNDgtMTE5MmVjZGU0MjVm&hl=en_US)

```
#read xml derivatives data from the
#US Treasury OCC Quarterly Derivatives Report
#2 methods of as far as I can tell 
#the first published example of how to read
#Microsoft Excel xml workbooks   require(XML)
require(ggplot2)   url = "http://www.occ.treas.gov/topics/capital-markets/financial-markets/trading/derivatives/dq410-xml.xml"
#url = "dq410-xml.xml"   doc = xmlInternalTreeParse("dq410-xml.xml")
#define namespaces
#figuring this out took hours
#but using getNodeSet was much cleaner than the
#next method
namespaces = c(o="urn:schemas-microsoft-com:office:office",
	x="urn:schemas-microsoft-com:office:excel",
	ss="urn:schemas-microsoft-com:office:spreadsheet",
	html="http://www.w3.org/TR/REC-html40")
ns <- getNodeSet(doc,"/ss:Workbook/ss:Worksheet[@ss:Name='Table 3']/ss:Table/ss:Row",namespaces)[[44]]
pct <- df <- as.data.frame(as.numeric(xmlSApply(ns, xmlValue))[5:8])
ns <- getNodeSet(doc,"/ss:Workbook/ss:Worksheet[@ss:Name='Table 3']/ss:Table/ss:Row",namespaces)[[8]]
lab <- as.character(xmlSApply(ns, xmlValue)[8:11])
df <- cbind(lab,df)
#jpeg(filename="derivatives by type.jpg",quality=100,
#	width=6.25, height = 8,  units="in",res=96)
barplot(df[,2],names.arg = df[,1],main="US Bank Derivatives by Type
	Q4 2010",ylab="% of Total")
mtext("Source: US Dept of Treasury OCC Quarterly Derivatives Report",
	side=1,line=3,cex=0.8,adj=0)
#dev.off()       #here is the original very hacked brute force method
doc = xmlRoot(xmlTreeParse(url))
#set xmlNodeList to Table 3
#hacked with brute force
table3 <- doc[6]$Worksheet
df <- as.data.frame(cbind(
	as.numeric(
	xmlApply(table3[[1]],function(x) xmlApply(x,xmlValue))[53]$Row[5:8])),
	stringsAsFactors=FALSE)
df <- cbind(
	as.character(xmlApply(table3[[1]],function(x) xmlApply(x,xmlValue))[17]$Row[c(8:11)]),
	df)
colnames(df) <- c("DerivativeType","PctOfTotal")
barplot(df[,2],names.arg = df[,1],main="US Bank Derivatives by Type
	Q4 2010",ylab="% of Total")
mtext("Source: US Dept of Treasury OCC Quarterly Derivatives Report",
	side=1,line=3,cex=0.8,adj=0)
```

[Created by Pretty R at inside-R.org](http://www.inside-r.org/pretty-r "Created by Pretty R at inside-R.org")