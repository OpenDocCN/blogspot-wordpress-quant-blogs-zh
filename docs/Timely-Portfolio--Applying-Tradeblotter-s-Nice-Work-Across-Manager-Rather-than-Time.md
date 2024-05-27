<!--yml

类别：未分类

date: 2024-05-18 15:01:44

-->

# 及时投资组合：在不同的管理者之间应用交易账单的好工作，而不是按时间

> 来源：[`timelyportfolio.blogspot.com/2013/01/applying-tradeblotters-nice-work-across.html#0001-01-01`](http://timelyportfolio.blogspot.com/2013/01/applying-tradeblotters-nice-work-across.html#0001-01-01)

自从我第一次看到[下载并解析 EDHEC 对冲基金指数](http://tradeblotter.wordpress.com/2012/06/04/download-and-parse-edhec-hedge-fund-indexes/)中非常有用的分布页面以来，我就广泛使用了它。现在，它已经功能化([视觉比较回报分布](http://tradeblotter.wordpress.com/2013/01/18/visually-comparing-return-distributions/)），我想稍微修改它，以便比较不同管理者的回报分布，而不是时间。作为一个简单的例子，我比较了[Vanguard](https://personal.vanguard.com/us/funds/vanguard/all?reset=true&sort=name&sortorder=asc)和[Pimco](http://investments.pimco.com/Products/pages/PlOEF.aspx?Level1=ulProducts&Center=ulProducts&Level2=liulProductsMutualFunds)提供的共同基金。这个修改后的功能可能对跨外部或内部货币管理者的单独管理账户的内部绩效监控非常有帮助。此外，为了组合分散度，这可能是一个好的开始摘要视图。

我喜欢在[PIMCO 基金的美观相关性地图](http://timelyportfolio.blogspot.com/2012/06/pretty-correlation-map-of-pimco-funds.html)中所做的工作，但这次我想要直接在表格中获取绩效数据，而不是从多个 getSymbols 函数调用中计算绩效。R 可以轻松加载这些表格，但我变得懒惰，将表格导入 Excel [`docs.google.com/file/d/0ByeeEIaS0AOsRE1OeWk2VmFFVUU/edit`](https://docs.google.com/file/d/0ByeeEIaS0AOsRE1OeWk2VmFFVUU/edit "https://docs.google.com/file/d/0ByeeEIaS0AOsRE1OeWk2VmFFVUU/edit")，然后用一些老式的透视表进行清理。数据处理完成后，我将它们复制并粘贴到数据表中以保存为.csv（本可以再次使用 R 直接从 Excel 获取数据），这样我就可以通过[Google Docs](https://docs.google.com/spreadsheet/pub?key=0AieeEIaS0AOsdDFET0ZmbTBKWDNoMnZrZ0oySWRia1E&single=true&gid=0&output=csv)发布，供任何想复制我所做工作的人使用。

现在，我想把这个非常不错的工作[跟踪历史集群的数量](http://systematicinvestor.wordpress.com/2013/01/27/tracking-number-of-historical-clusters/)纳入这个分析中，但我会在另一篇文章中讨论。

[Gist 上的代码](https://gist.github.com/4658217)
