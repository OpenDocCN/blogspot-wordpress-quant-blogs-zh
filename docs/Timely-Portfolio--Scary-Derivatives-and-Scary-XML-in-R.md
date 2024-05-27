<!--yml

分类：未分类

日期：2024-05-18 15:13:17

-->

# 及时投资组合：R 中的可怕衍生品和可怕的 XML

> 来源：[`timelyportfolio.blogspot.com/2011/07/scary-derivatives-and-scary-xml-in-r.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/07/scary-derivatives-and-scary-xml-in-r.html#0001-01-01)

我需要一些新的 R 技能，学习 R 中的 XML 没有比美国财政部的货币监理署（OCC）季度衍生品报告更令人畏惧的数据集更好的动机了——我将在稍后的帖子中转向更令人畏惧的全球[BIS 衍生品数据](http://www.bis.org/publ/otc_hy1105.htm)，以避免诱发噩梦和失眠。

2008-2009 年，被称为信用违约掉期的一小部分衍生品造成了巨大的损害，当我们看到它们只代表总衍生品风险暴露的< 7%时，这似乎像是一个微弱的警告警报。利率和货币衍生品，也是我认为下一次灾难发生的地方，比这些信用合同大 10 倍以上，达到 226 万亿美元。尽管有些人认为有安慰的是

> 双边净额结算：是一家银行和对手方之间的一种具有法律强制力的安排，创建了一个单一的法律义务，覆盖了所有包括在内的个别合同。这意味着，在某一方的违约或破产事件中，银行的应收或应付将是双边净额结算安排中所有合同的正负公允价值净额。

当您的对手方像雷曼兄弟那样失败时，双边净额结算效果不佳。

我知道在 R 中读取 Microsoft Excel XML 电子表格一定有更好的方法，但这两种是我认为最优雅的方法。请告诉我我还可以怎样做得更好。

[R 代码（点击下载）：](https://docs.google.com/leaf?id=0B2qp2r96khJPODIzYjViNGUtYjQyYi00NTkyLWIyNDgtMTE5MmVjZGU0MjVm&hl=en_US)

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

[由 Pretty R 在 inside-R.org 创建](http://www.inside-r.org/pretty-r "由 Pretty R 在 inside-R.org 创建")
