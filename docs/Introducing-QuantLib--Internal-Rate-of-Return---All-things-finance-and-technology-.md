<!--yml

分类: 未分类

日期: 2024-05-18 06:45:20

-->

# 介绍 QuantLib：内部收益率 | 金融和技术方方面面……

> 来源：[`mhittesdorf.wordpress.com/2013/03/03/introducing-quantlib-internal-rate-of-return/#0001-01-01`](https://mhittesdorf.wordpress.com/2013/03/03/introducing-quantlib-internal-rate-of-return/#0001-01-01)

欢迎回来！在我之前的帖子中，我们了解了债券定价背景下的利率期限结构。鉴于期限结构，我们看到了如何通过计算债券未来现金流的净现值（NPV）来计算固定利率债券的价格，包括其年息票支付和最终溢价偿还。如果你还记得，债券的价格是使用一个恒定的利率计算的，正如我之前的帖子中所述，这相当于一个平的利率期限结构。

现在，让我们假设我们知道债券的价格，或者更一般地说，未来现金流的现值，我们想知道用于计算 NPV 的利率是多少。这种回报率通常被称为投资的“内部收益率”（IRR），或者，当应用于债券时，被称为债券的“到期收益率”（YTM）。

让我们来看一下迄今为止我们一直在考虑的债券示例的现金流。该债券的面值为 100，年息票为 5%，现价（NPV）为 105.66。债券的现金流依次是 5.0、5.0 和 105.0。因此，要计算债券的到期收益率，我们需要解出以下方程中的利率 r：

**105.66 = 5/(1+r) + 5/(1+r)² + 105/(1+r)³**

事实证明，没有解析的代数方法可以确定 r 的值。因此，必须使用数值方法数值解方程。在接下来的示例代码中，我使用 [二分法](http://quantlib.org/reference/class_quant_lib_1_1_bisection.html) 类，这是 QuantLib 支持的几种求解器类之一，来反推债券的到期收益率。QuantLib 中可用的其他求解器包括：[布伦特](http://quantlib.org/reference/class_quant_lib_1_1_bisection.html)、[割线](http://quantlib.org/reference/class_quant_lib_1_1_secant.html)、[里德尔](http://quantlib.org/reference/class_quant_lib_1_1_ridder.html)、[牛顿](http://quantlib.org/reference/class_quant_lib_1_1_ridder.html)和[虚位法](http://quantlib.org/reference/class_quant_lib_1_1_false_position.html)。这些求解器类中的每一个都将通过改变函数的单个输入来找到函数的零点或根。当函数的返回值小于或等于*准确性*参数时，求解器将终止其搜索，在下面的代码中，准确度参数被定义为 .000001。

本示例中传递给二分法求解器的函数有两种形式。第一种是*函数对象*类，它是一个重载了 operator()的类。第二种是一个 lambda 表达式，它是[C++ 11](http://en.wikipedia.org/wiki/C%2B%2B11)引入的一种类型，是一种[closure](http://en.wikipedia.org/wiki/Closure_(computer_science))。

计算债券到期收益率的代码如下：

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

std::cout << “债券的现值是：” << npv << std::endl;

#### //使用二分法求解到期收益率的函数

Bisection bisection;

Real accuracy=0.000001, guess=.10;

Real min=.0025, max=.15;

#### //使用 IRRSolver 函数对象调用二分法求解器

Real irr = bisection.solve(IRRSolver(fixedRateBond.cashflows(), npv),

accuracy, guess, min, max);

#### std::cout << “债券到期收益率（IRR）为：” << irr << std::endl;

#### //使用 C++ 11 lambda 表达式调用二分法求解器

irr = bisection.solve([&] (const Rate& rate){ return CashFlows::npv(fixedRateBond.cashflows(), InterestRate(rate, ActualActual(ActualActual::Bond), Compounded, Annual), false) – npv;},

accuracy, guess, min, max);

#### std::cout << “债券到期收益率（IRR）为：” << irr << std::endl;

}

}

运行此代码的输出结果为：

`债券的现值是：105.657`

债券到期收益率（IRR）为：0.0300004

债券到期收益率（IRR）为：`0.0300004`

正如你所见，两种 IRR 求解方法产生了相同的结果，即 3%，这确实是债券的利率。

我希望您喜欢这篇文章。请随时留下您可能有的评论或问题。在本系列的下一部分中，我将探讨如何计算债券价格对利率水平的变化的敏感性。在此之前，祝您在使用 QuantLib 时玩得开心！

## 关于 Mick Hittesdorf

我是一位多才多艺的技术领导者，对数据分析、数据科学和大数据技术充满热情。我在大型和小型组织中都有工作经验，担任过各种角色。我曾负责管理一个全球数据科学和分析平台，开发了低延迟的专有交易系统，管理过软件开发团队，制定了企业架构策略，撰写了白皮书和博客，在行业期刊上发表文章，并以咨询和技术销售的身份向客户交付创新解决方案。我当前的关注领域包括大数据、数据工程、数据科学、R 和云计算。
