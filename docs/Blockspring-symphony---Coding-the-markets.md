<!--yml

分类: 未分类

日期: 2024-05-12 19:31:09

-->

# Blockspring 交响乐 | 编码市场

> 来源：[`etrading.wordpress.com/2015/09/10/blockspring-symphony/#0001-01-01`](https://etrading.wordpress.com/2015/09/10/blockspring-symphony/#0001-01-01)

## Blockspring 交响乐

### 2015 年 9 月 10 日

[Blockspring](http://www.blockspring.com) 是一家很酷的初创公司，可以让用户从 Excel 中调用网络服务 API。与 Amazon、Bing、Dropbox、Facebook、Github、Google、linkedin、Quandl、Slack、Twitter 等等进行了[预先制作的集成](https://open.blockspring.com/browse)。Blockspring 的美妙之处在于，它将所有这些多样的网络 API 规范化，以便可以从单个 Excel 工作表中调用它们的函数：=BLOCKSPRING(…) 众所周知，Excel 的巨大优势在于它使得非开发人员能够独立构建各种解决方案。Blockspring 极大地扩展了你可以在 Excel 中做的事情范围。要使一个服务可通过 =BLOCKSPRING(…) 使用，你需要在 Python、Ruby、JavaScript、PHP 或 R 中[编写一个“块”](https://www.blockspring.com/docs)。这些块托管在亚马逊服务器上。一切都很好，但这意味着你仍然需要是一个开发者来创建一个块。如果 Excel 用户可以在 Excel 本身中实现块，那该怎么办？要做到这一点，你需要一个可以自动执行电子表格的云托管服务器。当然，这正是 [SpreadServe](http://spreadserve.com/) 所做的！所需要的只是一些可以与 SpreadServe 实例通信的块的代码。这是 [GitHub 上的源代码](https://gist.github.com/osullivj/4196cfe28a4ca4d5ecfd)，以及它在 [Blockspring 上部署的情况](https://open.blockspring.com/osullivj/98fe3455701227485ec2727a7fb17f1a)。使用这个 SpreadServe 块，客户端电子表格可以将任何 SpreadServe 托管的电子表格用作 Web 服务。这里有一个例子。[InvestExcel](http://investexcel.net/) 的 BlackScholes 电子表格可以根据常规输入：股票和行权价格、波动率、无风险利率和期限来计算期权的认购和认沽价格。这个相同的电子表格在 [亚马逊托管的 SpreadServe 实例上部署的情况](http://52.88.140.209:8888/BlackScholes.xls/Black-Scholes%20Model)，它将其计算功能提供给了 Blockspring 客户端电子表格。[这个电子表格](https://github.com/SpreadServe/ssxls/blob/master/bspring2.xls)计算了一系列不同行权价格的期权的认购和认沽价格。确保在运行时将公式/计算选项设置为自动。系列中有九种不同的行权价格，所以每个认购和认沽计算都需要进行九次往返。尝试更改其中一个输入；股票或行权价格。它会导致所有认购和认沽价格重新计算。如果在重新计算过程中将浏览器指向[SpreadServe 主机的 RealTimeWebServer](http://52.88.140.209:8888/BlackScholes.xls/Black-Scholes%20Model)，你会看到所有输入都被传送过去，并且所有输出都会计算出来。所以你就有了 [Blockspring](http://blockspring.com) 和 [SpreadServe](http://spreadserve.com) - 两个味道都很美妙的组合！
