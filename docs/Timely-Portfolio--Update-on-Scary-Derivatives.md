<!--yml

category: 未分类

date: 2024-05-18 15:11:03

-->

# Timely Portfolio: 更新可怕衍生品

> 来源：[`timelyportfolio.blogspot.com/2011/11/after-reading-bloombergs-article.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/11/after-reading-bloombergs-article.html#0001-01-01)

阅读彭博社的文章后，

> 摩根大通银行和和高盛集团公司，世界上最大的信用衍生品交易商之一，向股东披露，他们已经在全球范围内出售了超过 5 万亿美元的债务保护。
> 
> [`bloom.bg/txiyuG`](http://bloom.bg/txiyuG)

我认为我们应该更新我的帖子[R 中的可怕衍生品和可怕的 XML](http://timelyportfolio.blogspot.com/2011/07/scary-derivatives-and-scary-xml-in-r.html)，其中我说

> 2008-2009 年，被称为信用违约掉期的衍生品小部分造成了巨大的损害，这似乎是一个微弱的警告警报，当我们看到它们只代表总衍生品风险的< 7%时。利率和货币衍生品，也是我认为下一个灾难发生的地方，比这些信用合同大 10 倍以上，达到 226 万亿美元。

这笔钱，无论双边净额如何，都是真正令人难以置信和震惊的。总债务 outstanding of the 主权国家并不是真正的问题。像房地产一样，由杠杆和衍生品加剧的指数恶化是真正的潜在灾难发生的地方。没有政府和中央银行有能力抵消任何主要货币或利率的损害。

[R 代码（点击从 Google Docs 下载）：](https://docs.google.com/open?id=0B2qp2r96khJPYjUwNDNkNTktMGFkZC00ZGViLWEyNjAtNTZiZWI2M2VlMWNi)

#从

#美国财政部 OCC 季度衍生品报告

#2 种方法

#仍然过于手动，因为它看起来格式发生了变化

#每个报告期

#据我所知

#第一个公开的读取

#微软 Excel 的 xml 工作簿

require(XML)

#require(ggplot2)

#获取 2011 年第二季度报告（dq211）

url = "[`www.occ.treas.gov/topics/capital-markets/financial-markets/trading/derivatives/dq211-xml.xml`](http://www.occ.treas.gov/topics/capital-markets/financial-markets/trading/derivatives/dq211-xml.xml%22)

doc = xmlInternalTreeParse(url)

#定义命名空间

#弄清楚这需要几个小时

#但使用 getNodeSet 比

#下一个方法

namespaces = c(o="urn:schemas-microsoft-com:office:office",

x="urn:schemas-microsoft-com:office:excel",

ss="urn:schemas-microsoft-com:office:spreadsheet",

html="[`www.w3.org/TR/REC-html40")`](http://www.w3.org/TR/REC-html40%22))

#此方法从表 3 工作表中获取总衍生品的第 41 行

ns <- getNodeSet(doc,"/ss:Workbook/ss:Worksheet[@ss:Name='Table 3']/ss:Table/ss:Row",namespaces)[[41]]

amt <- df <- as.data.frame(as.numeric(xmlSApply(ns, xmlValue))[4:11])

#信不信由你，这是万亿美元的美元

#移除一些零，这样我们可以在图表上更好地标记

amt <- amt/100000

df <- df/1000000

#此部分获取第 10 行的标签

ns <- getNodeSet(doc,"/ss:Workbook/ss:Worksheet[@ss:Name='Table 3']/ss:Table/ss:Row",namespaces)[[10]]

标签 <- 作为字符串的 xmlSApply(ns, xmlValue)[4:11]

#将标签与

df <- cbind(标签,df)

#jpeg(filename="按类型划分的衍生品.jpg",quality=100,

#    宽度=6.25, 高度 = 8, 单位="英寸", 分辨率=96)

barplot(df[5:8,2],名称参数=因子(df[5:8,1]),主标题="美国银行按类型划分的衍生品

第二季度 2011 年",y 轴标签="（万亿美元）",y 轴范围=c(0,max(df[5:8,2]+50)),空间=0,

颜色=c("indianred4","darkolivegreen4","cadetblue4","goldenrod3"))

mtext("数据来源：美国财政部货币监理署季度衍生品报告",

侧边=1,线宽=3,字体大小=0.8,位置调整=0)

#关闭设备
