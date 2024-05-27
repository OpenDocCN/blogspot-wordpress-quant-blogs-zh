<!--yml

分类：未分类

日期：2024-05-18 05:03:50

-->

# Magmasystems Blog: Of Pipes, CEP, and Traders

> 来源：[`magmasystems.blogspot.com/2008/02/of-pipes-cep-and-traders.html#0001-01-01`](http://magmasystems.blogspot.com/2008/02/of-pipes-cep-and-traders.html#0001-01-01)

在我们的复杂事件处理系统中，我们最终希望提供一个前端给我们的交易员，该前端将让交易员开发附加

hoc

实时流上的流查询打包的。我们还希望允许交易员通过在几年的数据上进行回测来实现他们自己的分析。

我最近稍微看了看雅虎管道，它的概念和我一直为交易员设想的那种 GUI 是一样的。在雅虎管道中，你可以把一个或多个高级对象输出的结果管道的输入另一个高级对象。

这里是一个雅虎管道的器件示例：

![](http://3.bp.blogspot.com/_BNP90JOg4yU/R8Al0Pk0_KI/AAAAAAAAACg/XTmXTh0KN2A/s1600-h/Yahoo+Pipes.jpg)

在我们的简单用例中，假设我们定义了交易员感兴趣的高级对象。这样的对象可以是

一个实时市场数据流，

一个历史市场数据流，

一个实时订单流流和缓存，

一个历史订单流流，

一个从行情到行业的映射器和过滤器，以及

一些计算模块。

中构建的“查询”类型。

Streambase

，Coral8，

Aleri

，

NEsper

) 在我们的评估过程中。然而，正如领域特定语言（

DSL

）可以创建，以使在特定领域开发应用程序变得更容易，我们可以制作一个针对分析股票数据而设计的雅虎管道的领域特定版本。

一旦交易员组装了他的管道的结果可以被翻译成

CEP

引擎支持。如果我们封装代码生成模块，那么我们可以为 Coral8、

Streambase

，

Aleri

，

NEsper

，以及其他引擎拥有代码生成器。我敢肯定，所有这些引擎都允许您动态注册和

取消注册

查询。您可以动态读取

CEP

引擎并将它反馈到 GUI 中。

Aleri

以及

Streambase

为他们的开发者提供了类似于雅虎管道的 GUI 构建器。然而，这些是我们在复杂事件处理引擎（

GUI

不是作为

工具包

;也就是说，你不能采取

Streambase

GUI 并进行适应以满足您的需求。Coral8 并没有真正的豪华 GUI 构建器；如前面提到的，他们的 GUI 相当简陋。

NEsper

/

Esper

没有所谓的 GUI，因为他们的模型是将引擎嵌入应用程序内部，这与其他供应商使用的模型不同。

版权所有 ©2008 Marc Adler - 保留所有权利
