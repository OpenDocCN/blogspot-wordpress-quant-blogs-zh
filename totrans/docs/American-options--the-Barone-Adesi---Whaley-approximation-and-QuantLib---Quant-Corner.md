<!--yml
category: 未分类
date: 2024-05-18 08:09:42
-->

# American options, the Barone-Adesi & Whaley approximation and QuantLib | Quant Corner

> 来源：[https://quantcorner.wordpress.com/2011/02/20/american-options-the-barone-adesi-whaley-approximation-and-quantlib/#0001-01-01](https://quantcorner.wordpress.com/2011/02/20/american-options-the-barone-adesi-whaley-approximation-and-quantlib/#0001-01-01)

In this post, we shall implement the widely-used Barone-Adesi & Whaley approximation using the **QuantLib** library.

Here, our interest lies in **futures options**. For example, we would like to price *options on agricultural futures* quoted on the **CME** markets.

As Barone-Adesi & Whaley (1987) explain in their seminal paper, the cost of carrying any futures position is equal to 0\. We thus set the cost-of-carry **b = 0** to work out the approximation method proposed by these authors.

### Introducing remarks

Most of the code used here to implement the BAW approximation is derived from previous posts. Nevertheles, some improvements are made:

– The program gets by itself today’s date, and associates it with the date the option price is calculated. This is done throught :

```
Date today = QuantLib::Date::todaysDate();
		Settings::instance().evaluationDate() = today;
```

– Option parameters are now set by the user at running-time. This is easily done by a **std::cout** and **std::cin** series:

```
		cout << "Call or put option (c/p)?: \t\t";
		cin >> optionType;
```

– The code is wrapped in an infinite loop. This way the program can be actually used as a simple option pricer for **American futures options**:

```
bool loopEnd = false;
do
{
} while (loopEnd != true);
```

### The code that implements the BAW approximation

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

### Concluding comments

This option pricer has been written quite easily, as it grounds on previous codes. The point is that **QuantLib** has a large variety of classes allowing to implement as many **numerical** as well as **analytical schemes** to price options. And, it is quite straightforward to re-engineer a piece of code so that to implement another scheme.