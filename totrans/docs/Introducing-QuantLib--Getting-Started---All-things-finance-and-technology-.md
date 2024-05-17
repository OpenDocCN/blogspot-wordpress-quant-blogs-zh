<!--yml
category: 未分类
date: 2024-05-18 06:45:48
-->

# Introducing QuantLib: Getting Started | All things finance and technology…

> 来源：[https://mhittesdorf.wordpress.com/2013/02/03/introducing-quantlib-getting-started/#0001-01-01](https://mhittesdorf.wordpress.com/2013/02/03/introducing-quantlib-getting-started/#0001-01-01)

In my last post, I introduced QuantLib (www.quantlib.org) , an open-source C++ library for quantitative finance. In this post, I’m going to show you how to start using QuantLib in your own programs.  I won’t assume any specialized financial knowledge.  I do expect, however, that you know C++ and are at least familiar with some of the more common Boost C++ library components, such as shared pointers.  Also, I’ve chosen to structure my code examples as Boost unit test cases rather than individual test programs. See the Boost Test Library at [http://www.boost.org](http://www.boost.org) for more information.

So where should we start? Most introductions to finance begin with the ‘time value of money’ so that’s where we will begin as well.  The concept of the ‘time value of money’ alludes to the fact that money is worth more now than it will be in the future.  If a person is to be deprived of the utility of his money now, in the present, the borrower must compensate him until the loan is repaid, in the future.  This leads to several important and closely related concepts, the ‘future value’ of money, the ‘present value’ of money and interest rates.

Taken in the context of what we’ve just learned about the time value of money, the interest rate is the compensation earned by the lender on the amount of money loaned, called the principal.  The principal plus the interest payment due at the maturity of the loan is the future value of the loan. Conversely, subtract the interest on the loan from the loan repayment to arrive at the loan’s present value, which in the case of a loan, is the same as the principal.  In simple mathematical terms where FV = Future Value, PV = Present Value, R = interest rate, and P = principal:

Future Value: FV = P (1 + R)

Present Value: PV = FV/(1+R)

Calculating and manipulating present values, future values and rates of interest turns out to be fundamental to much of the field of finance and financial mathematics.  So let’s see how QuantLib can be applied to these concepts. Take a look at the code below. It shows how to calculate the forward value of a loan, the amount due when the loan matures.

#include <ql/quantlib.hpp>

#include <iostream>

#define BOOST_AUTO_TEST_MAIN

#include <boost/test/unit_test.hpp>

using namespace QuantLib;

BOOST_AUTO_TEST_CASE(testCalculateLoanPayment) {
typedef FixedRateCoupon Loan;
Natural lengthOfLoan = 365;
Real loanAmount = 100.0;
Rate rate = .05;
Date today = Date::todaysDate();
Date paymentDate = today + lengthOfLoan;
Loan loan(paymentDate, loanAmount, rate, ActualActual(), today, paymentDate);
Real payment = loanAmount + loan.accruedAmount(paymentDate);
std::cout << “Payment due in ” << lengthOfLoan << ” days on loan amount of $” <<
loanAmount << ” at annual rate of ” << rate*100 << “% is: $” << payment << std::endl;
}

The output of the program when run is:

`Payment due in 365 days on loan amount of $100 at annual rate of 5% is: $105`

In my next post, I’ll go through this sample code and explain how it works. From there, I’ll show how to calculate present value and discuss QuantLib’s InterestRate class.  Check back soon!

## About Mick Hittesdorf

I'm a versatile technical leader with a passion for data analytics, data science and Big Data technology. I have experience working for both large and small organizations, in a variety of roles. I've been responsible for the management and operations of a global data science and analytics platform, developed low latency, proprietary trading systems, managed software development teams, defined enterprise architecture strategies, written white papers and blogs, published articles in industry journals and delivered innovative solutions to clients, both in a consulting and technical sales capacity. My current areas of focus include Big Data, data engineering, data science, R, and Cloud computing