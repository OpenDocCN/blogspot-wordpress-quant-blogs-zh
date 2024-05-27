<!--yml

category: 未分类

date: 2024-05-18 06:46:00

-->

# 介绍 QuantLib：隐含波动率 | 所有关于金融和科技的事物…

> 来源：[`mhittesdorf.wordpress.com/2013/08/29/introducing-quantlib-implied-volatility/#0001-01-01`](https://mhittesdorf.wordpress.com/2013/08/29/introducing-quantlib-implied-volatility/#0001-01-01)

欢迎回来！如果你阅读了我的前两篇帖子，你现在对期权理论和定价的基础知识已经非常熟悉了。特别是，我们已经看到波动率（或 sigma）是任何期权估值公式的关键输入。实际上，由于输入变量如执行价格、到期日、利率和标的资产价格在合同中规定或在市场上可观察，因此是众所周知的，波动率是唯一必须导出或估计的输入。假设没有股息，其时间和大小都有些不确定性，那么，期权价值可以被看作是一个未知数的函数。

那么，一个人应如何确定期权的“正确”波动率（sigma）水平呢？一个着手的地方是查看期权的市场价格，并反推出每个虚值看涨期权和看跌期权的 sigma。在这种情况下，sigma 被称为*隐含波动率*，因为它是从市场价格计算出的期权波动率水平。如果按执行价格绘制这些隐含波动率，构成所谓的*波动率微笑*，如下所示：

![volsmile](https://mhittesdorf.wordpress.com/wp-content/uploads/2013/08/volsmile.png)

微笑的形状和水平都清楚地表明了特定标的资产或资产类别的当前市场风险价格。通常，观察到低 delta 期权，“翅膀”期权，的交易隐含波动率高于平值期权。同样，通常观察到虚值看跌期权的 sigma 高于虚值看涨期权，这种现象称为“偏斜”，在上面的图表中表现出来。

知道了每个执行价格的隐含波动率后，我们就可以开始评估期权是否公平定价。某个期权的 sigma 水平相对于通过期权生命周期内的独立[实现波动率](http://en.wikipedia.org/wiki/Realized_variance)估计得出的公平价值来说，是太高还是太低？如果期权的 sigma 相对于公平价值过高，那么你可能想出售它。反之，如果 sigma 太低，那么你可能想购买这个期权。

So let’s look at how to generate the ES volatility smile above with QuantLib. ES is the exchange symbol for the CBOE’s E-Mini futures contract. The market as of 8/26/2013 (at approximately 2:30 Chicago time) for ES options expiring on 9/20/2013 (ESU3) is shown below. The data comes from my Interactive Brokers paper trading account.

![esoptions8262013-1430](https://mhittesdorf.wordpress.com/wp-content/uploads/2013/08/esoptions8262013-1430.png)

下面的 QuantLib C++ 代码列表解决了屏幕截图中 ES 期权价格对应的隐含波动率问题：

```
 #include <cstdlib>
#include <iostream>>
#define BOOST_AUTO_TEST_MAIN
#include <boost/test/unit_test.hpp>
#include <ql/quantlib.hpp>
#include <boost/detail/lightweight_test.hpp>
#include <vector>
#include <boost/function.hpp>
#include <boost/date_time/posix_time/posix_time.hpp>
#include <fstream>
#include <utility>

namespace {

using namespace QuantLib;

class StrikeInfo {

    public:
        typedef std::pair<SimpleQuote,SimpleQuote> BidAsk;
        StrikeInfo(Option::Type optionType, Real strike, const BidAsk& bidAsk) : 
            _payoff(PlainVanillaPayoff(optionType, strike)), _bidAsk(bidAsk),
            _impliedVol(0.0) {}

        //copy constructor
        StrikeInfo(const StrikeInfo& that) 
           : _payoff(new PlainVanillaPayoff(that.getPayoff().optionType(), that.getPayoff().strike())),
            _bidAsk(that.getBidAsk()), _impliedVol(that.getImpliedVol()) {
        }

        //assignment operator - [implements copy-and-swap idiom](http://stackoverflow.com/questions/3279543/what-is-the-copy-and-swap-idiom)
        StrikeInfo& operator=(StrikeInfo that) {
            swap(*this, that);
        }

        //swap
        friend void swap(StrikeInfo& first, StrikeInfo& second) {
            using std::swap;
            first._payoff.swap(second._payoff);
            std::swap(first._impliedVol, second._impliedVol);
            std::swap(first._bidAsk, second._bidAsk);
        }

        const StrikedTypePayoff& getPayoff() const { return *_payoff;}
        const BidAsk& getBidAsk() const { return _bidAsk; }
        const Volatility& getImpliedVol() const { return _impliedVol; }
        void setImpliedVol(Volatility impliedVol) { _impliedVol = impliedVol;}
        Real getStrike() { return _payoff->strike(); }

    private:

        boost::scoped_ptr<StrikedTypePayoff> _payoff;
        Volatility _impliedVol;
        BidAsk _bidAsk;

};

BOOST_AUTO_TEST_CASE(testESFuturesImpliedVolatility) {

    using namespace boost::posix_time;
    using namespace boost::gregorian;

    ActualActual actualActual;
    Settings::instance().evaluationDate() = Date(26, Month::August, 2013);
    Date expiration(20, Month::September, 2013);

    Time timeToMaturity = actualActual.yearFraction(Settings::instance().evaluationDate(), expiration);
    ptime quoteTime(from_iso_string("20130826T143000"));
    time_duration timeOfDayDuration = quoteTime.time_of_day();
    timeToMaturity += (timeOfDayDuration.hours() + timeOfDayDuration.minutes()/60.0)/(24.0 * 365.0);
    std::cout << boost::format("Time to maturity: %.6f") % timeToMaturity << std::endl;
    Real forwardBid = 1656.00; 
    Real forwardAsk = 1656.25;
    Rate riskFree = .00273;  //interpolated LIBOR rate (between EDU3 and EDV3)
    DiscountFactor discount = std::exp(-riskFree * timeToMaturity);

    //calculate implied volatilities for OTM put options

    std::vector<StrikeInfo> putOptions;
    putOptions.push_back(StrikeInfo(Option::Type::Put, std::make_pair(7.75, 8.00), 1600));
    putOptions.push_back(StrikeInfo(Option::Type::Put, std::make_pair(8.50, 9.00), 1605));
    putOptions.push_back(StrikeInfo(Option::Type::Put, std::make_pair(9.25, 9.75), 1610));
    putOptions.push_back(StrikeInfo(Option::Type::Put, std::make_pair(10.25, 10.75), 1615));
    putOptions.push_back(StrikeInfo(Option::Type::Put, std::make_pair(11.25, 11.75), 1620));
    putOptions.push_back(StrikeInfo(Option::Type::Put, std::make_pair(12.50, 12.75), 1625));
    putOptions.push_back(StrikeInfo(Option::Type::Put, std::make_pair(13.75, 14.00), 1630));
    putOptions.push_back(StrikeInfo(Option::Type::Put, std::make_pair(15.00, 15.50), 1635));
    putOptions.push_back(StrikeInfo(Option::Type::Put, std::make_pair(16.50, 17.00), 1640));
    putOptions.push_back(StrikeInfo(Option::Type::Put, std::make_pair(18.00, 18.50), 1645));
    putOptions.push_back(StrikeInfo(Option::Type::Put, std::make_pair(20.00, 20.25), 1650));
    putOptions.push_back(StrikeInfo(Option::Type::Put, std::make_pair(21.75, 22.25), 1655));
    putOptions.push_back(StrikeInfo(Option::Type::Put, std::make_pair(24.00, 24.25), 1660));
    putOptions.push_back(StrikeInfo(Option::Type::Put, std::make_pair(26.25, 26.75), 1665));
    putOptions.push_back(StrikeInfo(Option::Type::Put, std::make_pair(28.75, 29.25), 1670));
    putOptions.push_back(StrikeInfo(Option::Type::Put, std::make_pair(31.25, 32.25), 1675));
    putOptions.push_back(StrikeInfo(Option::Type::Put, std::make_pair(34.25, 35.25), 1680));
    putOptions.push_back(StrikeInfo(Option::Type::Put, std::make_pair(37.25, 38.25), 1685));
    putOptions.push_back(StrikeInfo(Option::Type::Put, std::make_pair(40.75, 41.75), 1690));
    putOptions.push_back(StrikeInfo(Option::Type::Put, std::make_pair(44.25, 45.25), 1695));
    putOptions.push_back(StrikeInfo(Option::Type::Put, std::make_pair(47.50, 49.75), 1700));
    putOptions.push_back(StrikeInfo(Option::Type::Put, std::make_pair(51.50, 53.75), 1705));
    putOptions.push_back(StrikeInfo(Option::Type::Put, std::make_pair(55.75, 58.00), 1710));

   for (StrikeInfo& putOption: putOptions) {
	StrikeInfo::BidAsk bidAsk = putOption.getBidAsk();
	Real price = (bidAsk.first.value() + bidAsk.second.value())/2.0;
	const StrikedTypePayoff& payoff = putOption.getPayoff();
	if (payoff(forwardAsk) > 0) continue; //skip ITM options
        Bisection bisection;
        Real accuracy = 0.000001, guess = .20;
        Real min = .05, max = .40;
        Volatility sigma = bisection.solve(& {
        Real stdDev = sigma * std::sqrt(timeToMaturity);
        BlackCalculator blackCalculator(payoff.optionType(), payoff.strike(), forwardAsk, stdDev, discount);
            	return blackCalculator.value() - price;
        	}, accuracy, guess, min, max);

	putOption.setImpliedVol(sigma);
        std::cout << boost::format("IV of %f put is %f") % putOption.getStrike() % sigma << std::endl;

    }

   //calculate implied volatilities for OTM call options

   std::vector<StrikeInfo> callOptions;
   callOptions.push_back(StrikeInfo(Option::Type::Call, std::make_pair(63.00, 65.25), 1600));
   callOptions.push_back(StrikeInfo(Option::Type::Call, std::make_pair(59.25, 60.25), 1605));
   callOptions.push_back(StrikeInfo(Option::Type::Call, std::make_pair(55.25, 56.25), 1610));
   callOptions.push_back(StrikeInfo(Option::Type::Call, std::make_pair(51.00, 52.00), 1615));
   callOptions.push_back(StrikeInfo(Option::Type::Call, std::make_pair(47.00, 48.00), 1620));
   callOptions.push_back(StrikeInfo(Option::Type::Call, std::make_pair(43.25, 44.25), 1625));
   callOptions.push_back(StrikeInfo(Option::Type::Call, std::make_pair(39.50, 40.50), 1630));
   callOptions.push_back(StrikeInfo(Option::Type::Call, std::make_pair(35.75, 36.75), 1635));
   callOptions.push_back(StrikeInfo(Option::Type::Call, std::make_pair(32.25, 33.25), 1640));
   callOptions.push_back(StrikeInfo(Option::Type::Call, std::make_pair(29.25, 29.75), 1645));
   callOptions.push_back(StrikeInfo(Option::Type::Call, std::make_pair(26.00, 26.25), 1650));
   callOptions.push_back(StrikeInfo(Option::Type::Call, std::make_pair(23.00, 23.50), 1655));
   callOptions.push_back(StrikeInfo(Option::Type::Call, std::make_pair(20.00, 20.50), 1660));
   callOptions.push_back(StrikeInfo(Option::Type::Call, std::make_pair(17.25, 17.75), 1665));
   callOptions.push_back(StrikeInfo(Option::Type::Call, std::make_pair(14.75, 15.25), 1670));
   callOptions.push_back(StrikeInfo(Option::Type::Call, std::make_pair(12.50, 13.00), 1675));
   callOptions.push_back(StrikeInfo(Option::Type::Call, std::make_pair(10.50, 11.00), 1680));
   callOptions.push_back(StrikeInfo(Option::Type::Call, std::make_pair(8.75, 9.25), 1685));
   callOptions.push_back(StrikeInfo(Option::Type::Call, std::make_pair(7.00, 7.50), 1690));
   callOptions.push_back(StrikeInfo(Option::Type::Call, std::make_pair(5.75, 6.00), 1695));
   callOptions.push_back(StrikeInfo(Option::Type::Call, std::make_pair(4.70, 4.80), 1700));
   callOptions.push_back(StrikeInfo(Option::Type::Call, std::make_pair(3.70, 3.85), 1705));
   callOptions.push_back(StrikeInfo(Option::Type::Call, std::make_pair(2.90, 3.05), 1710));

    for (StrikeInfo& callOption: callOptions) {
        StrikeInfo::BidAsk bidAsk = callOption.getBidAsk();
	Real price = (bidAsk.first.value() + bidAsk.second.value())/2.0;
	const StrikedTypePayoff& payoff = callOption.getPayoff();
	if (payoff(forwardBid) > 0) continue; //skip ITM options
        Bisection bisection;
        Real accuracy = 0.000001, guess = .20;
        Real min = .05, max = .40;
        Volatility sigma = bisection.solve(& {
            Real stdDev = sigma * std::sqrt(timeToMaturity);
            BlackCalculator blackCalculator(payoff.optionType(), payoff.strike(), forwardBid, stdDev, discount);
            	return blackCalculator.value() - price;
            }, accuracy, guess, min, max);

	callOption->setImpliedVol(sigma);

        std::cout << boost::format("IV of %f call is %f") % callOption.getStrike() % sigma << std::endl;
    }

    //write strike and IV to file for each option
    std::ofstream ivFile;
    ivFile.open("/tmp/iv.dat", std::ios::out);

    //write OTM put IVs
    for (StrikeInfo& putOption: putOptions) {
	if (putOption.getImpliedVol() > 0.0) {
	    ivFile << boost::format("%f %f") % putOption.getStrike() % putOption.getImpliedVol() << std::endl; 
	}
    }

    //write OTM call IVs		
    for (StrikeInfo& callOption: callOptions) {
	if (callOption.getImpliedVol() > 0.0) {
	    ivFile << boost::format("%f %f") % callOption.getStrike() % callOption.getImpliedVol() << std::endl; 
	}
    }
    ivFile.close();

    //plot with gnuplot using commands below. Run 'gnuplot' then type in: 
    /*
    set terminal png
    set output "/tmp/volsmile.png"
    set key top center
    set key box
    set xlabel "Strike"
    set ylabel "Volatility"
    plot '/tmp/iv.dat' using 1:2 w linespoints title "ES Volatility Smile"
    */
}} 
```

当运行时，代码产生以下输出：

`Time to maturity: 0.070148

IV of 1600.000000 put is 0.1584

IV of 1605.000000 put is 0.1566

IV of 1610.000000 put is 0.1532

IV of 1615.000000 put is 0.1511

IV of 1620.000000 put is 0.1482

IV of 1625.000000 put is 0.1456

IV of 1630.000000 put is 0.1430

IV of 1635.000000 put is 0.1405

IV of 1640.000000 put is 0.1379

IV of 1645.000000 put is 0.1345

IV of 1650.000000 put is 0.1324

IV of 1655.000000 put is 0.1293

IV of 1660.000000 call is 0.1267

IV of 1665.000000 call is 0.1237

IV of 1670.000000 call is 0.1211

IV of 1675.000000 call is 0.1187

IV of 1680.000000 call is 0.1167

IV of 1685.000000 call is 0.1150

IV of 1690.000000 call is 0.1119

IV of 1695.000000 call is 0.1100

IV of 1700.000000 call is 0.1087

IV of 1705.000000 call is 0.1072

IV of 1710.000000 call is 0.1060`

我的输出并没有完全复制 Interactive Brokers 发布的 IV，但它们通常非常接近，并且我的隐含波动率曲线的整体形状与 IB 的值一致。

在我结束这篇文章之前，对代码的一些评论：

+   使用 QuantLib [Bisection](http://quantlib.org/reference/class_quant_lib_1_1_bisection.html) 求解器，类似于我在文章 ‘[Introducing QuantLib: Internal Rate of Return](https://mhitt

+   由于 ES 期权是期货期权，我使用了 QuantLib [BlackCalculator](http://quantlib.org/reference/class_quant_lib_1_1_black_calculator.html)，它实现了 Black-Scholes 模型的 [Black 76](http://www.wilmottwiki.com/wiki/index.php?title=Black_76) 变体，而不是我上一篇文章中介绍的 BlackScholesCalculator。

+   利率为 0.0273% 的利率是对应于期权到期日的 LIBOR 曲线上的点。这个利率是通过在九月和十月欧元美元期货合约（符号 = EDU3, EDV3）之间插值得到的。

+   期权的价值持续衰减，因此到期时间被测量到分钟级别的精度，然后年化为年分数。

+   期权买卖价差的中间点被用作期权价格，因为期权的市场价格通常在其理论值周围有一定宽度。

+   买价作为看涨期权的标的价格，而卖价作为看跌期权的标的价格，因为期权通常是对冲的。因此，看涨期权（正的 delta）将通过在买价上卖出期货进行对冲，而看跌期权将通过在卖价上购买期货进行对冲。

那么，关于我‘介绍 QuantLib’系列的这一部分就到这里了。我希望我现在已经向你提供了一个对隐含波动率以及如何使用 QuantLib 来计算它的基本理解。*一如既往，祝您使用 QuantLib 愉快！*
