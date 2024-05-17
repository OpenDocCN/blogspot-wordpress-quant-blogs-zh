<!--yml
category: 未分类
date: 2024-05-18 06:46:16
-->

# Introducing QuantLib: Calculating Present Value | All things finance and technology…

> 来源：[https://mhittesdorf.wordpress.com/2013/02/14/introducing-quantlib-calculating-present-value/#0001-01-01](https://mhittesdorf.wordpress.com/2013/02/14/introducing-quantlib-calculating-present-value/#0001-01-01)

In a [previous post](https://mhittesdorf.wordpress.com/2013/02/03/introducing-quantlib-getting-started/) in this series, I introduced the concept of ‘present value’. In this post, I will cover some examples of calculating present value using QuantLib’s [CashFlow](http://quantlib.org/reference/class_quant_lib_1_1_cash_flow.html) and [CashFlows](http://quantlib.org/reference/class_quant_lib_1_1_cash_flows.html) classes.  Though certainly a simplification, it is not too much of a stretch to claim that all financial instrument pricing boils down to estimating the present value of a future cash flow or series of cash flows.  A cash flow can be the repayment of a loan on its maturity date,  which we learned how to calculate in my last post.  Or a future cash flow could be a stock dividend, an interest payment, an annuity payment, the payoff from an option or a bond coupon.

So let’s start with the example from my last post – a loan with a single future cash flow, the amount due on a $100 one-year loan with an interest rate of 5% compounded annually.  The amount due at the end of the loan period is $105, which is the sum of the principal and the accrued interest.  What is the ‘present value’ of the loan assuming that the loan was issued today? The code below computes the answer:

#include <ql/quantlib.hpp>

#include <iostream>

#define BOOST_AUTO_TEST_MAIN

#include <boost/test/unit_test.hpp>

BOOST_AUTO_TEST_CASE(testCalculatePresentValue)
{
Leg cashFlows;
Date date = Date::todaysDate();
cashFlows.push_back(boost::shared_ptr<CashFlow>(new SimpleCashFlow(105.0, date + 365)));
Rate rate = .05;
Real npv = CashFlows::npv(cashFlows, InterestRate(rate, ActualActual(), Compounded, Annual), true);
std::cout << “Net Present Value (NPV) of cash flows is: ” << npv << std::endl;
}

The output of this code is:

`Net Present Value (NPV) of cash flows is: 100`

The first line of the test instantiates a Leg object.  Leg is defined in cashflow.hpp as:

`typedef std::vector<boost::shared_ptr<CashFlow> > Leg`,

which is a sequence of cash flows.  The loan repayment amount is modeled as a single cash flow, which is subsquently added to the Leg.  The static `Cashflows::npv` function is used to calculate the present value of the cash flow given the specified interest rate, day count convention, simple compounding rule and annual compounding period.

In my next post, we’ll apply what we’ve learned about present value to price a bond with annual coupons. See you then and thanks for reading my blog!

## About Mick Hittesdorf

I'm a versatile technical leader with a passion for data analytics, data science and Big Data technology. I have experience working for both large and small organizations, in a variety of roles. I've been responsible for the management and operations of a global data science and analytics platform, developed low latency, proprietary trading systems, managed software development teams, defined enterprise architecture strategies, written white papers and blogs, published articles in industry journals and delivered innovative solutions to clients, both in a consulting and technical sales capacity. My current areas of focus include Big Data, data engineering, data science, R, and Cloud computing