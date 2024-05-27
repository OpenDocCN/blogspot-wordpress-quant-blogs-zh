<!--yml

category: 未分类

日期：2024-05-18 06:46:16

-->

# 介绍 QuantLib：计算现值 | 金融和技术一切…

> 来源：[`mhittesdorf.wordpress.com/2013/02/14/introducing-quantlib-calculating-present-value/#0001-01-01`](https://mhittesdorf.wordpress.com/2013/02/14/introducing-quantlib-calculating-present-value/#0001-01-01)

在本系列的[之前的文章](https://mhittesdorf.wordpress.com/2013/02/03/introducing-quantlib-getting-started/)中，我介绍了‘现值’的概念。在这篇文章中，我将介绍使用 QuantLib 的 [CashFlow](http://quantlib.org/reference/class_quant_lib_1_1_cash_flow.html) 和 [CashFlows](http://quantlib.org/reference/class_quant_lib_1_1_cash_flows.html) 类计算现值的一些示例。尽管这当然是一个简化，但可以毫不夸张地说，所有的金融工具定价归结为估计未来现金流或一系列现金流的现值。一个现金流可以是贷款在到期日的偿还，我们在上一篇文章中学习了如何计算。或者未来现金流可能是股息、利息支付、年金支付、期权的结算或债券票息的支付。

所以让我们从我上一篇文章的例子开始 - 一笔带有单一未来现金流的贷款，即以年利率 5%复利发放的 100 美元一年期贷款到期时应付的金额。在贷款期末应付的金额为 105 美元，这是本金和应计利息的总和。假设今天发放贷款，贷款的‘现值’是多少？以下代码计算答案：

#include <ql/quantlib.hpp>

#include <iostream>

#define BOOST_AUTO_TEST_MAIN

#include <boost/test/unit_test.hpp>

BOOST_AUTO_TEST_CASE(测试计算现值)

{

Leg cashFlows;

日期 date = Date::todaysDate();

cashFlows.push_back(boost::shared_ptr<CashFlow>(new SimpleCashFlow(105.0, date + 365)));

利率 = .05;

实际现值 = CashFlows::npv(cashFlows, InterestRate(rate, ActualActual(), Compounded, Annual), true);

std::cout << “现金流的净现值（NPV）为：” << npv << std::endl;

}

此代码的输出是：

`现金流的净现值（NPV）为：100`

测试的第一行实例化了一个 Leg 对象。Leg 在 cashflow.hpp 中定义为：

`typedef std::vector<boost::shared_ptr<CashFlow> > Leg`,

这是一系列现金流。贷款偿还金额被建模为单一现金流，随后添加到 Leg 中。使用静态的 `Cashflows::npv` 函数来计算给定指定利率、日计数约定、简单复利规则和年复利周期的现金流的现值。

在我的下一篇文章中，我们将应用我们所学的现值知识来定价年息票债券。那时再见，感谢您阅读我的博客！

## 关于 Mick Hittesdorf

我是一位多才多艺的技术领导者，对数据分析、数据科学和大数据技术充满热情。我在大型和小型组织中都有工作经验，担任过各种角色。我曾负责管理一个全球数据科学和分析平台，开发了低延迟的、专有的交易系统，管理过软件开发团队，制定了企业架构策略，撰写了白皮书和博客，在行业期刊上发表过文章，并以咨询和技术销售的身份向客户提供了创新的解决方案。我当前的关注领域包括大数据、数据工程、数据科学、R 语言和云计算。
