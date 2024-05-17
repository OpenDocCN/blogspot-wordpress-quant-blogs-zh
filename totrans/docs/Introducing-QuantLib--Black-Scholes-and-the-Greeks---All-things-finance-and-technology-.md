<!--yml
category: 未分类
date: 2024-05-18 06:46:11
-->

# Introducing QuantLib: Black-Scholes and the Greeks | All things finance and technology…

> 来源：[https://mhittesdorf.wordpress.com/2013/07/29/introducing-quantlib-black-scholes-and-the-greeks/#0001-01-01](https://mhittesdorf.wordpress.com/2013/07/29/introducing-quantlib-black-scholes-and-the-greeks/#0001-01-01)

As I wrote the title of this post, I couldn’t help but think of the classic Elton John song, Bennie and the Jets (cue music…) Bennie.. Bennie.. Bennie and the Je..e.ets. Elton John’s hit song was recorded in May of 1973\. The Black-Scholes model was first published in a 1973 paper titled “The Pricing of Options and Corporate Liabilities”. Elton John went on to become an international pop superstar while Myron Scholes and another key contributor to the development of the Black-Scholes equation, Robert Merton, went on to win the Nobel Prize in Economics. Maybe some musically inclined option quants can come up with a silly parody something like “Black-Scholes.. Black-Scholes.. Black-Scholes and the Gre..ee..eeks”.

My awful attempt at humor aside, it’s beyond dispute that the Black-Scholes equation revolutionized derivatives pricing and established Fischer Black, Myron Scholes and Robert Merton as the ‘rock stars’ of modern finance.

### The Black-Scholes Equation

So let’s take a closer look at the Black-Scholes equation. First, it is important to understand the basic assumptions of the Black-Scholes model, which I’ve taken from the excellent book, “[Options, Futures and Other Derivatives](http://www.amazon.com/Options-Futures-Other-Derivatives-6th/dp/0131499084/ref=sr_1_3?s=books&ie=UTF8&qid=1375158629&sr=1-3&keywords=options+futures+and+other+derivatives)”, by John Hull:

*   The underlying asset price follows a ‘random walk’ in accordance with a process known as Geometric Brownian Motion
*   Shorts sales are permitted
*   No transaction costs are incurred
*   No dividends are paid prior to expiration of the option
*   Security trading is continuous, with no jumps in the underlying asset price
*   The risk-free interest rate, r, is constant

The first assumption leads to a model of stock price behavior that I briefly touched on in my last post in which the underlying asset’s return is assumed to be constant and normally distributed, the asset’s price is lognormally distributed and its volatility is constant. The discrete time version of the lognormal model of stock prices is described by the equation below, which is also the starting point for the derivation of the Black-Scholes differential equation, where delta S is the change in stock price over an instantaneous period of time, t, mu represents the underlying return, sigma its volatility and delta z is a normally distributed random (stochastic) variable:

[![discretetimestockpricemodel](img/7ac4638b6e68058edaea8e3fd0012883.png)](https://mhittesdorf.wordpress.com/wp-content/uploads/2013/07/discretetimestockpricemodel1.jpg)

The next step is to apply [Ito’s Lemma](http://en.wikipedia.org/wiki/It%C5%8D%27s_lemma), which describes how a function, f, of the underlying S and time t is related to changes in S and t.  Then a ‘riskless’ portfolio is formed consisting of a long position in the derivative and a short position in ‘delta’  units of the underlying (I’ll get to what delta means in a moment). This effectively cancels out the randomness of the underlying stochastic process and create an instantaneously riskless position.   The position is riskless only for an instant because the relationship between f, S and t is constantly changing as the market moves.  I won’t go into all the math, which is beyond the scope of this post, but the end result is the Black-Scholes differential equation:

[![bsmdiffequation](img/40983566590a5eea189dc5c44a299fff.png)](https://mhittesdorf.wordpress.com/wp-content/uploads/2013/07/bsmdiffequation.jpg)

Lastly, to solve for the value of a call and put, the appropriate boundary conditions must be used, which should be familiar from my last post as the *payoff* functions for a call and put respectively.

For a call, the boundary condition is:

[![callboundary](img/81235ab043de47f40bbe3ff230ec83fb.png)](https://mhittesdorf.wordpress.com/wp-content/uploads/2013/07/callboundary.jpg)

For a put, the boundary condition is:

[![putboundary](img/9779a3d87b6fbc910b0c4207020a96a4.png)](https://mhittesdorf.wordpress.com/wp-content/uploads/2013/07/putboundary.jpg)

This results in the following equation for the value of a call:

[![callequation](img/1ca95c74e1126bf1ba5ffa9b24158507.png)](https://mhittesdorf.wordpress.com/wp-content/uploads/2013/07/callequation.jpg)and the value of a put:

[![putequation](img/7e487047b9bd9d6829eaf8827adf2645.png)](https://mhittesdorf.wordpress.com/wp-content/uploads/2013/07/putequation.jpg)

where d1 and d2 are defined as follows:

[![d1andd2](img/40c4fb7e4ac6f5f92518defa68da7246.png)](https://mhittesdorf.wordpress.com/wp-content/uploads/2013/07/d1andd2.jpg)

and N is the normal cumulative probability density function. As such, N(x) is the probability that a normally distributed random variable is less than x.

To illustrate how these equations are used in practice to calculate the value of a call and put, I’ve uploaded a spread sheet to my Box account at [https://app.box.com/s/iqekbg6phhf9m23tuzki](https://app.box.com/s/iqekbg6phhf9m23tuzki) .  A screen shot is below:

[![bscalc](img/be2f9b110e31136ef541b898cd7abc3f.png)](https://mhittesdorf.wordpress.com/wp-content/uploads/2013/07/bscalc.png)

Note that N(x) is implemented in LibreOffice (and Excel) as the function *normsdist.* Also you can see that the call and put values agree with those from my previous post.

### The Greeks

So let’s move on to the second part of this post, in which I’ll introduce and show how to calculate the *Greeks*.  In the context of option valuation, the Greeks refer to a standard set of option sensitivity measures.   They are:

*   Delta (df/dS) – the change in the value of an option (f) given a one point change in the price of the underlying (S).  Delta is defined as the first derivative of f with respect to S.
*   Gamma (d2f/d2S) – the change in the delta of an option given a one point change in the price of the  underlying (S).  Gamma is defined as the second derivative of f with respect to S.
*   Theta (df/dt) – the change in the value of an option (f) given a 1 day decrease in the option’s time to maturity (t).  Theta is often referred to as the decay rate of an option. It is defined as the first derivative of f with respect to t.
*   Vega (df/dsigma) – the change in the value of an option (f) given a one point change in the volatility (sigma).  Vega is defined as the first derivative of f with respect to sigma.
*   Rho (df/dr) – the change in the value of an option (f) given a one basis point change in the risk-free rate (r).  Rho is defined as the first derivative of f with respect to r.

In options trading, the Greeks are critical to managing the risk of an options portfolio. For example, vega can be used to measure the PnL impact of a change in market volatility.

Additionally, as most option traders seek to limit their exposure to movements in the underlying, the delta of an option is used as a hedge ratio.  To achieve a delta neutral position, a trader must offset his delta by buying (selling) delta units of the underlying if the trader’s option delta is negative (positive).

Also, by virtue of the fact that delta and gamma are the first and second derivatives of the option valuation function (f) with respect to S, the new value of an option can be estimated by means of a [Taylor series expansion](http://en.wikipedia.org/wiki/Taylor_expansion).  As such, delta and gamma are similar in many respects to duration and convexity in the fixed income domain (see my March 2013 post,  Introducing QuantLib: Duration and Convexity).

So now that we’ve covered all the key background concepts related to the valuation of options with Black-Scholes and the measurement of option price sensitivity,  I’ll show how easy it is to value an option in QuantLib using the [BlackScholesCalculator](http://quantlib.org/reference/class_quant_lib_1_1_black_scholes_calculator.html) class. This class, in keeping with the Black-Scholes assumptions above, takes a constant volatility (sigma) and rate (r) as input along with the underlying’s price (S), the option’s strike (K) and the option’s time to maturity (t).

Unlike the original, classic Black-Scholes model, the QuantLib BlackScholesCalculator also supports an optional dividend yield.   Also, a subtle quirk of the BlackScholesCalculator implementation to watch out for is that the constructor expects sigma to be multiplied by the square root of time.

```
 #include <iostream>
#include <cstdlib>
#define BOOST_AUTO_TEST_MAIN
#include <boost/test/unit_test.hpp>
#include <boost/detail/lightweight_test.hpp>
#include <ql/quantlib.hpp>
#include <boost/format.hpp>

namespace {

using namespace QuantLib;

BOOST_AUTO_TEST_CASE(testBlackScholes) {
Real strike = 110.0;
Real timeToMaturity = .5; //years
Real spot = 100.0;
Rate riskFree = .03;
Rate dividendYield = 0.0;
Volatility sigma = .20;

//QuantLib requires sigma * sqrt(T) rather than just sigma/volatility
Real vol = sigma * std::sqrt(timeToMaturity);

//calculate dividend discount factor assuming continuous compounding (e^-rt)
DiscountFactor growth = std::exp(-dividendYield * timeToMaturity);

//calculate payoff discount factor assuming continuous compounding 
DiscountFactor discount = std::exp(-riskFree * timeToMaturity);

//instantiate payoff function for a call 
boost::shared_ptr<[PlainVanillaPayoff](http://quantlib.org/reference/class_quant_lib_1_1_plain_vanilla_payoff.html)> vanillaCallPayoff = 
    boost::shared_ptr<PlainVanillaPayoff>(new PlainVanillaPayoff(Option::Type::Call, strike));

BlackScholesCalculator bsCalculator(vanillaCallPayoff, spot, growth, vol, discount);
std::cout << boost::format("Value of 110.0 call is %.4f") % bsCalculator.value() << std::endl;
std::cout << boost::format("Delta of 110.0 call is %.4f") % bsCalculator.delta() << std::endl;
std::cout << boost::format("Gamma of 110.0 call is %.4f") % bsCalculator.gamma() << std::endl;
std::cout << boost::format("Vega of 110.0 call is %.4f") % bsCalculator.vega(timeToMaturity)/100 << std::endl;
std::cout << boost::format("Theta of 110.0 call is %.4f") % (bsCalculator.thetaPerDay(timeToMaturity)) << std::endl;

Real changeInSpot = 1.0;
BlackScholesCalculator bsCalculatorSpotUpOneDollar(Option::Type::Call, strike, spot + changeInSpot, growth, vol, discount);
std::cout << boost::format("Value of 110.0 call (spot up $%d) is %.4f") % changeInSpot % bsCalculatorSpotUpOneDollar.value() << std::endl;
std::cout << boost::format("Value of 110.0 call (spot up $%d) estimated from delta is %.4f") % changeInSpot % (bsCalculator.value() + bsCalculator.delta() * changeInSpot) << std::endl;

//use a Taylor series expansion to estimate the new price of a call given delta and gamma
std::cout << boost::format("Value of 110.0 call (spot up $%d) estimated from delta and gamma is %.4f") % changeInSpot % (bsCalculator.value() + (bsCalculator.delta() * changeInSpot) + (.5 * bsCalculator.gamma() * changeInSpot)) << std::endl;

//calculate new price of a call given a one point change in volatility
Real changeInSigma = .01;
BlackScholesCalculator bsCalculatorSigmaUpOnePoint(Option::Type::Call, strike, spot, growth, (sigma + changeInSigma) * std::sqrt(timeToMaturity) , discount);
std::cout << boost::format("Value of 110.0 call (sigma up %.2f) is %.4f") % changeInSigma % bsCalculatorSigmaUpOnePoint.value() << std::endl;

//estimate new price of call given one point change in volatility using vega
std::cout << boost::format("Value of 110.0 call (sigma up %.2f) estimated from vega) is %.4f") % changeInSigma % (bsCalculator.value() + (bsCalculator.vega(timeToMaturity)/100)) << std::endl;
}}
```

When run, the code produces the following output:
 `Value of 110.0 call is 2.6119
Delta of 110.0 call is 0.3095
Gamma of 110.0 call is 0.0249
Vega of 110.0 call is 0.2493
Theta of 110.0 call is -0.0160
Value of 110.0 call (spot up $1) is 2.9340
Value of 110.0 call (spot up $1) estimated from delta is 2.9214
Value of 110.0 call (spot up $1) estimated from delta and gamma is 2.9339
Value of 110.0 call (sigma up 0.01) is 2.8631
Value of 110.0 call (sigma up 0.01 estimated from vega) is 2.8612` 

As you can see, for small changes in the Black-Scholes input parameters, the Greeks can accurately estimate the new price of the option.   For larger changes in parameter values or when needing to consider the combined effect of multiple parameter changes (often called a *scenario*), it is necessary to revalue all of the options in a portfolio. This can be expensive and time consuming depending on the performance of the option pricing code, the number of options and the complexity of the scenario.

At this point, I think we’ve covered all the essentials of computing option values and sensitivities with QuantLib’s BlackScholesCalculator class. I hope you enjoyed my latest ‘Introducing QuantLib’ post. Until next time, have fun with QuantLib!