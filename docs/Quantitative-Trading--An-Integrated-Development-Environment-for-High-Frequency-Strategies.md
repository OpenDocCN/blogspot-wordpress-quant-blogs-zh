<!--yml

category: 未分类

date: 2024-05-12 18:59:47

-->

# 量化交易：高频策略的集成开发环境

> 来源：[`epchan.blogspot.com/2013/04/an-integrated-development-environment.html#0001-01-01`](http://epchan.blogspot.com/2013/04/an-integrated-development-environment.html#0001-01-01)

我已经接触过许多软件平台，允许交易员首先指定和回测策略，然后，只需按一下按钮，将回测策略转换为一个可以自动向他们喜爱的经纪人提交订单的实时交易程序。（在此主题上查看我的所有文章）

[这里](http://epchan.blogspot.com/search/label/Automated%20trading%20platforms)

.)  我称这些平台为我的“集成开发环境”（IDE）

[新书](http://www.amazon.com/gp/product/1118460146/ref=as_li_qf_sp_asin_il_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=1118460146&linkCode=as2&tag=quantitativet-20)

的平台，它们从熟悉且面向零售的（例如 MetaTrader，NinjaTrader，TradeStation）到专业但需要技能的（例如 ActiveQuant，Marketcetera，TradeLink），再到全面且工业强度的（例如 Deltix，Progress Apama，QuantHouse，RTD Tango）不等。其中一些根本不需要编程技能，允许您通过拖放来构建策略，另一些使用一些简单的脚本语言如 Python，还有一些需要 Java，C#或 C++的全面编程能力。但这些哪些允许我们回测和执行高频策略？

显而易见的是：回测 HF 策略相当困难。数据量是一个问题。但此外，执行细节对这些策略非常重要：诸如我们将订单路由到的确切交易所/场所、触发我们订单的订单簿的精确状态、我们正在使用的订单类型，以及如果我们使用非市场订单，被填充的概率。搞砸其中一个细节，回测将远非真实。我经常告诉人们，纸上交易高频策略比回测高频策略更容易。虽然我上面报告的许多平台确实允许使用 tick 数据进行回测，但我不知道它们是否允许使用完整的订单簿和执行场所进行回测。在此背景下，我很高兴地报告我最近发现了一个名为

[Lime Strategy Studio](http://www.limebrokerage.com/services/marketdata/simulation)

.

~~首先，坏消息。LimeTrader 仅对与 Lime Brokerage 交易的交易员有用，因为它配置为仅向 Lime 发送实时订单。~~

[

**更新：**

我后来了解到，为第三方经纪人提供了适配器。]然而，如果你打算交易高频股票和期货策略，为什么不选择 Lime 呢，因为他们为你提供了一个全面的 API，直接从交易所获取超低延迟的数据流，并允许（甚至坚持）在交易所或他们的数据中心进行托管，费用合理？（全文披露：目前我没有任何与 Lime 的商业关系，尽管我曾是他们的客户。）另一个不好的消息是：策略的规格必须使用 C++。

但一旦你克服了这两个障碍，好处将是多方面的。你可以为实盘交易策略指定的每一个细节都可以为回测和模拟交易指定。正如我所说，这些细节可能包括订单类型、交易场所、订单簿的状态，甚至订单簿的统计数据，更不用说基本数据，如收益、公司行动和其他用户提供的数据，如新闻。fill 模拟器用于你的非市场订单。与其他 IDE 一样，一旦你在其每一个细节上都回测过策略并对性能指标满意，你就可以通过一键操作将其投入实盘（无论是用于模拟交易还是实际交易）。

如果任何读者知道有其他具有类似功能并适用于回测高频策略的 IDE，请告诉我们！

===

说到高频策略，交易员们经常抱怨围绕它们的超高度机密性以及在这个领域收集知识 difficulty. A friend (hat tip: Dave) referred me to this

[论文](http://www.math.stevens.edu/~ifloresc/Research/Publications/ProjectpricevolFinalwithDragos.pdf)

Dragos Bozdog 教授著

*et. al.*

让人们了解到可能涉及哪种类型的建模。我觉得这篇论文非常易读且发人深思。

===

还有两个名额可以在我的在线

[均值回归策略研讨会](http://www.epchan.com/my-workshops/)

计划于五月进行。
