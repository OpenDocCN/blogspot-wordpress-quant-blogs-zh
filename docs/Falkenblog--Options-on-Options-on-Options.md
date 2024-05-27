<!--yml

类别：未分类

日期：2024-05-12 21:30:52

-->

# Falkenblog: Options on Options on Options

> Source: [`falkenblog.blogspot.com/2010/06/options-on-options-on-options.html#0001-01-01`](http://falkenblog.blogspot.com/2010/06/options-on-options-on-options.html#0001-01-01)

权益是公司资产的一种选择，行权价是其总负债。 因此，大多数“权益期权”实际上是对某些人（

[Geske](http://www.global-derivatives.com/index.php/pricing-models-topmenu-37/31?task=view)

)制定了这样明确的模型（但作为一项实际事务几乎不怎么使用）。

VIX 是对标准普尔 500 指数范围内期权价格的加权混合物。 2006 年，通过期货，指数本身直接可交易。 现在我们有了

[VXX](http://www.google.com/finance?client=ob&q=NYSE:VXX)

以及 VXV，新 ETF 允许股票投资者访问 VIX 波动率指数。VXX 每天交易很多，约 3000 万股。这意味着我们现在有 VIX 期权。这些不是对期权的期权，而是对对期权的隐含波动率的期权（哎呀！）。观察到行权隐含波动率，并将其与 SPY 上的暗示进行比较，我们看到它们是完全不同的小动物。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiTkyMdWwYNKP2bDKunmkxUGT6Hkc_rzmD8mPUsQ2Fg2BJwCVrsMjtf8OKHFyhVB5pBlKethWceG5XG9qKgi2AClnxjVJOtDmVy2RqlxJUtaF1xmslBRp5meUfQpDWsv8Gqsamvig/s1600/ivol.gif)

注意，对于 SPY，隐含波动率随着行权价格的下降而增加，因为市场预期指数下行运动与更高的波动率相关。 这

[VXX](http://www.google.com/finance?client=ob&q=NYSE:VXX)

，相比之下，隐含曲线呈现出上升趋势，因为随着波动率的增加，其波动率也会增加。

波动率曲线不平坦表明标准的期权模型，例如布莱克-斯科尔斯模型是错误的，因为它们假定波动率是恒定的。 正如彼得·卡尔所说的，'隐含波动率是

错误

我们在其中使用的波动率

错误

模型以获得

正确

价格”。布莱克-斯科尔斯和其美式期权相对方仍然非常有用，但这突显出实际上任何模型都是在创建的一系列规则内来实施的

临时的

这是由现实所启发的规则。有更多的价格点来确定如何通过行权/到期调整隐含波动率是非常有用的，这

[Sandy Grossman](http://www.jstor.org/pss/1942852)

所谓的“完全市场”，使人们可以看到更多市场驱动概率估计的各种自然状态，其中此时状态不仅是一个价格，而是另一个价格波动率的波动率。
