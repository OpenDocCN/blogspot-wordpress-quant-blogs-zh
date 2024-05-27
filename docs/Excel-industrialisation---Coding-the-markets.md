<!--yml

分类：未分类

日期：2024 年 5 月 12 日 19:32:04

-->

# Excel 工业化 | 编码市场

> 来源：[`etrading.wordpress.com/2015/04/03/excel-industrialisation/#0001-01-01`](https://etrading.wordpress.com/2015/04/03/excel-industrialisation/#0001-01-01)

## Excel 工业化

### 2015 年 4 月 3 日

[John Greenan](https://www.linkedin.com/in/johngreenan) 在[他的博客](http://blog.alignment-systems.com)上发布了一系列关于 Excel VBA 工业化的[优秀文章](http://blog.alignment-systems.com/search/label/Excel%20Industrialisation)，这个主题对我来说很重要，所以我觉得我最好回应一下。在他的文章中，JG 提出了一系列基于 VB 扩展的技术，以实现从电子表格中导出嵌入的 VB，以便进行版本控制，以及用于错误记录和报告的技术。这些代码在 [github](https://github.com/JohnGreenan) 上可用，这对公共领域是一个有价值的补充，特别是因为有几个商业产品在解决这个领域的问题，比如 [spreadgit](http://spreadgit.com/)，[ClusterSeven](http://www.clusterseven.com/) 和 [Finsbury Solutions](http://www.finsburysolutions.com/)。JG 在第一部分开始讨论时观察到 VBA 处于低谷，而时髦的孩子们正在使用 MEAN、Scala、OCaml 或 Haskell。当然，时髦的孩子们永远不会使用 VBA。但这不仅仅是因为其他语言更酷，而是因为 VBA 和最新的编程语言面向的是完全不同的受众。Scala、OCaml 和 Haskell 是为开发人员设计的，而 Excel 是为非开发人员、最终用户、业务用户设计的。Excel 能够让最终用户创建软件解决方案，这正是其成功和普及的原因。显然，世界上有 [1100 万专业软件开发人员](http://www.infoq.com/news/2014/01/IDC-software-developers)。但即使这 1100 万人也无法满足世界对软件的需求，所以最终用户必须生成自己的解决方案，并且他们使用 Excel 来完成。正如 JG 在他系列文章的 [第六部分的评论](http://blog.alignment-systems.com/2015/03/excel-vba-industrialisationpart-six.html?showComment=1427590236378#c5959579053154491774) 中指出的那样：“在许多情况下，对 Excel 工业化的需求来自于拥有成千上万张电子表格的公司，这些表格不可能全部以成本效益的方式手动重写以符合编码标准。”

版本控制系统是控制这些端用户开发的电子表格组合的重要部分。然而，它只解决了问题的一部分。导致这么多电子表格问题的另一个重要潜在因素是它们的手动式桌面操作。由于 Excel 是一个桌面应用程序，Excel 电子表格必须由用户手动操作。用户必须启动 Excel，加载表格，输入未经验证的数据，按 F9，然后复制粘贴或通过电子邮件传送结果。所有这些操作都容易出错。所有这些手动操作是阻止任何有组织的系统测试的一个主要因素。所有这些问题在[伦敦鲸](http://baselinescenario.com/2013/02/09/the-importance-of-excel/)身上都很明显。如果我们能够将 Excel 作为开发环境与 Excel 作为运行时分离，所有这些问题都能解决。端用户可以在 Excel 中开发自己的解决方案是很好的，但是这些解决方案在桌面 PC 上手动操作是麻烦且容易出错的。这些解决方案应该是自动化的、有弹性的和可扩展的，并由服务器端运行。当然，这就是[SpreadServe](http://spreadserve.com/industries/)。
