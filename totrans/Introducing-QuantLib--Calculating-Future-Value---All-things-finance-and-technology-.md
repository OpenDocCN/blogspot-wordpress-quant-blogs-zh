<!--yml
category: 未分类
date: 2024-05-18 06:47:07
-->

# Introducing QuantLib: Calculating Future Value | All things finance and technology…

> 来源：[https://mhittesdorf.wordpress.com/2013/02/11/introducing-quantlib-calculating-future-value/#0001-01-01](https://mhittesdorf.wordpress.com/2013/02/11/introducing-quantlib-calculating-future-value/#0001-01-01)

Welcome back. In my last post I showed how to calculate the future value of a loan, that is the amount owed when the loan is due assuming a one year term at a 5% annual rate compounded annually. The code is repeated below:

#include <ql/quantlib.hpp>
#include <iostream>
#define BOOST_AUTO_TEST_MAIN
#include <boost/test/unit_test.hpp>

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

Let’s go through this code and highlight some of the key statements. First and most important is the class that represents the loan, [FixedRateCoupon](http://quantlib.org/reference/class_quant_lib_1_1_fixed_rate_coupon.html "FixedRateCoupon").  The FixedRateCoupon class models a payment where the dollar amount due at the payment date is specified at the inception of the loan.  Our simple loan has one payment, the premium plus the interest, which is owed the lender when the loan is due.  I aliased the FixedRateCoupon class with a typedef to create a Loan abstraction that, hopefully, makes subsequent code more intuitive.

The next several lines just define the loan’s term, premium and interest rate using specialized QuantLib data types, such as [Natural](http://quantlib.org/reference/group__types.html) and [Real](http://quantlib.org/reference/group__types.html).  In the next two lines, today’s date is established and the payment date is calculated with respect to today’s date.

In the following line, an instance of the Loan class is declared, given the loan parameters previously defined. The [ActualActua](http://quantlib.org/reference/class_quant_lib_1_1_actual_actual.html)l() argument is the ‘day count’ convention for the loan. I’ll cover day count conventions in a future post, but suffice it to say that different types of loans are priced using different day count conventions.

Finally, the final payment is calculated by adding the interest due on the loan, obtained with the accruedAmount() method, to the loan principal. As is probably obvious, the argument to accruedAmount() is the date that the loan matures and the loan repayment is due.

I hope that the code makes sense. If you have any questions about anything that I haven’t covered, I encourage you to consult the QuantLib [documentation](http://quantlib.org/reference/annotated.html).

Rather than jump into the calculation of present value and interest rates as I had originally planned, I will instead defer those topics to my next post. Thanks for visiting my blog and feel free to leave a comment or question.

## About Mick Hittesdorf

I'm a versatile technical leader with a passion for data analytics, data science and Big Data technology. I have experience working for both large and small organizations, in a variety of roles. I've been responsible for the management and operations of a global data science and analytics platform, developed low latency, proprietary trading systems, managed software development teams, defined enterprise architecture strategies, written white papers and blogs, published articles in industry journals and delivered innovative solutions to clients, both in a consulting and technical sales capacity. My current areas of focus include Big Data, data engineering, data science, R, and Cloud computing