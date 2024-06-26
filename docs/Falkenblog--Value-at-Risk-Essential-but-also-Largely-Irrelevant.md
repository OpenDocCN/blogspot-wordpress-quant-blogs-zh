<!--yml

category: 未分类

date: 2024-05-12 21:59:12

-->

# Falkenblog: Value at Risk Essential but also Largely Irrelevant

> 来源：[`falkenblog.blogspot.com/2009/06/value-at-risk-essential-but-also.html#0001-01-01`](http://falkenblog.blogspot.com/2009/06/value-at-risk-essential-but-also.html#0001-01-01)

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhf2lBlVYaArfwpfFB5XTSa21wZlsjfwvZlTCvWAyXpeiTugte9AdEoPPclza3ox5x_i1OLnGCmdPkMfRuyKseaGkCT8PiG7Vn4z8Gi8MRqJDAqSDKZ9sntvD0PLoaUNG7V1P6m5A/s1600-h/mvopt.jpg)

我发现风险价值（VaR）非常有用，主要是为了让你知道人们没有进行未经授权的投注。如果一名流氓交易员决定对美元兑日元的汇率进行投机，那就会暴露出来，所以这有助于让你的交易员守规矩。但这很少很少地...

drives

银行的战略决策。这更像是银行网站的互联网安全，必不可少，但对于管理银行相关风险并不是头等大事。如果认为银行在均值-波动率空间中选择 VaR 来找到其在有效前沿上的最佳位置，那是一个头等大的错误。VaR 风险主要是偶然的，并且有助于最大限度地减少操作风险（例如，许多致命风险在事先根本不会被容忍）。

[Ricardo Rebenatto](http://www.riccardorebonato.co.uk/)

写了一些非常好的关于利率模型的书和文章，我重新阅读了其中的几篇。他是苏格兰皇家银行(Royal Bank of Scotland)市场风险负责人和全球定量研究团队负责人。他的书，

[牌局的预言家](http://www.amazon.com/Plight-Fortune-Tellers-Financial-Differently/dp/0691133611/ref=sr_1_1?ie=UTF8&s=books&qid=1244471388&sr=1-1)

，反对定量模型的天真应用，这是一个大胆的立场，肯定会被金融中天真使用模型的倡导者所驳斥（我找不到他们的主页......）。我们需要更多的常识，对“没有常识”这一广受欢迎的口号的又一个勇敢的打击。

Russ Roberts

[采访了他](http://www.econtalk.org/archives/2009/06/rebonato_on_ris.html)

在 EconTalk 上，我突然想到，这家伙典型地象征着一个“风险经理”。“他有证明他懂很多数学的资格（核工程博士和凝聚态物理/材料科学博士）。他经常在风险会议上发言，并且担任 GARP 的董事会成员。但显而易见的是，他并没有向苏格兰皇家银行的决策者多交流关于实际战略的事情。

为什么我这么说？因为，认为风险度量到小数点后第五位是“危险的”，意味着重大决策是基于这些信息做出的。从他的前言中：

> 金融风险管理处于一种困惑状态。它变得过分专注于测量风险。与此同时，它忘记了管理风险是关于在不确定性下做出决策。它似乎还抱着两种危险的信念：首先，我们的风险度量可以估计到 5 位小数；其次，一旦我们这样做了，结果将不言自明地指导我们的风险管理选择。

在你认为这种情况正在发生的范围内，你真的不知道你不知道这些信息如何与战略和战术决策相关。VaR 对银行来说是相当无关紧要的。当然，这是一种集合市场风险的基本方式，但在当前危机中，这种风险是相当微不足道的，因为只要资产或企业受到 VaR 的影响，VaR 就是基于推动业务决策的假设计算的（即证券化的资产净值不会下降）。这一假设（并不是很技术性的一个），使得所产生的 VaR 无害，这是每个人都能理解的。人们为什么会做出这样的假设？这是一个有趣的问题，但我认为这与风险价值-at-Risk 关系不大。也就是说，到 2006 年前后，任意的但较大的压力测试将具有相同的假设。

如果你看看 Rebenatto 的 RBS，在他们的年度报告中，他们展示了仅有的 4000 万英镑的每日 95%VaR，这相当于 99.9%VaR 的 13 亿英镑。假设我们把这个数字乘以 3，得到所需的资金，我们将得到 40 亿英镑。RBS 的股本约为 730 亿英镑。显然，即使在他自己的公司里，VaR 也不是理解他们“风险”最主要的驱动因素。

关于风险价值-at-Risk，或者说小数点后第五位的风险数字是危险的这个想法，假设人们正在重要的方式下使用这些信息。也就是说，当货币市场的 VaR 从 43.32491 变为 43.32492 时，交易员会调整他们的点差。我们假设里卡多恰好看到了这一点，认为“小数点后第五位”的说法是修辞手法。无论如何，他认为 VaR 推动了真正的决策。在他的人际关系圈（全球风险专业人士协会，风险管理大会，向监管机构展示 VaR），这种论点也许是站得住脚的，但却突显了他不理解银行内部如何制定战略决策。他被高层管理层放纵，他们非常喜欢认为 VaR 的第五位小数是重要的风险管理者，因为他们没有看到更大的图景，便可以自行其事。

VaR 主要应用于市场交易活动，通常这些活动的夏普比率很高（>3），因为你可以通过买卖价差和在顾客前进行交易来赚钱，因此利润主要是与成交量挂钩。任何剩余的持有通过你的 VaR 产生“市场风险”，但大多数市场交易员并不太在意，因为从 VaR 的角度来看，他们都是打出了巨大的全垒打，因为夏普比率总是高于任何人的提款利率。市场交易的利润是与成交量挂钩的，这意味着销售、联系，而不是拥有更好的 VaR 测量。如果他们可以选择将其市场交易活动扩大一倍，从而使其 VaR 翻倍，所有的市场交易员都会选择这样做。VaR 是一个很好的方法，可以确保交易员不改变他们的经营模式，但它并没有捕捉到商业模式的任何关键因素，因为所有的市场交易员都希望有更多的交易量；VaR 并不像风险回报空间中的一个选择变量。

他争辩说我们应基本上使用从显性偏好中推断出的概率，指出“行为金融学”显示出各种偏见。这意味着，依据的是个案。你只需有代表性的个案，正确的先验！这就是常识的问题。有些人认为是基本常识的事情，其他人可能认为是胡说八道。这并不是说这种说法不正确，只是没有帮助。应当毋庸置疑，现实世界不是从我们了解其中所含蓝球和红球的比例的罐子中抽出数字。考虑到大多数商业决策的狭隘性，这并不能比说“在做未来决策时，你应该考虑所有信息来估计风险”更有帮助。

[凯特·凯利的书](http://falkenblog.blogspot.com/2009/05/bear-books.html)

对贝尔斯登的失败强调了这类风险管理者的不重要性。正如她所说，“风险管理和运营等部门的经理在公司核心业务中被视为次要，因此在重要决策中基本上被排除在外”。Rebenatto 的关注点突出了其中的原因。他正在银行风险管理领域的一小部分范围内寻找：全职风险管理人员的范畴。

有趣的是，Rebenatto 对硬科学领域的博士们缺乏常识、对公式的自闭关注、对更大局的无知感到痛心。他对他人的批评与他自己的观点如此一致，这表明了一种非常有趣的偏见。
