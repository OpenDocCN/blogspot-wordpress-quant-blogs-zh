<!--yml

分类：未分类

日期：2024-05-18 06:46:23

-->

# 介绍 QuantLib：期权理论与定价 | 所有关于金融与科技的事物……

> 来源：[`mhittesdorf.wordpress.com/2013/07/05/introducing-quantlib-option-theory-and-pricing/#0001-01-01`](https://mhittesdorf.wordpress.com/2013/07/05/introducing-quantlib-option-theory-and-pricing/#0001-01-01)

欢迎回来！在本文中，我将展示如何使用 QuantLib 定价期权。具体来说，我们将定价一种在主要公共衍生品交易所上市的标准期权，比如芝加哥期权交易所（CBOE）的期权。但首先，我需要介绍和定义一些对于期权定价理论至关重要的基本概念和术语。

期权是一种其价值源于另一种工具，通常称为*标的资产*的金融工具。因此，期权属于金融工具的一个类别，称为*衍生品*。衍生品的估值是 QuantLib 真正擅长的领域，因为这正是创建该库的初衷之一。

股票期权是一种衍生品，其价值取决于股票（S）的价格，比如 AAPL。期权分为两种类型，看涨期权和看跌期权。看涨期权赋予买家权利，但不负有义务，以期权的*行权*价格购买一定数量的标的资产，通常是 100 股，行权价格通常缩写为‘K’。看跌期权则赋予买家权利，但不负有义务，以行权价格出售一定数量的股份。

期权有一个关联的到期日期，在此日期之后，期权的买家将失去购买或出售标的资产的权利，期权变得一文不值。交易所交易的期权有标准的到期日期，通常是每月第三个星期五。近年来，交易所也列出了每周到期的期权，月末、季末等。

如果期权受*欧洲*式行权规则约束，看涨或看跌期权的买家只能在期权到期时选择购买或出售标的资产。而*美式*期权则允许期权买方在期权到期前的任何时间行使其权利。

理解如何定价期权的第一步是考虑期权的*收益。*期权的收益定义了期权到期前一刻的价值。

对于看涨期权，收益公式是：**max(0, S – K)**

对于看跌期权，收益公式是：**max(0, K – S)**

**由于未来股票价格（即远期价格）是未知的，期权在到期前的任何时间点的价格都必须考虑到股票可能采取的上升或下降的可能路径，从当前位置，从现在到期权到期。期权的基础价格“波动”的速度由其*波动率*衡量，这个概念上对应于基础回报的一个标准差变化，通常计算为 ln(St+1/St)。对于目前*价外期权*，其中回报公式等于零，更高的波动率意味着更高的期权价格，因为期权最终*价内*回报大于零的可能性增加了。

正如您可能从我的早期“介绍 QuantLib”文章中回忆起的那样，为了确定未来现金流的价值，如期权支付，需要计算该现金流的现值。我们通过将现金流以无风险利率（r）折现来实现，假设连续复利。由于期权的未来现金流基于随机变量，即基础远期价格，必须折现期权的*预期价值*。从概念上讲，看涨期权的价值由以下公式决定，其中 E 是期望运算符。

**Vc= e^(-rt) * E(max(0,  S – K))**

同样，看跌期权的价值由以下公式实现：

**Vp = e ^ (-rt) *  E(max(0, K – S))**

重要的是要注意，这种分析做出了简化的假设，即在期权有效期内，基础股票不支付股息。

从 Hull 的《期权、期货和其他衍生品，第 6 版》第十三章附录中，看涨期权收益的期望值定义为：

![expectedvaluecalloption](https://mhittesdorf.wordpress.com/wp-content/uploads/2013/07/expectedvaluecalloption2.png)

其中 f(S) 是 S 的自然对数的概率密度函数（pdf），dS 表示在非常短的时间段内股票价格的变化。看跌期权的公式类似——只需将收益计算中的（K – S）替换即可。

你可能在问为什么 f(S) 是基础价格的对数分布的 pdf。这是由于基础价格呈对数正态分布。考虑到股票价格不能低于零，且股票回报率（假设连续复利）计算为 ln(St+1/St) 时呈正态分布，这一点必须是如此。为了更深入地了解股票价格的对数正态性质，建议你参考上面提到的 Hull 书中第 13.1 节。

考虑到到目前为止所展示的内容，我们是否有足够的信息来实际定价一个看涨期权呢？事实证明，我们确实有。查看下面的源代码列表，它通过数值积分计算了看涨期权的收益乘以给定 S 值的概率从 K 到 10*K（一个相对较大的数，有效作用为“无穷大”）。

```
 #include <iostream> 
#include <cstdlib>
#define BOOST_AUTO_TEST_MAIN
#include <boost/test/unit_test.hpp>
#include <boost/detail/lightweight_test.hpp>
#include <ql/quantlib.hpp>
#include <boost/format.hpp>
#include <boost/math/distributions.hpp>
#include <boost/function.hpp>

namespace {

using namespace QuantLib;

Real expectedValueCallPayoff(Real spot, Real strike,
        Rate r, Volatility sigma, Time t, Real x) {
    Real mean = log(spot)+(r - 0.5 * sigma * sigma) * t;
    Real stdDev = sigma * sqrt(t);
    boost::math::lognormal d(mean, stdDev);
    return [PlainVanillaPayoff](http://quantlib.org/reference/class_quant_lib_1_1_plain_vanilla_payoff.html)(Option::Type::Call, strike)(x) * boost::math::pdf(d, x);
}

BOOST_AUTO_TEST_CASE(testPriceCallOption) {
    Real spot = 100.0; //current price of the underlying stock (S)
    Rate r = 0.03; //risk-free rate
    Time t = 0.5;  //half a year
    Volatility vol = 0.20; //estimated volatility of underlying
    Real strike = 110.0; // strike price of the call (K)

    //b need not be infinity, but can just be a large number that is improbable
    Real a = strike, b = strike * 10.0;

    boost::function< Real(Real) > ptrToExpectedValueCallPayoff = 
        boost::bind(&expectedValueCallPayoff, spot, strike, r, vol, t, _1);

    Real absAcc = 0.00001;
    Size maxEval = 1000;
    SimpsonIntegral numInt(absAcc, maxEval); 

    /* numerically integrate the call option payoff function from a to b and
     * calculate the present value using the risk free rate as the discount factor
     */ 
    Real callOptionValue = numInt(ptrToExpectedValueCallPayoff, a, b) * std::exp(-r * t); 

    std::cout << "Call option value is: " << callOptionValue << std::endl;
}}
```

运行此代码后，会产生以下输出：

`看涨期权价值为：2.6119`

这是看涨期权的正确价格吗？让我们将价格与我在网上找到的第三方期权定价计算器[`www.option-price.com`](http://www.option-price.com/index.php)进行比较。下面是屏幕截图：

![wwoptionpricecom](https://mhittesdorf.wordpress.com/wp-content/uploads/2013/07/wwoptionpricecom.png)

正如你所见，列出的“理论价格”与我们在“看涨期权”列中计算出的值相符！所以我们应该确信所展示的方法从理论上讲是正确的。然而，正如你将在接下来的文章中看到的，这个方法过于简化，因为它假设波动率恒定、没有股息和一个单一的、恒定的贴现因子。与替代方法相比，数值积分也非常慢且不太灵活。

在现实世界中，为了准确地定价和交易期权，我们必须找到一种方法来建模和管理随时间、到期和/或执行价变化波动率、股息和利率曲线。在电子、高频交易的时代的背景下，期权价格必须在微秒级别进行计算。幸运的是，QuantLib 为“现实世界”期权定价提供了广泛、复杂的框架，我将在不久的将来深入研究。所以请随时关注更深入、全面的 QuantLib 定价期权内容。

我希望你能享受我博客的最新篇章。下次见，玩转 QuantLib 吧，和往常一样，我期待听到反馈、评论和问题。谢谢！**
