-->yml

分类：未分类

日期：2024-05-18 06:45:36

-->

# 介绍 QuantLib：带股息的美国期权定价 | 金融与科技事事……

> 来源：[`mhittesdorf.wordpress.com/2013/11/17/introducing-quantlib-american-option-pricing-with-dividends/#0001-01-01`](https://mhittesdorf.wordpress.com/2013/11/17/introducing-quantlib-american-option-pricing-with-dividends/#0001-01-01)

在这篇关于期权定价的最后一篇博客中，我将讨论在美式行权规则下，考虑在期权到期前预期支付的股息，对期权估值的机制。具体来说，我将展示如何计算一系列于 2014 年 2 月 21 日到期的英特尔（INTC）看涨期权的价值，其中预期在 2014 年 2 月 5 日支付 0.22 的股息。

美式期权与欧式期权不同，可以在期权到期前任何时候行使。这种特权带来了一定的溢价，使得美式期权通常比其欧式对应期权更贵，在其他条件相同的情况下。股息代表了一种预期的未来现金流，它减少了标的资产的前向价格的价值，从而影响了相应期权的价值。更具体地说，与没有股息的相同期权相比，股息会减少看涨期权的价值，增加看跌期权的价值，在其他条件相同的情况下。

在之前的博客中，我依赖于 Black-Scholes 作为我的理论期权定价模型。严格来说，Black-Scholes 并不支持不进行调整就定价带有股息的美式期权。因此，通常使用如二叉树或有限差分的格子模型来定价美式期权。或者，如果速度是一个主要考虑因素，美国解析近似之一，例如[Barone-Adesi-Whaley](http://www.investopedia.com/terms/b/barone-adesi-whaley-model.asp)可能是一个不错的选择。幸运的是，QuantLib 提供了许多不同类型的美式期权定价模型的支持，这些模型在速度、数值稳定性和复杂性方面有所不同，同时产生非常接近的期权估值。

在这篇博客中，我将使用 Crank-Nicolson 有限差分格子模型作为定价引擎，该引擎由[FDAmericanEngine<CrankNicolson>](http://quantlib.org/reference/class_quant_lib_1_1_f_d_american_engine.html)类实现。此外，我并不会展示一个过于简化的例子，该例子假设利率、股息和波动率期限结构平坦，而是将从 Interactive Brokers 市场数据（见下面的屏幕截图）和当前 LIBOR 利率中引导出所需的股息、利率和波动率曲线。这应该能让你对在“现实世界”中估值期权所需的东西有一个很好的了解。

![inteloptions-11-15-2013](https://mhittesdorf.wordpress.com/wp-content/uploads/2013/11/inteloptions-11-15-2013.png)

那么让我们从构建必要的市场数据曲线开始。首先，我将介绍一个函数，该函数将用于构建 2014 年 2 月 INTC 看涨期权的波动率微笑曲线。（想了解波动率微笑曲线，请参阅我之前的文章[这里](https://mhittesdorf.wordpress.com/2013/08/29/introducing-quantlib-implied-volatility/)。）该函数依赖于 QuantLib [BlackVarianceSurface](http://quantlib.org/reference/class_quant_lib_1_1_black_variance_surface.html)类，它支持罢工水平的波动率。以下是代码：

```
 #include <cstdlib>
#include <iostream>
#include <ql/quantlib.hpp>

using namespace QuantLib;

boost::shared_ptr<BlackVolTermStructure> bootstrapVolatilityCurve(const Date& 
evaluationDate, const std::vector<Real>& strikes, 
const std::vector<Volatility>& vols, const Date& expiration) {

    Calendar calendar = UnitedStates(UnitedStates::NYSE);

    std::vector<Date> expirations;
    expirations.push_back(expiration);

    Matrix volMatrix(strikes.size(), 1);

    //implied volatilities from Interactive Brokers
    for (int i=0; i< vols.size(); ++i) {
        volMatrix[i][0] = vols[i];
    }

    return boost::shared_ptr<BlackVolTermStructure>(new BlackVarianceSurface(evaluationDate, calendar,
expirations, strikes, volMatrix, Actual365Fixed()));		
} 
```

接下来，让我们引导 LIBOR 零利率曲线，该曲线提供了折现期权收益所需的利率。美元 LIBOR 利率是从[globalrates.com](http://www.global-rates.com/interest-rates/libor/american-dollar/american-dollar.aspx)网站上获取的。以下代码如下：

```
 #include <cstdlib>
#include <iostream>
#include <ql/quantlib.hpp>
#include <boost/assign/std/vector.hpp>

using namespace QuantLib;

boost::shared_ptr<YieldTermStructure> bootstrapLiborZeroCurve(const Date& evaluationDate) {

    using namespace boost::assign;

    //bootstrap from USD LIBOR rates;
    IborIndex libor = USDLiborON();  
    const Calendar& calendar = libor.fixingCalendar();
    const Date& settlement = calendar.advance(evaluationDate, 2, Days);
    const DayCounter& dayCounter = libor.dayCounter();       
    Settings::instance().evaluationDate() = settlement;

    //rates obtained from http://www.global-rates.com/interest-rates/libor/libor.aspx 
    Rate overnight = .10490/100.0;
    Rate oneWeek = .12925/100.0;
    Rate oneMonth = .16750/100.0;
    Rate twoMonths = .20700/100.0;
    Rate threeMonths = .23810/100.0;
    Rate sixMonths = .35140/100.0;
    Rate twelveMonths = .58410/100.0;

    std::vector<boost::shared_ptr<RateHelper>> liborRates;
    liborRates += boost::shared_ptrRateHelper>(new DepositRateHelper(overnight,
        boost::shared_ptr<IborIndex>(new USDLiborON()))); 
    liborRates += boost::shared_ptr<RateHelper>(new DepositRateHelper(oneWeek,
        boost::shared_ptr<IborIndex>(new USDLibor(Period(1, Weeks)))));
    liborRates += boost::shared_ptr<RateHelper>(new DepositRateHelper(oneMonth,
        boost::shared_ptr<IborIndex>(new USDLibor(Period(1, Months)))));
    liborRates += boost::shared_ptr<RateHelper>(new DepositRateHelper(twoMonths,
	boost::shared_ptr<IborIndex>(new USDLibor(Period(2, Months)))));
    liborRates += boost::shared_ptr<RateHelper>(new DepositRateHelper(threeMonths,
	boost::shared_ptr<IborIndex>(new USDLibor(Period(3, Months)))));
    liborRates += boost::shared_ptr<RateHelper>(new DepositRateHelper(sixMonths,
	boost::shared_ptr<IborIndex>(new USDLibor(Period(6, Months)))));
    liborRates += boost::shared_ptr<RateHelper>(new DepositRateHelper(twelveMonths,
	boost::shared_ptr<IborIndex>(new USDLibor(Period(12, Months)))));

    //use cubic interpolation
    boost::shared_ptr<YieldTermStructure> yieldCurve = 
    boost::shared_ptr<YieldTermStructure>(new [PiecewiseYieldCurve](http://quantlib.org/reference/class_quant_lib_1_1_piecewise_yield_curve.html)<ZeroYield, 
Cubic>(settlement, liborRates, dayCounter));

    return yieldCurve;	
} 
```

我们最后需要生成的曲线提供了英特尔的年化股息收益率。以下是引导股息曲线的代码：

```
 #include <cstdlib>
#include <iostream>
#include <ql/quantlib.hpp>
#include <boost/format.hpp>

using namespace QuantLib;

boost::shared_ptr<ZeroCurve> bootstrapDividendCurve(const Date& evaluationDate, 
const Date& expiration, const Date& exDivDate, Real underlyingPrice, Real annualDividend) {

    UnitedStates calendar(UnitedStates::NYSE);
    Settings::instance().evaluationDate() = evaluationDate;
    Real settlementDays = 2.0;

    Real dividendDiscountDays = (expiration - evaluationDate) + settlementDays;
    std::cout << boost::format("Dividend discounting days: %d") %
 dividendDiscountDays << std::endl;
    Rate dividendYield = (annualDividend/underlyingPrice) * dividendDiscountDays/365;

    // ex div dates and yields
    std::vector<Date> exDivDates;
    std::vector<Rate&gt dividendYields;

    //last ex div date and yield
    exDivDates.push_back(calendar.advance(exDivDate, Period(-3, Months), 
ModifiedPreceding, true));
    dividendYields.push_back(dividendYield);

    //currently announced ex div date and yield
    exDivDates.push_back(exDivDate);
    dividendYields.push_back(dividendYield);

    //next ex div date (projected) and yield
    Date projectedNextExDivDate = calendar.advance(exDivDate, Period(3, Months), 
ModifiedPreceding, true); 
    std::cout << boost::format("Next projected ex div date for INTC: %s") % 
projectedNextExDivDate << std::endl;
    exDivDates.push_back(projectedNextExDivDate);
    dividendYields.push_back(dividendYield);

    return boost::shared_ptr<ZeroCurve>(new ZeroCurve(exDivDates, dividendYields, 
ActualActual(), calendar));

} 
```

现在我们已经有了引导所有市场数据曲线的代码，英特尔看涨期权的定价代码相当简单：

```
 #include <cstdlib>
#include <iostream>
#include <ql/quantlib.hpp>
#define BOOST_AUTO_TEST_MAIN
#include <boost/test/unit_test.hpp>
#include <boost/detail/lightweight_test.hpp>
#include <boost/format.hpp>
#include <boost/assign/std/vector.hpp>

using namespace QuantLib;

BOOST_AUTO_TEST_CASE(testAmericanOptionPricingWithDividends) {

    using namespace boost::assign;

    //set up calendar/dates
    Calendar calendar = UnitedStates(UnitedStates::NYSE);
    Date today(15, Nov, 2013);
    Real settlementDays = 2;
    Date settlement = calendar.advance(today, settlementDays, Days);
    Settings::instance().evaluationDate() = today;

    //define options to price
    Option::Type type(Option::Call);
    Real underlying = 24.52;

    // INTC Feb 21 strikes
    std::vector strikes;
    strikes += 22.0, 23.0, 24.0, 25.0, 26.0, 27.0, 28.0;

    // volatility for each strike above
    std::vector vols;
    vols += .23356, .21369, .20657, .20128, .19917, .19978, .20117;

    // Feb 2014 expiration      
    Date expiration(21, Feb, 2014);

    //INTC dividend information - .90 per year paid quarterly
    Date exDivDate(5, Feb, 2014);
    Real annualDividend = .90;

    //build yield term structure from LIBOR rates 
    Handle<YieldTermStructure> yieldTermStructure(bootstrapLiborZeroCurve(today));

    //build dividend term structure
    Handle<YieldTermStructure> dividendTermStructure(bootstrapDividendCurve(today, 
expiration, exDivDate, underlying, annualDividend));

    //build vol term structure 
    Handle<BlackVolTermStructure> volatilityTermStructure(bootstrapVolatilityCurve(today, 
strikes, vols, expiration));

    //instantiate BSM process
    Handle<Quote> underlyingH(boost::shared_ptr(new SimpleQuote(underlying)));
    boost::shared_ptr<BlackScholesMertonProcess> bsmProcess(new BlackScholesMertonProcess(underlyingH, 
dividendTermStructure, yieldTermStructure, volatilityTermStructure));

    //instantiate pricing engine
    boost::shared_ptr<PricingEngine> pricingEngine(new FDAmericanEngine<CrankNicolson>
(bsmProcess, 801, 800));

    //price the options
    boost::shared_ptr<Exercise> americanExercise(new AmericanExercise(settlement, expiration));
    for (Real strike: strikes) {
        boost::shared_ptr<StrikedTypePayoff> payoff(new PlainVanillaPayoff(type, strike));
	VanillaOption americanOption(payoff, americanExercise);
	americanOption.setPricingEngine(pricingEngine);
	Real tv = americanOption.NPV();
	std::cout << boost::format("Intel %s %.2f %s value is: %.2f") % 
expiration % strike % type % tv  << std::endl;
	std::cout << boost::format("Delta: %.4f") % americanOption.delta() << std::endl;
	std::cout << boost::format("Gamma: %.4f") % americanOption.gamma() << std::endl;
     }
} 
```

当代码运行时，它生成了以下 22 至 28 罢工选项的价值和希腊字母：

`英特尔 2014 年 2 月 21 日 22.00 看涨期权价值为：2.77

Delta: 0.8287

Gamma: 0.0883

英特尔 2014 年 2 月 21 日 23.00 看涨期权价值为：1.94

Delta: 0.7312

Gamma: 0.1230

英特尔 2014 年 2 月 21 日 24.00 看涨期权价值为：1.28

Delta: 0.5922

Gamma: 0.1486

英特尔 2014 年 2 月 21 日 25.00 看涨期权价值为：0.78

Delta: 0.4380

Gamma: 0.1544

英特尔 2014 年 2 月 21 日 26.00 看涨期权价值为：0.45

Delta: 0.2948

Gamma: 0.1364

英特尔 2014 年 2 月 21 日 27.00 看涨期权价值为：0.24

Delta: 0.1835

Gamma: 0.1046

英特尔 2014 年 2 月 21 日 28.00 看涨期权价值为：0.13

Delta: 0.1068

Gamma: 0.0720`

上述打印的期权价值在 Interactive Brokers 截图中的每个罢工价格都在或略高于买卖价差。一角钱或两角的偏差可能是由于 Interactive Brokers 所使用的模型与 QuantLib Crank-Nicolson 模型的差异，输入市场数据的差异，或者甚至可能是交易机会（即“边缘”）。实际上，认识到、调整或利用理论期权价值与市场之间的偏差是现代期权定价和交易的核心。

有了这个，我将结束这篇有点长的帖子。我深信你从中获得了乐趣，并学到了一些有关使用 QuantLib 定价分红股票的美股期权的方法。请随时在下面提交你的评论或问题。我会尽我所能尽快回复你。当然，也要和 QuantLib 一起玩得开心！
