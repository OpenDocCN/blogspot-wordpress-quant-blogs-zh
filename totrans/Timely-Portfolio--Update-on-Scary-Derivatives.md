<!--yml
category: 未分类
date: 2024-05-18 15:11:03
-->

# Timely Portfolio: Update on Scary Derivatives

> 来源：[http://timelyportfolio.blogspot.com/2011/11/after-reading-bloombergs-article.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/11/after-reading-bloombergs-article.html#0001-01-01)

After reading Bloomberg’s article,

> JPMorgan Chase & Co. and Goldman Sachs Group Inc., among the world’s biggest traders of credit derivatives, disclosed to shareholders that they have sold protection on more than $5 trillion of debt globally.
> 
> [http://bloom.bg/txiyuG](http://bloom.bg/txiyuG)

I thought we should update my post [Scary Derivatives and Scary XML in R](http://timelyportfolio.blogspot.com/2011/07/scary-derivatives-and-scary-xml-in-r.html) in which I said

> The massive damage caused in 2008-2009 by the sliver of derivatives called credit default swaps seems like a faint warning siren when we see that they only represent < 7% of total derivatives exposure. Interest rate and currency derivatives, also where I think the next disaster occurs, are more than 10 times larger than these credit contracts at $226 Trillion.

This amount of money, bilaterally netted or not, is truly unbelievable and staggering.  Total debt outstanding of the sovereign nations is not the real problem.  Like housing, the exponential exacerbation caused by the leverage and derivatives traded on the underlying is where the real potential catastrophe occurs.  No government and no central bank has the ability to counter any major damage in currencies or interest rates.

[R code (click to download from Google Docs):](https://docs.google.com/open?id=0B2qp2r96khJPYjUwNDNkNTktMGFkZC00ZGViLWEyNjAtNTZiZWI2M2VlMWNi)

#read xml derivatives data from the
#US Treasury OCC Quarterly Derivatives Report
#2 methods
#still way too manual since it appears the format changes
#each reporting period

#as far as I can tell
#the first published example of how to read
#Microsoft Excel xml workbooks

require(XML)
#require(ggplot2)

#get 2nd Quarter of 2011 report (dq211)
url = "[http://www.occ.treas.gov/topics/capital-markets/financial-markets/trading/derivatives/dq211-xml.xml"](http://www.occ.treas.gov/topics/capital-markets/financial-markets/trading/derivatives/dq211-xml.xml%22)

doc = xmlInternalTreeParse(url)
#define namespaces
#figuring this out took hours
#but using getNodeSet was much cleaner than the
#next method
namespaces = c(o="urn:schemas-microsoft-com:office:office",
    x="urn:schemas-microsoft-com:office:excel",
    ss="urn:schemas-microsoft-com:office:spreadsheet",
    html="[http://www.w3.org/TR/REC-html40")](http://www.w3.org/TR/REC-html40%22))
#this gets row 41 from the Table 3 worksheet for the total $ of derivatives
ns <- getNodeSet(doc,"/ss:Workbook/ss:Worksheet[@ss:Name='Table 3']/ss:Table/ss:Row",namespaces)[[41]]
amt <- df <- as.data.frame(as.numeric(xmlSApply(ns, xmlValue))[4:11])
#believe it or not this is $trillions of dollars
#remove some zeros so we can label better on the graph
amt <- amt/1000000
df <- df/1000000
#this gets row 10 for labels
ns <- getNodeSet(doc,"/ss:Workbook/ss:Worksheet[@ss:Name='Table 3']/ss:Table/ss:Row",namespaces)[[10]]
lab <- as.character(xmlSApply(ns, xmlValue)[4:11])
#combine the labels with
df <- cbind(lab,df)
#jpeg(filename="derivatives by type.jpg",quality=100,
#    width=6.25, height = 8,  units="in",res=96)
barplot(df[5:8,2],names.arg = factor(df[5:8,1]),main="US Bank Derivatives by Type
    Q2 2011",ylab="$ (in trillions)",ylim=c(0,max(df[5:8,2]+50)),space=0,
    col=c("indianred4","darkolivegreen4","cadetblue4","goldenrod3"))
mtext("Source: US Dept of Treasury OCC Quarterly Derivatives Report",
    side=1,line=3,cex=0.8,adj=0)
#dev.off()