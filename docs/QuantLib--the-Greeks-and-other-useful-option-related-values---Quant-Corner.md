<!--yml

分类：未分类

日期：2024-05-18 08:09:24

-->

# QuantLib, the Greeks and other useful option-related values | Quant Corner

> 来源：[`quantcorner.wordpress.com/2011/02/06/quantlib-the-greeks-and-other-useful-option-related-values/#0001-01-01`](https://quantcorner.wordpress.com/2011/02/06/quantlib-the-greeks-and-other-useful-option-related-values/#0001-01-01)

在本文中，我们向读者提供了**C++/QuantLib**代码，该代码可以计算最常用的**期权敏感性**——**希腊字母**——以及期权的**弹性**和其**隐含波动率**。在回顾**希腊字母**公式之前，作为**Black-Scholes 公式**的**偏导数**。并且，我们非常简要地指示了如何计算**隐含波动率**。

到处都可以读到**QuantLib**对初学者来说过于复杂。本文再次展示了**QuantLib**的强大之处。实际上，一旦在代码中定义了期权参数和 Quantlib 工具，我们就能一次获得所有的希腊字母。我的意思是**QuantLib**绝对值得一试。

### Delta

![](img/7d956fbec1b9ef9c8af2c8f958984351.png "delta")

### Gamma

![](img/7d956fbec1b9ef9c8af2c8f958984351.png "gamma")

### Theta

![](img/7d956fbec1b9ef9c8af2c8f958984351.png "theta")

### Vega

![](img/7d956fbec1b9ef9c8af2c8f958984351.png "vega")

### 弹性度

弹性度量了期权价格对其标的资产价格百分比变动的敏感性。

![](https://quantcorner.wordpress.com/wp-content/uploads/2011/02/elasticity1.jpg)

### 隐含波动率

获取隐含波动率并非易事。我们必须解出 Black-Scholes 方程 V(S[0], t[0]; σ, r; E, T ) = 已知值对于σ。而且，所谓的牛顿-拉弗森方法通常被使用。

### 基于 C++/QuantLib 的代码

为了尽可能简单，我们回到最近编程的基本**欧式股票期权**。我们将我们的计算结果与来自**Excel**定价器的**E.G.Haug**手册中伴随的**The complete guide to option pricing formulas, 2nd Ed.**的结果进行了基准测试。

_________________________________

期权类型 =              看跌

期权执行价格 =              50

股价 =              47

无风险利率 =              5%

股息收益率 =              0%

波动率 =              20%

期权到期日 =    2011 年 12 月 10 日

__________________________________

```
#include <ql/quantlib.hpp>

#ifdef BOOST_MSVC
#endif

using std::cout;
using std::endl;
using std::setprecision;
using namespace QuantLib;

#if defined(QL_ENABLE_SESSIONS)
namespace QuantLib
{
	Integer sessionId() { return 0; }
}
#endif

int main(int, char* []) {

	try {
		// Calendar stuff set up
		Calendar calendar = TARGET();
		Date todaysDate(6, February, 2011);
		Settings::instance().evaluationDate() = todaysDate;
		DayCounter dayCounter = Actual365Fixed();

		// Option parameter
		Option::Type type(Option::Put);
		Real underlying = 50;
		Real strike = 47;
		Spread dividendYield = 0.00;
		Rate riskFreeRate = 0.05;
		Volatility volatility = 0.20;
		Date maturity(10, December, 2011);

		// European exercise type handler
		boost::shared_ptr<Exercise> europeanExercise(
			new EuropeanExercise(
			maturity));

		// Quote (=underlying price) handler
		Handle<Quote> underlyingH(
			boost::shared_ptr<Quote>(
			new SimpleQuote(underlying)));

		// Yield term structure handler
		Handle<YieldTermStructure> flatTermStructure(
			boost::shared_ptr<YieldTermStructure>(
			new FlatForward(
			todaysDate,
			riskFreeRate,
			dayCounter)));

		// Dividend handler
		Handle<YieldTermStructure> flatDividendTermStructure(
			boost::shared_ptr<YieldTermStructure>(
			new FlatForward(
			todaysDate,
			dividendYield,
			dayCounter)));

		// Volatility handler
		Handle<BlackVolTermStructure> flatVolTermStructure(
			boost::shared_ptr<BlackVolTermStructure>(
			new BlackConstantVol(
			todaysDate,
			calendar,
			volatility,
			dayCounter)));

		// Payoff handler
		boost::shared_ptr<StrikedTypePayoff> payoff(
			new PlainVanillaPayoff(
			type,
			strike));

		// Black Scholes
		boost::shared_ptr<BlackScholesMertonProcess> bsmProcess(
			new BlackScholesMertonProcess(
			underlyingH,
			flatDividendTermStructure,
			flatTermStructure,
			flatVolTermStructure));

		// Option characteristics
		VanillaOption europeanOption(payoff, europeanExercise);

		// Pricing Engine : in this case BS for European options
		europeanOption.setPricingEngine(boost::shared_ptr<PricingEngine>(
			new AnalyticEuropeanEngine(
			bsmProcess)));

		/**************
		*  OUTPUTTING *
		***************/

		// 1) Option parameters
		cout << "Option type =\t\t" << type << endl;
		cout << "Maturity =\t\t" << maturity << endl;
		cout << "Underlying price =\t" << underlying << endl;
		cout << "Strike =\t\t" << strike << endl;
		cout << "Risk-free int. rate =\t" << setprecision(2) << io::rate(riskFreeRate) << endl;
		cout << "Dividend yield =\t" << io::rate(dividendYield) << endl;
		cout << "Volatility =\t\t" << setprecision(2) << io::volatility(volatility) << endl;
		cout << endl;
		cout << endl;

		// 2) Calculation results
		cout << "Option price :\t" << setprecision(5) << europeanOption.NPV() << endl;
		cout << "Delta :\t\t" << setprecision(5) << europeanOption.delta() << endl;
		cout << "Elasticity :\t" << setprecision(5) << europeanOption.elasticity() << endl;
		cout << "Gamma :\t\t" << setprecision(5) << europeanOption.gamma() << endl;
		cout << "Vega :\t\t" << setprecision(5) << europeanOption.vega()/100 << endl;
		cout << "Theta :\t\t" << setprecision(5) << europeanOption.thetaPerDay() << endl;
		cout << "Rho :\t\t" << setprecision(5) << europeanOption.rho()/100 << endl;
		cout << endl;

		return 0;

		}
		catch (std::exception& e)
		{
			std::cerr << e.what() << endl;
			return 1;
		}
		catch (...)
		{
			std::cerr << "unknown error" << endl;
			return 1;
		}
}
```
