<!--yml

分类：未分类

日期：2024-05-18 06:37:14

-->

# MPP：通过内存技术和分析的实时大数据 | 交易桌上的故事

> 来源：[`mdavey.wordpress.com/2012/07/24/mpp-big-data-in-real-time-through-in-memory-technology-and-analytics/#0001-01-01`](https://mdavey.wordpress.com/2012/07/24/mpp-big-data-in-real-time-through-in-memory-technology-and-analytics/#0001-01-01)

## MPP：通过内存技术和分析的实时大数据

通过内存技术和分析实时利用大数据的力量](http://www3.weforum.org/docs/GITR/2012/GITR_Chapter1.7_2012.pdf)的阅读引导产生了以下思考：PDF 的第 93 页讨论了金融和建模环境（我猜是风险？）。随着更多系统趋向于近实时（NRT），很显然内存是首选路径。有了内存技术，问题转化为哪种产品/开源解决方案能帮助这条路径。[GridGain](http://www.gridgain.com/blog/fyi/gridgain-4-2-released/)就是这一领域的技术之一。[RBS](http://www.bankingtech.com/bankingtech/article.do?articleid=20000192301)，如之前博客所述，已经在大数据交易世界中采取了 Oracle Coherence 的方法——操作数据缓存。

在 GridGain 作为大数据[产品](http://www.gridgain.com/blog/archives/new-products-and-services-from-gridgain/)的情况下，产品演变已经创造了三个[产品](http://www.gridgain.com/features/)——计算网格、数据网格和大数据（实际上是另外两个产品的组合）。很明显，[Hadoop](http://www.gridgain.com/blog/fyi/gigaom-hadoop-days-are-numbered-are-they/)在[大数据](http://gigaom.com/cloud/why-the-days-are-numbered-for-hadoop-as-we-know-it/)领域的末日已经过时了。

转向 Gigaspaces，“XAP 9.0 – Geared for Real-Time Big Data Stream [Processing](http://blog.gigaspaces.com/xap-9-0-%E2%80%93-geared-for-real-time-bigdata-stream-processing/)”触及了一个重要点，这个点很少被谈论——数据移动：

> 一旦你在多个节点上存储了内存中的数据，实现数据的局部性和处理是很重要的。如果你在一个节点上处理一个传入事件，并且需要读取和更新其他节点上的数据，你的处理延迟和可扩展性将会非常有限。实现局部性需要一个坚固的路由机制，这将允许你将事件发送到与它们最相关的节点，即需要其处理数据的节点。

另一个提供在大数据上进行内存分析能力的产品是[Kognitio](http://www.kognitio.com/analyticalplatform)。“信用和风险管理”提到，但细节不多。有谁用过 Kognitio？

~ mdavey 于 2012 年 7 月 24 日。

发布在[未分类](https://mdavey.wordpress.com/category/uncategorized/)

Tags: [大数据](https://mdavey.wordpress.com/tag/bigdata/), [MPP](https://mdavey.wordpress.com/tag/mpp/)
