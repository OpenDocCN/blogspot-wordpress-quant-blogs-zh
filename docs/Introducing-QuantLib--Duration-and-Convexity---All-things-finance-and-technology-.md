<!--yml

分类：未分类

日期：2024-05-18 06:45:12

-->

# 介绍 QuantLib：持续期和凸度 | 金融与科技事事…

> 来源：[`mhittesdorf.wordpress.com/2013/03/12/introduction-to-quantlib-duration-and-convexity/#0001-01-01`](https://mhittesdorf.wordpress.com/2013/03/12/introduction-to-quantlib-duration-and-convexity/#0001-01-01)

在这篇文章中，我将探讨 QuantLib 对评估债券风险的支持。债券的风险与债券价格对利率的小幅变化的变化幅度密切相关，这可以通过计算债券的持续期和凸度以不同程度的精度量化。这些利率敏感性度量是经典固定收益风险管理的基础。了解债券或债券投资组合的持续期和凸度，可以执行对冲以抵消利率环境变化的影响。此外，可以使用一组共同的基准来比较不同收益率、票息率和到期日的债券的风险。

如我们之前所见，债券的价格与债券的利率成反比。当利率上升时，债券的价格下降，反之亦然。然而，这种关系并不是线性的。随着债券收益率的下降，债券的价格以 increasing rate 增加，随着债券收益率的上升，以 decreasing rate 增加，如下图所示：

![interestratesensitivity](https://mhittesdorf.wordpress.com/wp-content/uploads/2013/03/interestratesensitivity.png)

持续期和凸度试图量化价格与收益率关系动态。

**持续期**

让我们更深入地了解持续期的概念。持续期有两种口味：麦考利持续期和修正持续期。计算麦考利持续期的公式，其中 C = 票息，r = 利率，P = 债券价格，F = 债券的面值，n 是期间数是：

**麦考利持续期 = (C1/(1+r) + 2*C2/(1+r)² +… n * (Cn+F)/(1+r)^n)/P**

麦考利持续期可以理解为债券的时间加权平均到期时间。具有更高持续期的债券比具有更低持续期的债券在未来更远的时期支付更多的现金流。另一种说法是，持有具有更低持续期的债券的人比持有具有更高持续期的债券的人更快地得到偿还。

实际上，由于货币的时间价值，具有更高麦考利持续期的债券对利率变化的敏感度高于具有更低麦考利持续期的债券。这归因于现金流折现于更长期间对债券现值的影响大于近期现金流。

修改后的久期与久期密切相关，可以通过久期计算得出。从概念上讲，它等价于图中所示曲线的切线斜率。因此，它是一种一阶敏感度度量，仅适用于债券利率的小幅变化。修改后的久期是根据麦考利久期得出的，公式如下：

**Dmod = – Macaulay_Duration/(1+r)**

另外，由于修改后的久期是切线到债券定价函数的斜率，因此可以通过对债券定价公式求导并除以债券价格来计算修改后的久期：

**Dmod = 1/P * dP/dr**

修改后的久期可以用于计算给定债券利率变化时债券价格的变化，如下所示：

**Change_in_P =  Dmod * Change_in_r, **其中 Dmod 是一个负量，反映了债券价格和收益率之间的反比关系：

**凸度**

如前所述，久期是利率敏感性的线性一阶度量。因此，它高估了利率上升对债券价格的影响，反之亦然，低估了利率下降对价格的影响。为了更准确地量化债券定价与其收益率之间的关系，必须考虑债券定价函数的曲率。这是通过我们的第二个利率敏感度度量——*凸度*来实现的。凸度是利率敏感性的二阶度量。因此，凸度是通过取债券定价函数的二阶导数并除以债券价格来计算的：

**Convexity = 1/P * dP2/dr2**

使用以下公式重新定价债券，该公式结合了久期和凸度，比仅使用（修改后）久期更为精确：

**Change_in_P = P * ( Dmod * Change_in_r + .5 * Convexity * Change_in_r ^ 2)**

为了说明这些久期和凸度公式并提供对 QuantLib 利率敏感度计算的独立验证，我使用了 Maxima，一个开源的计算机辅助代数（CAA）包。Maxima 对符号方程的操纵支持与商业软件产品 Mathematica 和 Maple 相似。在某个时候，我会写一系列关于 Maxima 的文章，但现在，那些对下面要给出的 Maxima 代码的含义感到好奇的人必须依靠 Maxima 的文档：

标准债券定价公式：

bondprice(r,c,t,f):=(‘sum(c*f/(1+r)^i,i,1,t-1) + (c*f+f)/(1+r)^t);

![maximabondprice](https://mhittesdorf.wordpress.com/wp-content/uploads/2013/03/maximabondprice.png)

麦考利久期——债券的时间加权平均到期日：

duration(r,c,t,f):=(‘sum(i*c*f/(1+r)^i,i,1,t-1) + t*(c*f + f)/(1+r)^t)/bondprice(r,c,t,f);

![maximaduration](https://mhittesdorf.wordpress.com/wp-content/uploads/2013/03/maximaduration.png)

-1 乘以 Macaulay 持续期除以（1+r）得到修改后的持续期：

dmod(r,c,t,f,p):=-1* duration(r,c,t,f)/(1+r);

![maximadmod](https://mhittesdorf.wordpress.com/wp-content/uploads/2013/03/maximadmod.png)

对债券定价公式求导，除以债券价格，得到修改后的持续期（另一种推导方法）：

dbondprice:diff(bondprice(r,c,t,f),r);

dmod2(r,c,t,f):=ev(dbondprice,r=r,c=c,t=t,f=f)/bondprice(r,c,t,f);

![maximadmod2](https://mhittesdorf.wordpress.com/wp-content/uploads/2013/03/maximadmod2.png)

dconvexity:diff(bondprice(r,c,t,f),r,2);

convexity(r,c,t,f):=ev(dconvexity,r=r,c=c,t=t,f=f)/bondprice(r,c,t,f);

![maximaconvexity](https://mhittesdorf.wordpress.com/wp-content/uploads/2013/03/maximaconvexity.png)

QuantLib 通过其[BondFunctions](http://quantlib.org/reference/struct_quant_lib_1_1_bond_functions.html)类提供支持，用于计算持续期、凸度以及其他几种利率敏感性的度量。让我们看看如何使用 QuantLib 计算债券的持续期和凸度：

```
#include <cstdlib>
#include <iostream>
#define BOOST_AUTO_TEST_MAIN
#include <boost/test/unit_test.hpp>
#include <boost/detail/lightweight_test.hpp>
#include <ql/quantlib.hpp>
#include <vector>
#include <boost/math/distributions.hpp>
#include <ql/instruments/bonds/fixedratebond.hpp> 
#include <ql/pricingengines/bond/bondfunctions.hpp>
#include <boost/format.hpp>

BOOST_AUTO_TEST_CASE(testCalculateBondDurationAndConvexity) {
Calendar calendar = UnitedStates(UnitedStates::GovernmentBond);
const Natural settlementDays = 3;
Date today = Date::todaysDate();
Date issueDate = today;
Date terminationDate = issueDate + Period(3, Years);
Rate rate = .03;

InterestRate couponRate(.05, ActualActual(ActualActual::Bond), 
Compounded, Annual);
Real faceValue = 100.0;
std::vector<InterestRate> coupons(3, couponRate);
Schedule schedule(issueDate, terminationDate, Period(Annual), 
calendar,
Unadjusted, Unadjusted, DateGeneration::Backward, false);
FixedRateBond fixedRateBond(settlementDays, faceValue, schedule, 
coupons);
boost::shared_ptr<YieldTermStructure> flatForwardRates(
new FlatForward(issueDate,rate, ActualActual(ActualActual::Bond), Compounded, Annual));
Handle<YieldTermStructure> flatTermStructure(flatForwardRates);
boost::shared_ptr<PricingEngine> bondEngine(
new DiscountingBondEngine(flatTermStructure));
fixedRateBond.setPricingEngine(bondEngine);

//calculate bond price
Real price = fixedRateBond.NPV();
std::cout << "Bond price: " << price << std::endl;

//calculate yield to maturity (YTM)/internal rate of return (IRR)
Real ytm = fixedRateBond.yield(ActualActual(ActualActual::Bond), 
Compounded, Annual);
std::cout << "yield to maturity: " << ytm << std::endl;

//calculate Macaulay duration
InterestRate yield(ytm, ActualActual(ActualActual::Bond), 
Compounded, Annual);
Time macDuration = BondFunctions::duration(fixedRateBond, yield, 
Duration::Macaulay, today);
std::cout << "Macaulay duration: " << macDuration << std::endl;

//calculate modified duration
Time modDuration = -1 * BondFunctions::duration(fixedRateBond, yield, 
Duration::Modified, today);
std::cout << "Modified duration: " << modDuration << std::endl;

//calculate convexity
Real convexity = BondFunctions::convexity(fixedRateBond, yield, 
today);
std::cout << "Convexity: " << convexity << std::endl;

//estimate new bond price for an increase in interest rate of 1% 
//using modified duration
Real priceDuration = price + price * (modDuration * .01);
std::cout << boost::format("Estimated bond price using only duration (rate up .01): %.2f ") %
priceDuration << std::endl;

//estimate new bond price for an increase in interest rate of 1% 
//using duration and convexity
Real priceConvexity = price + price * (modDuration * .01 + (.5 * convexity * std::pow(.01, 2)));
std::cout << boost::format("Estimated bond price using duration 
and convexity (rate up .01): %.2f") % priceConvexity << std::endl;

}
```

当运行此代码时，输出结果为：

`Bond price: 105.657

yield to maturity: 0.03

Macaulay duration: 2.8635

修改后的持续期：-2.7801

Convexity: 10.6258

仅使用持续期估算的债券价格（利率上升 0.01）：102.72

使用持续期和凸度估算的债券价格（利率上升 0.01）：102.78`

让我们将持续期和凸度数值与 Maxima 方程式产生的结果进行比较：

![maximaoutput](https://mhittesdorf.wordpress.com/wp-content/uploads/2013/03/maximaoutput.png)

正如预期，Maxima 的计算确实确认了 QuantLib 的持续期和凸度计算，这是件好事！

本文就到此结束。我希望你对于如何使用持续期和凸度来帮助评估债券的风险性以及当利率变化时重新定价债券有了新的认识。下次再见，祝你在 QuantLib 中玩得开心！
