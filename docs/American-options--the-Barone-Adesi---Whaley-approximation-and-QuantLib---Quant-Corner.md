<!--yml

category: 未分类

日期：2024-05-18 08:09:42

-->

# 美国期权，Barone-Adesi & Whaley 近似和 QuantLib | Quant Corner

> 来源：[`quantcorner.wordpress.com/2011/02/20/american-options-the-barone-adesi-whaley-approximation-and-quantlib/#0001-01-01`](https://quantcorner.wordpress.com/2011/02/20/american-options-the-barone-adesi-whaley-approximation-and-quantlib/#0001-01-01)

在本文中，我们将使用**QuantLib**库实现广泛使用的 Barone-Adesi & Whaley 近似。

这里，我们感兴趣的是**期货期权**。例如，我们想要定价在**CME**市场上报价的*农产品期货期权*。

正如 Barone-Adesi & Whaley（1987）在他们的开创性论文中所解释的那样，任何期货头寸的持有成本都等于 0。因此，我们将持有成本**b = 0**设置为计算这些作者提出的近似方法的基础。

### 引入备注

这里用于实现 BAW 近似的大部分代码都来自以前的帖子。尽管如此，还是做了一些改进：

– 程序会自行获取今天的日期，并将其与计算期权价格的日期关联起来。这是通过以下方式完成的：

```
Date today = QuantLib::Date::todaysDate();
		Settings::instance().evaluationDate() = today;
```

– 选项参数现在由用户在运行时设置。通过一系列**std::cout**和**std::cin**很容易实现这一点：

```
		cout << "Call or put option (c/p)?: \t\t";
		cin >> optionType;
```

– 代码被包装在一个无限循环中。这样程序实际上可以用作**美国期货期权**的简单期权定价器：

```
bool loopEnd = false;
do
{
} while (loopEnd != true);
```

### 实现 BAW 近似的代码

```
#include <ql\quantlib.hpp>

using std::cout;
using std::cin;
using std::endl;
using std::setprecision;
using std::string;

using namespace QuantLib;

int main(int, char*[]){

	bool loopEnd = false;
	do
	{

	try{

		// Option Parameters
		Option::Type type;
		Real underlying;
		Real strike;
		Rate riskFreeRate;
		Spread dividendYield = 0;
		Volatility volatility;
		double optionValue;

		std::string optionType;
		std::string c;

		int maturityD;
		int maturityM;
		int maturityY;

		cout << "Call or put option (c/p)?: \t\t";
		cin >> optionType;

		cout << "Enter expiration date (dd mm yyyy): \t";
		cin >> maturityD >> maturityM >> maturityY;

		cout << "Enter strike: \t\t\t\t";
		cin >> strike;

		cout << "Enter underlying price: \t\t";
		cin >> underlying;

		cout << "Enter volatility (%): \t\t\t";
		cin >> volatility;

		cout << "Enter risk free rate (%): \t\t";
		cin >> riskFreeRate;

		if((optionType == ("c")) || (optionType == "C"))
			type=Option::Call;
		else
			type=Option::Put;

		// Calendar stuff
		Calendar calendar = TARGET();
		Date today = QuantLib::Date::todaysDate();
		Settings::instance().evaluationDate() = today;
		DayCounter dayCounter = Actual365Fixed();
		Date maturity(maturityD, Month (maturityM), maturityY);

		// American exercise style option handler
		boost::shared_ptr<Exercise> americanExercise(
			new AmericanExercise(
			today, maturity));

		// Underlying price handler
		Handle<Quote> underlyingH(
			boost::shared_ptr<Quote>(
			new SimpleQuote(underlying)));

		// Yield term structure handler
		Handle<YieldTermStructure> flatTermStructure(
			boost::shared_ptr<YieldTermStructure>(
			new FlatForward(
			today,
			riskFreeRate/100,
			dayCounter)));

		// Dividend handler
		Handle<YieldTermStructure> flatDividendTermStructure(
			boost::shared_ptr<YieldTermStructure>(
			new FlatForward(
			today,
			dividendYield,
			dayCounter)));

		// Volatility handler
		Handle<BlackVolTermStructure> flatVolTermStructure(
			boost::shared_ptr<BlackVolTermStructure>(
			new BlackConstantVol(
			today,
			calendar,
			volatility/100,
			dayCounter)));

		// Payoff handler
		boost::shared_ptr<StrikedTypePayoff> payoff(
			new PlainVanillaPayoff(
			type,
			strike));

		// Black Scholes
		boost::shared_ptr<BlackScholesMertonProcess> BSMProcess(
			new BlackScholesMertonProcess(
			underlyingH,
			flatDividendTermStructure,
			flatTermStructure,
			flatVolTermStructure));

		// Option characteristics
		VanillaOption americanOption(payoff, americanExercise);

		// Pricing Engine : in this case BS for European options
		americanOption.setPricingEngine(
			boost::shared_ptr<PricingEngine>(
			new BaroneAdesiWhaleyApproximationEngine(
			BSMProcess)));

		optionValue = americanOption.NPV();

		// Outputting
		cout << endl;
		cout << "Option price :\t" << setprecision(5) << optionValue << endl;
		cout << endl;

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

} while (loopEnd != true);
}
```

### 结语

这个期权定价器写起来相当容易，因为它基于以前的代码。关键在于**QuantLib**有许多类可以用来实现**数值**和**分析方案**来定价期权。而且，重新设计代码片段以实现另一种方案非常简单。
