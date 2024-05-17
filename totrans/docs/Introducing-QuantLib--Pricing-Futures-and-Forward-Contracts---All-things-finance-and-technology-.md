<!--yml
category: 未分类
date: 2024-05-18 06:46:55
-->

# Introducing QuantLib: Pricing Futures and Forward Contracts | All things finance and technology…

> 来源：[https://mhittesdorf.wordpress.com/2013/04/02/introduction-to-quantlib-pricing-futures-and-forward-contracts/#0001-01-01](https://mhittesdorf.wordpress.com/2013/04/02/introduction-to-quantlib-pricing-futures-and-forward-contracts/#0001-01-01)

In this installment of my series on QuantLib, I’m going to show how to price a forward contract on a fixed rate bond. A forward contract obligates the buyer to purchase an underlying asset at a specified future point in time at a specified strike price from the seller of the forward contract, who is likewise obligated to deliver the underlying asset at the agreed strike price. At the inception of the contract, the strike price is established as the expected future value of the underlying asset, which we learned how to calculate in an earlier post in this series.

A futures contract is a standardized, exchange-traded forward contract with daily mark-to-market.  For the purposes of this post, we will assume that futures and forward prices are equivalent. For the subtleties that can cause futures and forward price to diverge in the real world, I recommend that you read Chapter 5 of John Hull’s classic book, “Options, futures and Other Derivatives, 6th Edition”.

To calculate the (strike) price of a forward contract on a fixed-rate bond, which is an asset with a known, fixed income consisting of regular coupon payments, the following formula is used, where K = the forward price at issuance, S0 = the underlying asset’s price at issuance, I = the present value of any income received during the life of the forward contract, r = the interest rate and T is the tenor of the contract:

K = (S0 – I)e^rT

As time progresses and/or interest rates move subsequent to the issuance of the forward contract, the value of the forward contract changes. To reprice the contract, the following formula is used, with all the variables as defined previously:

F = S0 – I – Ke^-rT

The QuantLib code to price a 15 month forward contract on a 3% fixed rate bond with a face value of 100 and 5% coupons paid annually is shown below.  The code also demonstrates how to re-value the forward given both a 1% up and down shift in the level of interest rates. Take note of the `[RelinkableHandle<YieldTermStructure>](http://quantlib.org/reference/class_quant_lib_1_1_relinkable_handle.html)` , which is a powerful QuantLib programming construct that enables a new, updated yield curve to be ‘re-linked’ to the existing forward contract, which causes the forward contract to reprice itself at the higher or lower interest rate when the `FixedRateBondForward::NPV()` method is called.

```
#include <iostream>
#include <cstdlib>
#define BOOST_AUTO_TEST_MAIN
#include <boost/test/unit_test.hpp>
#include <boost/detail/lightweight_test.hpp>
#include <ql/quantlib.hpp>
#include <boost/math/distributions.hpp>
#include <vector>
#include <boost/function.hpp>
#include <boost/math/distributions.hpp>
#include <ql/instruments/bonds/fixedratebond.hpp> 
#include <ql/pricingengines/bond/bondfunctions.hpp>
#include <boost/format.hpp>
#include <ql/instruments/fixedratebondforward.hpp>
#include <ql/termstructures/yield/discountcurve.hpp>

using namespace QuantLib;

BOOST_AUTO_TEST_CASE(testCalculateForwardPriceOfFixedRateBond) {

Calendar calendar = UnitedStates(UnitedStates::GovernmentBond);
const Natural settlementDays = 1;
Date today = Date::todaysDate();
Date bondIssueDate = calendar.adjust(today, ModifiedFollowing);
Date bondMaturityDate = bondIssueDate + Period(3, Years);
Rate rate = .03;
Settings::instance().evaluationDate() = bondIssueDate;

//coupon schedule
std::vector coupons(1, .05);

//fixed rate bond
Real faceValue = 100.0;
boost::shared_ptr<FixedRateBond> fixedRateBondPtr(new FixedRateBond(settlementDays, calendar, 
faceValue, bondIssueDate, bondMaturityDate, Period(Annual), coupons, ActualActual(ActualActual::Bond)));
boost::shared_ptr<YieldTermStructure> flatForwardRates(new FlatForward(bondIssueDate,
rate, ActualActual(ActualActual::Bond), Compounded, Annual));
RelinkableHandle<YieldTermStructure> flatTermStructure(flatForwardRates);
boost::shared_ptr<PricingEngine> bondEngine(new DiscountingBondEngine(flatTermStructure));
fixedRateBondPtr->setPricingEngine(bondEngine);

//calculate bond price
Real bondPrice = fixedRateBondPtr->NPV();
std::cout << "Bond price: " << bondPrice << std::endl;

//print cash flows using C++ 11 range-based for loop
for (boost::shared_ptr<CashFlow> cashFlow : fixedRateBondPtr->cashflows()) {
     std::cout << boost::format("Cash flow: %s, %.2f") % cashFlow->date() % cashFlow->amount() << std::endl; 
}

//forward maturity tenor 
Date forwardMaturityDate = bondIssueDate + Period(15, Months); 
Natural daysToMaturityOfForwardContract = (forwardMaturityDate - bondIssueDate) - settlementDays;
std::cout << boost::format("Expiration of forward contract: %s") % forwardMaturityDate << std::endl;
std::cout << boost::format("Days to maturity of forward contract: %i") % daysToMaturityOfForwardContract << std::endl; 

//calculate strike price/future value of the bond using periodic, annual rate (not continuous) because this a bond		
Real income = (fixedRateBondPtr->nextCouponRate(bondIssueDate) * faceValue);
const Real strike = bondPrice * (1 + rate * daysToMaturityOfForwardContract/365) - income;  
std::cout << boost::format("Strike price of forward contract is: %.2f") % strike << std::endl;

//forward contract on a fixed rate bond
FixedRateBondForward fixedRateBondForward(bondIssueDate, forwardMaturityDate, Position::Type::Long, strike, settlementDays,
ActualActual(ActualActual::Bond), calendar, ModifiedFollowing, fixedRateBondPtr, flatTermStructure, flatTermStructure);

//calculate forward price of bond 
Real forwardPrice = fixedRateBondForward.NPV();
std::cout << boost::format("Bond forward contract value: %.2f") % forwardPrice << std::endl;

//evaluate forward contract by shocking interest rates +/- 1%
boost::shared_ptr<YieldTermStructure> flatForwardRatesUpOnePercent(new FlatForward(bondIssueDate,
rate + .01, ActualActual(ActualActual::Bond), Compounded, Annual));

flatTermStructure.linkTo(flatForwardRatesUpOnePercent);

//recalculate forward price of bond 
std::cout << boost::format("Bond forward contract value (rates up 1 percent): %.2f") % fixedRateBondForward.NPV() << std::endl;

boost::shared_ptr<YieldTermStructure> flatForwardRatesDownOnePercent(new FlatForward(bondIssueDate,
rate - .01, ActualActual(ActualActual::Bond), Compounded, Annual));

flatTermStructure.linkTo(flatForwardRatesDownOnePercent);

//recalculate forward price of bond 
std::cout << boost::format("Bond forward contract value (rates down 1 percent): %.2f") % fixedRateBondForward.NPV() << std::endl;

}
```

The output of this code when run is:

`Bond price: 105.657
Cash flow: April 2nd, 2014, 5.00
Cash flow: April 2nd, 2015, 5.00
Cash flow: April 4th, 2016, 5.00
Cash flow: April 4th, 2016, 100.00
Expiration of forward contract: July 2nd, 2014
Days to maturity of forward contract: 455
Strike price of forward contract is: 104.61
Bond forward contract value: -0.00
Bond forward contract value (rates up 1 percent): -1.63
Bond forward contract value (rates down 1 percent): 1.70` 

As expected, the value of the forward contract is zero, when first issued. The value of the forward contract falls when interest rates go up/the bond price goes down and vice versa when interest rates decline/the bond’s price rises.

I hope you enjoyed this latest post explaining how to value forward and futures contracts with QuantLib. Check back soon and, as always, please feel free to leave comments and questions. Have fun with QuantLib!

## About Mick Hittesdorf

I'm a versatile technical leader with a passion for data analytics, data science and Big Data technology. I have experience working for both large and small organizations, in a variety of roles. I've been responsible for the management and operations of a global data science and analytics platform, developed low latency, proprietary trading systems, managed software development teams, defined enterprise architecture strategies, written white papers and blogs, published articles in industry journals and delivered innovative solutions to clients, both in a consulting and technical sales capacity. My current areas of focus include Big Data, data engineering, data science, R, and Cloud computing