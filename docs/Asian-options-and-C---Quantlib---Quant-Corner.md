<!--yml

类别：未分类

日期：2024-05-18 08:10:46

-->

# 亚洲期权和 C++/Quantlib | 量化角落

> 来源：[`quantcorner.wordpress.com/2011/02/04/asian-options-and-cquantlib/#0001-01-01`](https://quantcorner.wordpress.com/2011/02/04/asian-options-and-cquantlib/#0001-01-01)

换句话说，**亚洲期权**是一种期权合同，其收益由一定时期内标的资产的平均值确定。正如 P.Wilmott (2006) 和 E.G.Haug (2007)所指出的，亚洲期权在场外能源市场和其他缺乏流动性的大宗商品市场中很受欢迎。实际上，平均意味着降低的价格波动性，更便宜的期权价格，以及市场操纵的可能性更小。

现在，亚洲期权可以根据几个维度进行分类，即:

– 平均执行期权 vs 平均利率期权

– 算术平均值 vs 几何平均值

– 离散 vs 连续平均

– 美式期权 vs 欧式期权

### **等利率/价格期权 vs 平均执行期权**

亚洲期权被分类为**等利率**（**或等价格**）或**平均执行**。有关详细讨论，请参阅 P.Wilmott(2006)，J.C.Hull(2008)和 C.Alexander（2008）。下表显示了可能的收益:

| **收益** | 看涨期权 | 看跌期权 |
| --- | --- | --- |
| 平均执行期权 | max (S-A, 0) | max (A-S, 0) |
| 等利率期权（或等价格期权） | max (A-E, 0) | max (E-S, 0) |

**S** = 标的价格

**E** = 行使(执行)价格

**A** = 平均执行价格

在本文中，我们感兴趣的是平均利率/价格期权。

### **连续 vs 离散/平均**

在**连续情况**下，**连续抽样平均值**被建模为一个**积分**。在**离散情况**下，人们在期权生命周期中平均了有限数量的期权价值。例如，我们可能使用每周的基准价格。

实际上(由于法律和实际问题)，**亚洲期权**通常在**离散时间**监测。而且，我们只考虑基准价格之间的等时间长度。

### **Black-Scholes**世界和亚洲期权

在**离散情况**下，通过所谓的**更新规则**，人们可以得到处理**Black-Scholes**随机微分方程**（SDE）**的亚洲期权价格

在算术情况下，人们必须解决解决标准**Black-Scholes**方程的问题

![](https://quantcorner.wordpress.com/wp-content/uploads/2011/02/normal-black-scholes.jpg)用于 V(S, A, t) 方程

![](https://quantcorner.wordpress.com/wp-content/uploads/2011/02/v-a-t-arithmetic.jpg)但是没有**封闭形式的解**。

在几何情况下，平均值是所有构成价格的对数的指数和，我们通过离散采样价格的和来除以(我们只限于等时间步)。

再次，我们使用普通的**Black Scholes**方程

![](https://quantcorner.wordpress.com/wp-content/uploads/2011/02/normal-black-scholes.jpg)然而，现在跳跃条件变成了：

![](https://quantcorner.wordpress.com/wp-content/uploads/2011/02/v_a_t_geometric1.jpg)

对于**几何平均亚洲期权**，存在**闭合形式解**，因为对数正态随机变量的几何平均保持对数正态性质。而且，这就是我们打算使用**Quantlib**编写的内容。事实上，**Quantlib**配备了一个特殊的期权引擎，用于通过**AnalyticDiscreteGeometricAveragePriceAsianEngine**类解析地计算离散和几何平均的亚洲期权价格。

如果我们愿意，我们可以将我们的解析计算结果与从**蒙特卡罗模拟**中获得的结果进行比较。而且，人们可能希望通过**MCDiscreteArithmeticAPEngine**来定价算术平均期权。

### **C++/Quantlib 代码**

我们现在转向编码

___________________________

期权类型                      :      看跌期权

行权价:                              :      36

底层:                            :      40

期权到期            :      2011 年 12 月 10 日

无风险利率          :      6%

红利收益率                    :      无风险利率 – (0,5 x (波动率²))

时间步长之间

连续固定              :    7 天

前期固定              :    无

波动率                    :    20% ______________________

```
#include<ql\quantlib.hpp>
#include <iostream>

using namespace QuantLib;

#if defined(QL_ENABLE_SESSIONS)
namespace QuantLib {

    Integer sessionId() { return 0; }
}
#endif

int main(int, char* []) {

    try {

		// Calendar set up
		Calendar calendar = TARGET();
		Date todaysDate(5, February, 2011);
		Settings::instance().evaluationDate() = todaysDate;

		// Option parameters
		Option::Type optionType(Option::Put);
		Average::Type averageType = Average::Geometric;
		Real strike = 40;
		Real underlying = 38;
		Rate riskFreeRate = 0.05;
		Volatility volatility = 0.20;
		Spread dividendYield = riskFreeRate-(0.5*volatility*volatility);
		Date maturity (10, December, 2011);
		DayCounter dayCounter = Actual365Fixed();
		Real runningSum = 1.0;
		Size pastFixings = 0;
		std::vector<Date> fixingDates;
		for (Date incrementedDate=todaysDate+7; incrementedDate<=maturity; incrementedDate += 7)
			fixingDates.push_back(incrementedDate);

		// Option exercise type
		boost::shared_ptr<Exercise> europeanExercise(
			new EuropeanExercise(
			maturity));

		// Quote handling
		Handle<Quote> underlyingH(
			boost::shared_ptr<Quote>(
			new SimpleQuote(
			underlying)));

		// Yield term structure handling
		Handle<YieldTermStructure> flatTermStructure(
			boost::shared_ptr<YieldTermStructure>(
			new FlatForward(
			todaysDate,
			riskFreeRate,
			dayCounter)));

		// Dividend term structure handling
		Handle<YieldTermStructure> flatDividendTermStructure(
			boost::shared_ptr<YieldTermStructure>(
			new FlatForward(
			todaysDate,
			dividendYield,
			dayCounter)));

		// Volatility structure handling
		Handle<BlackVolTermStructure> flatVolTermStructure(
			boost::shared_ptr<BlackVolTermStructure>(
			new BlackConstantVol(
			todaysDate,
			calendar,
			volatility,
			dayCounter)));

		// the BS equation behind
		boost::shared_ptr<BlackScholesMertonProcess> bsmProcess(
			new BlackScholesMertonProcess(
			underlyingH,
			flatDividendTermStructure,
			flatTermStructure,
			flatVolTermStructure));

		// Payoff
		boost::shared_ptr<StrikedTypePayoff> payoffAsianOption (
			new PlainVanillaPayoff(
			Option::Type(optionType),
			strike));

		// Discretely-averaged Asian option
		DiscreteAveragingAsianOption discreteAsianAverageOption(
			averageType,
			runningSum,
			pastFixings,
			fixingDates,
			payoffAsianOption,
			europeanExercise);

		// Pricing engine
		discreteAsianAverageOption.setPricingEngine(
		boost::shared_ptr<PricingEngine>(
		new AnalyticDiscreteGeometricAveragePriceAsianEngine(
		bsmProcess)));

		// Ouputting on the screen
		std::cout << "Option type = " << optionType << std::endl;
		std::cout << "Option maturity = " << maturity << std::endl;
		std::cout << "Underlying  = " << underlying << std::endl;
		std::cout << "Strike = " << strike << std::endl;
		std::cout << "Risk-free interest rate = " <<  std::setprecision(2) << io::rate(riskFreeRate) << std::endl;
		std::cout << "Dividend yield = " << std::setprecision(2) << io::rate(dividendYield) << std::endl;
		std::cout << "Volatility = " <<  std::setprecision(2) << io::volatility(volatility) << std::endl;
		std::cout << "Time-length between successive fixings = weekly time step" << std::endl;
		std::cout << "Previous fixings = " << pastFixings << std::endl;
		std::cout << std::endl;
		std::cout << "Option price : " << discreteAsianAverageOption.NPV() << std::endl;

		system("pause");
		return 0;

		} 
		catch (std::exception& e)
		{
		std::cerr << e.what() << std::endl;
		return 1;
		}
		catch (...)
		{
		std::cerr << "unknown error" << std::endl;
		return 1;
		}
}
```
