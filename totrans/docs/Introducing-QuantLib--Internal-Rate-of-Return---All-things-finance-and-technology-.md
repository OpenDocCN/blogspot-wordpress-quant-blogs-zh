<!--yml
category: 未分类
date: 2024-05-18 06:45:20
-->

# Introducing QuantLib: Internal Rate of Return | All things finance and technology…

> 来源：[https://mhittesdorf.wordpress.com/2013/03/03/introducing-quantlib-internal-rate-of-return/#0001-01-01](https://mhittesdorf.wordpress.com/2013/03/03/introducing-quantlib-internal-rate-of-return/#0001-01-01)

Welcome back!  In my previous post, we learned about the term structure of interest rates in the context of bond pricing. Given the term structure, we saw how to calculate the price of a fixed-rate bond by calculating the net present value (NPV) of the bond’s future cash flows,  consisting of its annual coupon payments plus the final premium repayment.  The bond’s price, if you recall, was calculated using a constant interest rate, which, as stated in my previous post, is equivalent to a flat interest rate term structure.

Now, let’s assume that we know the price of a bond or, more generally, the present value of a sequence of future cash flows and we would like to know what interest rate was used to arrive at the NPV. This rate of return is commonly referred to as the investment’s ‘internal rate of return’ (IRR) or, when applied to a bond, the bond’s ‘yield to maturity’ (YTM).

Let’s look at the cash flows from the bond example we’ve been considering thus far. The bond has a face value of 100, pays annual coupons of 5% and has a price (NPV) of 105.66\. The bond’s cash flows, in order are, 5.0, 5.0 and 105.0\. Therefore, to compute the yield to maturity of the bond, we need to solve for the interest rate, r, in the following equation:

**105.66 = 5/(1+r) + 5/(1+r)^2 + 105/(1+r)^3**

It turns out that there is no analytical, algebraic method to determine the value of r.  As such, the equation must be solved numerically, using a solver method.   In the example code that follows, I use the [Bisection](http://quantlib.org/reference/class_quant_lib_1_1_bisection.html) class, one of several solver classes supported by QuantLib to back out the  bond’s yield to maturity.  Other solvers available in QuantLib include: [Brent](http://quantlib.org/reference/class_quant_lib_1_1_bisection.html), [Secant](http://quantlib.org/reference/class_quant_lib_1_1_secant.html), [Ridder](http://quantlib.org/reference/class_quant_lib_1_1_ridder.html), [Newton](http://quantlib.org/reference/class_quant_lib_1_1_ridder.html) and [FalsePosition](http://quantlib.org/reference/class_quant_lib_1_1_false_position.html).  Each one of these solver classes will find the zero, or root, of a function by varying a single input to the function.  The solver will terminate its search when the return value of the function is less than or equal to the *accuracy* parameter, which is defined to be .000001 in the code below.

The function passed to the Bisection solver in this example takes two forms. The first is a *functor* class, which is a class with operator() overridden. The second is a lambda expression, which is a type of [closure](http://en.wikipedia.org/wiki/Closure_(computer_science)) introduced in the latest C++ standard, [C++ 11](http://en.wikipedia.org/wiki/C%2B%2B11).

The code to calculate the bond’s yield to maturity is as follows:

#### #include <cstdlib>
#include <iostream>
#define BOOST_AUTO_TEST_MAIN
#include <boost/test/unit_test.hpp>
#include <boost/detail/lightweight_test.hpp>
#include <ql/quantlib.hpp>
#include <vector>
#include <ql/instruments/bonds/fixedratebond.hpp>

#### namespace {
using namespace QuantLib;class IRRSolver {
public:
explicit IRRSolver(const Leg& cashFlows, Real npv): _cashFlows(cashFlows),_npv(npv){};
Real operator() (const Rate& rate) const {
InterestRate interestRate(rate, ActualActual(ActualActual::Bond), Compounded, Annual);
return CashFlows::npv(_cashFlows, interestRate, false) – _npv;
}
private:
const Real _npv;
const Leg& _cashFlows;
};

#### BOOST_AUTO_TEST_CASE(testCalculateBondYieldToMaturity) {
Calendar calendar = UnitedStates(UnitedStates::GovernmentBond);
const Natural settlementDays = 3;
Date today = Date::todaysDate();
Date issueDate = today;
Date terminationDate = issueDate + Period(3, Years);
Rate rate = .03;

#### InterestRate couponRate(.05, ActualActual(ActualActual::Bond), Compounded, Annual);
Real faceValue = 100.0;
std::vector<Rate> coupons(3, couponRate);
Schedule schedule(issueDate, terminationDate, Period(Annual), calendar,
Unadjusted, Unadjusted, DateGeneration::Backward, false);
FixedRateBond fixedRateBond(settlementDays, faceValue, schedule, coupons);
boost::shared_ptr<YieldTermStructure> flatForwardRates(new FlatForward(issueDate, rate, ActualActual(ActualActual::Bond), Compounded, Annual));
Handle<YieldTermStructure> flatTermStructure(flatForwardRates);
boost::shared_ptr<PricingEngine> bondEngine(new DiscountingBondEngine(flatTermStructure));

#### fixedRateBond.setPricingEngine(bondEngine);
Real npv = fixedRateBond.NPV();
std::cout << “NPV of bond is: ” << npv << std::endl;

#### //solve for yield to maturity using bisection solver
Bisection bisection;
Real accuracy=0.000001, guess=.10;
Real min=.0025, max=.15;

#### //invoke bisection solver with IRRSolver functor
Real irr = bisection.solve(IRRSolver(fixedRateBond.cashflows(), npv),
accuracy, guess, min, max);

#### std::cout << “Bond yield to maturity (IRR) is: ” << irr << std::endl;

#### //invoke bisection solver with C++ 11 lambda expression
irr = bisection.solve([&] (const Rate& rate){ return CashFlows::npv(fixedRateBond.cashflows(), InterestRate(rate, ActualActual(ActualActual::Bond), Compounded, Annual), false) – npv;},
accuracy, guess, min, max);

#### std::cout << “Bond yield to maturity (IRR) is: ” << irr << std::endl;
}
}

The output of this code when run is:
 `NPV of bond is: 105.657
Bond yield to maturity (IRR) is: 0.0300004
Bond yield to maturity (IRR) is: 0.0300004` 

As you can see both IRR solver methods produce the same result, 3%, which is indeed the interest rate of the bond.

I hope you enjoyed this post. Please feel free to leave comments or questions that you might have. In the next installment of this series, I’ll examine how to calculate the sensitivity of a bond’s price to a change in the level of interest rates. Until then, have fun with QuantLib!

## About Mick Hittesdorf

I'm a versatile technical leader with a passion for data analytics, data science and Big Data technology. I have experience working for both large and small organizations, in a variety of roles. I've been responsible for the management and operations of a global data science and analytics platform, developed low latency, proprietary trading systems, managed software development teams, defined enterprise architecture strategies, written white papers and blogs, published articles in industry journals and delivered innovative solutions to clients, both in a consulting and technical sales capacity. My current areas of focus include Big Data, data engineering, data science, R, and Cloud computing