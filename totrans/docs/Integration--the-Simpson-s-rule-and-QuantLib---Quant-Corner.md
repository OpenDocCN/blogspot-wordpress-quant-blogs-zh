<!--yml
category: 未分类
date: 2024-05-18 08:09:54
-->

# Integration, the Simpson´s rule and QuantLib | Quant Corner

> 来源：[https://quantcorner.wordpress.com/2011/02/14/integration-the-simpson%c2%b4s-rule-and-quantlib/#0001-01-01](https://quantcorner.wordpress.com/2011/02/14/integration-the-simpson%c2%b4s-rule-and-quantlib/#0001-01-01)

 ***QuantLib** provides with numerous mathematical and function-related tools, and it closely works with the **Boost** library.*

 *Here, we deal with **integrals**. More specifically, we implement the well-known **Simpson’s integral**. We keep the things concrete by calculating the value of a call option from its integral representation.

The integral of a function is the area between the curve and the x-axis. Limits can be defined so that we have a **definite integral**. The integral will thus be computed by dividing the x-axis and the corresponding area between the curve and the x-axis between the upper and the lower bound.

We can write :
[![](img/cef1354e0af385d0bcad2788fb745360.png "integral")](https://quantcorner.wordpress.com/wp-content/uploads/2011/02/integral.jpg)

where **a** is the lower limit, and **b** the upper limit.

The integral representation of a call is
[![](img/621fdd7fac4ce84031e911513ed9b8cb.png "integral_call")](https://quantcorner.wordpress.com/wp-content/uploads/2011/02/integral_call.jpg)

where f(x) is the **lognormal density** with **mean** [](https://quantcorner.wordpress.com/wp-content/uploads/2011/02/integral_call.jpg)**[![](img/2fcb14e226b469cea449755ad0ce76cc.png "mean_log_normal_density")](https://quantcorner.wordpress.com/wp-content/uploads/2011/02/mean_log_normal_density1.jpg)**

And **standard deviation
**![](img/2ad4f40d1fb4a770d20b61418cc5ee8e.png "standard_deviation_log_normal_density")****

The **Simpson’s rule** gets numerical approximations of definite integrals
 *[![](img/44b142b2896a3b3f0d23337756e7324c.png "simpson_rule")](https://quantcorner.wordpress.com/wp-content/uploads/2011/02/simpson_rule.jpg)*

 *Our code uses the **boost::bind** class, which is a predefined metafunction. Please, refer to the Boost documentation.

The **a**-lower limit is the strike, and the **b**-upper limit is an arbitrary higher value. In this case 10 x **a**.

```
#include<ql\quantlib.hpp>
#include <boost/math/distributions.hpp>
#include<math.h>

using namespace QuantLib;

Real callOptionFunction(
	Real underlying,
	Real strike,
	Rate riskFreeInterestRate,
	Volatility volatility,
	Time tau,
	Real x){
		Real mean = log(underlying) + (riskFreeInterestRate
			- 0.5 * volatility * volatility) * tau ;

		Real standardDeviation = volatility * sqrt(tau);

		boost::math::lognormal_distribution<>d(mean, standardDeviation);
		return (x - strike) * pdf(d,x) * exp (-riskFreeInterestRate * tau);
}

int main(int, char*[]){

	//option parameters
	Real underlying = 30;
	Real strike = 36;
	Rate riskFreeInterestRate = 0.06;
	Time tau = 0.5; // 0,5 year
	Volatility volatility = 0.20;

	//Integration parameters : absolute accuracy
	//and maximum number of evaluations
	Real absoluteAccuracy = 1e-4;
	Size maxEvaluations = 1e3;

	boost::function<Real(Real)> ptrF;
	ptrF = boost::bind(
		&callOptionFunction,
		underlying,
		strike,
		riskFreeInterestRate,
		volatility,
		tau,
		_1);

	SimpsonIntegral numInt(
		absoluteAccuracy,
		maxEvaluations);

	std::cout << "Call option value : " << numInt(
		ptrF,
		strike,/*lower limit a*/
		10*strike)/*upper limit b*/ << std::endl;

	return 0;
}
```**