<!--yml
category: 未分类
date: 2024-05-18 08:07:28
-->

# Pricing European equity options with Quantlib | Quant Corner

> 来源：[https://quantcorner.wordpress.com/2011/01/27/a-pricer-for-european-style-options-on-stocks-a-smooth-start-with-quantlib/#0001-01-01](https://quantcorner.wordpress.com/2011/01/27/a-pricer-for-european-style-options-on-stocks-a-smooth-start-with-quantlib/#0001-01-01)

Below is a piece of code to price **European-style options** on **stocks** with **continuous dividend**. Option value is calculated **analytically**.

This is the first code C++ based on **Quantlib** on this blog site. For the one familiar with C++, it clearly isn’t professional coding. But, we don’t care that much for now. It is a starting point.

It provides the reader with a base structure that will later be improved and derived to price other option types and/or to use other computing methods. Thus, it is very important to understand well this code. Please, refer to both the **Quantlib** and **Boost** documentations.

We end up this post with comments on  required and possible improvements.

________________________________________
Option type = call
Option strike = 40
Stock Price = 47
Risk-free rate = 5%
Volatility = 20%
Option expiration = May 27^(th), 2011
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

### Concluding comments

The code above works well, and our ‘European option calculator’ provides exact calculation results. But, this code is not ‘pure’ C++ coding, and it has limitations from the user’s standpoint.

First, we knew beforehand this code would work. But, what if the code contained fanciful parameters, for example? Thus, we should add some lines able to check some conditions that we ourselves have to define. This is called an **exception mechanism**, that is – in simple terms – code that warns something went wrong, what is was, and where the error in question lies in code. Exception mechanisms generally take the form of **try**, **throw** and **catch** blocks. Exceptions are named explicitly. For example, one might encounter a DividedByZero exception in the maths and finance areas.

Second, this code is all but user-friendly. It computes the value of a unique option the parameters of which are (pre)defined at the time of coding. An obvious improvement is allowing the user to enter its own option parameters. The **STL library** has everything one needs to do that (basically, **std::cin**). Further, one might want a rich-designed user interface. In this case, one good choice is using **Qt** as it allows to build good-looking **GUI** in no-time. For now, we let the reader exploring those possibilities by him(her-)self.