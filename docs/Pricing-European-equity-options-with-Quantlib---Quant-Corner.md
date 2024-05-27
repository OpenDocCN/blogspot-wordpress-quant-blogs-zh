<!--yml

分类：未分类

日期：2024-05-18 08:07:28

-->

# 使用 Quantlib 定价欧式股票期权 | 量化角

> 来源：[`quantcorner.wordpress.com/2011/01/27/a-pricer-for-european-style-options-on-stocks-a-smooth-start-with-quantlib/#0001-01-01`](https://quantcorner.wordpress.com/2011/01/27/a-pricer-for-european-style-options-on-stocks-a-smooth-start-with-quantlib/#0001-01-01)

下面是一段用于定价带有**连续股息**的**欧式股票期权**的代码。期权价值是**解析地**计算的。

这是基于**Quantlib**的第一个 C++代码。对于熟悉 C++的人来说，这显然不是专业的编程。但是，我们现在不在乎那么多。这是一个起点。

它为读者提供了一个基本结构，后来将进行改进和派生，以定价其他期权类型和/或使用其他计算方法。因此，充分理解这段代码非常重要。请参阅**Quantlib**和**Boost**的文档。

我们在本文的最后提出了需要和可能的改进意见。

________________________________________

期权类型 = 看涨

期权执行价格 = 40

股票价格 = 47

无风险利率 = 5%

波动率 = 20%

期权到期日 = 2011 年 5 月 27 日

________________________________________

```
#include <ql/quantlib.hpp>

using namespace QuantLib;

int main(int, char* []) {

// date set up
Calendar calendar = TARGET();
Date todaysDate(27, Jan, 2011);
Date settlementDate(27, Jan, 2011);
Settings::instance().evaluationDate() = todaysDate;

// option parameters
Option::Type type(Option::Call);
Real stock = 47;
Real strike = 40;
Spread dividendYield = 0.00;
Rate riskFreeRate = 0.05;
Volatility volatility = 0.20;
Date maturity(27, May, 2011);
DayCounter dayCounter = Actual365Fixed();

boost::shared_ptr<Exercise> europeanExercise(new EuropeanExercise(maturity));

Handle<Quote> underlyingH(boost::shared_ptr<Quote>(new SimpleQuote(stock)));

// bootstrap the yield/dividend/vol curves
Handle<YieldTermStructure> flatTermStructure(boost::shared_ptr<YieldTermStructure>(
	new FlatForward(
	settlementDate,
	riskFreeRate,
	dayCounter)));

Handle<YieldTermStructure> flatDividendTS(boost::shared_ptr<YieldTermStructure>(
	new FlatForward(settlementDate,
	dividendYield,
	dayCounter)));

Handle<BlackVolTermStructure> flatVolTS(boost::shared_ptr<BlackVolTermStructure>(
	new BlackConstantVol(
	settlementDate,
	calendar,
	volatility,
	dayCounter)));

boost::shared_ptr<StrikedTypePayoff> payoff(
	new PlainVanillaPayoff(
	type,
	strike));

boost::shared_ptr<BlackScholesMertonProcess> bsmProcess(
	new BlackScholesMertonProcess(
	underlyingH,
	flatDividendTS,
	flatTermStructure,
	flatVolTS));

// our option is European-style
VanillaOption europeanOption(
	payoff,
	europeanExercise);

// computing the option price with the analytic Black-Scholes formulae
europeanOption.setPricingEngine(boost::shared_ptr<PricingEngine>(
	new AnalyticEuropeanEngine(
	bsmProcess)));

// outputting
std::cout << "Option type = " << type << std::endl;
std::cout << "Maturity = " << maturity << std::endl;
std::cout << "Stock price = " << stock << std::endl;
std::cout << "Strike = " << strike << std::endl;
std::cout << "Risk-free interest rate = " << io::rate(riskFreeRate) << std::endl;
std::cout << "Dividend yield = " << io::rate(dividendYield) << std::endl;
std::cout << "Volatility = " << io::volatility(volatility) << std::endl << std::endl;
std::cout<<"European Option value = " << europeanOption.NPV() << std::endl;
return 0;
}
```

### 总结评论

上面的代码运行良好，我们的“欧式期权计算器”提供了确切的计算结果。但是，这段代码不是“纯”的 C++代码，从用户的角度来看，它有局限性。

首先，我们事先知道这段代码是有效的。但是，如果代码中包含了奇异的参数，例如呢？因此，我们应该增加一些能够检查我们自行定义的一些条件的行。这被称为**异常机制**，也就是说——简单来说——代码能够警告出错了什么，是什么出了问题，以及问题出现在代码的哪个位置。异常机制通常采用**try**、**throw**和**catch**代码块的形式。异常是明确命名的。例如，在数学和金融领域可能会遇到一个 DividedByZero 异常。

其次，这段代码几乎不是用户友好的。它计算了一个唯一期权的价值，其参数在编码时间是（预）定义的。一个明显的改进是允许用户输入自己的期权参数。**STL 库**有一个人需要的一切（基本上，**std::cin**）。此外，一个人可能想要一个丰富设计的用户界面。在这种情况下，一个不错的选择是使用**Qt**，因为它可以迅速构建外观良好的**GUI**。现在，我们让读者自己探索这些可能性。
