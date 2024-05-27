<!--yml

类别：未分类

日期：2024 年 05 月 18 日 06 时 47 分 29 秒

-->

# 金融和技术的一切…… | 高金融与高技术交叉点的见解、牢骚和赞美

> 来源：[`mhittesdorf.wordpress.com#0001-01-01`](https://mhittesdorf.wordpress.com#0001-01-01)

欢迎回来！在本文中，我将展示如何利用 QuantLib 的 [Monte Carlo 框架](http://quantlib.org/reference/group__mcarlo.html) 中的类来建模资产价格在一段时间内可能走势，例如下面所示的一年英特尔（INTC）股票图表中的情况。我们为什么需要资产价格模型呢？有很多很好的理由。其中之一是资产价格动态模型对衍生品的估值至关重要，如股票和指数期权。其次，这样的模型是风险管理的强大工具。模拟的资产价格可以用来创建各种假设情景，用以计算投资组合的总体市场风险敞口，例如通过价值-at-风险（VaR）等指标。第三，符合历史资产回报参数（例如年化均值和标准差）的模拟价格可以作为回测交易策略的市场数据。

![intc-stock-chart](https://mhittesdorf.wordpress.com/wp-content/uploads/2013/12/intc-stock-chart.png)

所以现在我们明白了为什么，让我们看看如何。首先，让我们简要地讨论资产价格动态的理论基础 - 随机过程。非正式地说，随机过程是一个或多个时间变化参数的函数，其中至少一个参数是非确定性的；其值对应于从选定概率分布中抽取的一系列独立随机变量。更确切地说，描述股票价格演变的特定随机过程被称为几何布朗运动（GBM）。

几何布朗运动可以被公式化为如下形式的随机微分方程（SDE）：

![](img/68c2d37e8366208dcc744b07dabcb19c.png)

其中 *S* 是时间 *t* 的股票价格，μ（*mu*）代表过程的恒定漂移或趋势（即年度收益），σ（*sigma*）代表趋势周围的随机变化量（即对数收益的年化标准差）。直观地，*mu* 可以被视为‘信号’，而 *sigma* 是 GBM 随机过程的‘噪音’。 这个方程告诉我们的是，在小的离散时间增量（*dt*）内，股票价格的变化是股票回报（*mu*）和股票波动性（*sigma*）的函数，其中波动性由维纳过程（*dWt*）的输出进行缩放。 维纳过程基本上提供与给定（通常是高斯）概率分布相一致的随机数。 有关几何布朗运动的更多信息，我建议您查看维基百科条目 [这里](http://en.wikipedia.org/wiki/Geometric_Brownian_motion)。

### 资产回报的正态分布模型

通过对几何布朗运动理论的简要阐述，让我们继续进行 QuantLib C++ 代码编写。首先，我将介绍实现经典模型的代码，其中假设股票回报服从正态分布，尽管实证证据表明资产回报实际上具有“fat tailed”的性质。这意味着，在现实中，股票市场的“崩盘”和“反弹”比严格的正态股票回报模型所示的要多。很快，我将展示如何扩展经典模型以明确考虑 fat-tailed 回报。

这里是用 QuantLib C++ 代码生成单个股价路径的代码，假设资产回报服从正态分布：

```
 #include <ql/quantlib.hpp>

using namespace QuantLib;

BOOST_AUTO_TEST_CASE(testGeometricBrownianMotion) {

    Real startingPrice = 20.16; //closing price for INTC on 12/7/2012
    Real mu = .2312; //INTC one year historical annual return
    Volatility sigma = 0.2116; //INTC one year historical volatility
    Size timeSteps = 255; //trading days in a year (U.S.)
    Time length = 1; //one year

    //instantiate Geometric Brownian Motion (GBM) stochastic process
    const boost::shared_ptr<StochasticProcess>& gbm =
        boost::shared_ptr<StochasticProcess> (new GeometricBrownianMotionProcess(startingPrice, 
        mu, sigma));

    //generate a sequence of normally distributed random numbers from a
    //uniform distribution using Box-Muller transformation
    BigInteger seed = SeedGenerator::instance().get();
    typedef BoxMullerGaussianRng MersenneBoxMuller;
    MersenneTwisterUniformRng mersenneRng(seed);
    MersenneBoxMuller boxMullerRng(mersenneRng);
    RandomSequenceGenerator<MersenneBoxMuller> gsg(timeSteps, boxMullerRng);

    //generate simulated path of stock price using GBM stochastic process
    PathGenerator<RandomSequenceGenerator<MersenneBoxMuller> > gbmPathGenerator(gbm, length, 
        timeSteps, gsg, false);
    const Path& samplePath = gbmPathGenerator.next().value;

    //calculate simulated sample returns using C++11 lambda expression
    boost::function<Real, (Real, Real)> calcLogReturns = [](Real x, Real y) {return std::log(y/x);};
    std::vector<Real> logReturns;
    Path::iterator samplePathBegin = samplePath.begin();
    Path::iterator samplePathEnd = samplePath.end();
    Path::iterator endMinusOne = std::prev(samplePathEnd);
    Path::iterator beginPlusOne = std::next(samplePathBegin);

    std::transform(samplePathBegin, endMinusOne, beginPlusOne,
         std::back_inserter(logReturns), calcLogReturns);		

    //calculate some general statistics
    GeneralStatistics statistics;

    //returns statistics
    statistics.addSequence(logReturns.begin(), logReturns.end());
    std::cout << boost::format("Standard deviation of simulated returns (Normal): 
         %.4f") % (statistics.standardDeviation() * std::sqrt(255)) << std::endl;

    //price statistics
    statistics.reset();
    statistics.addSequence(samplePath.begin(), samplePath.end());
    std::cout << boost::format("Price statistics: mean=%.2f, min=%.2f, max=%.2f") %
         statistics.mean() % statistics.min() % statistics.max() << std::endl;  

    //write simulated path to a file for charting with gnuplot
    std::ofstream gbmFile;
    gbmFile.open("/tmp/gbm.dat", 
        std::ios::out);
    for (Size i = 0; i < timeSteps; ++i) {
        gbmFile << boost::format("%d %.4f") % i % samplePath.at(i) << std::endl;
    }

    gbmFile.close();

    /* gnuplot script to chart stock price path
    set key bottom center
    set key bottom box
    set xlabel "Time Step (Days)"
    set ylabel "Stock Price"
    plot "/tmp/gbm.dat" using 1:2 w lines t "INTC simulated stock price"
    */
}
} 
```

当执行时，此代码将生成类似于以下内容的输出，尽管每次运行程序时统计数据会有所变化：

`模拟回报的标准差（正态）：0.2105

价格统计：平均=24.99，最小=19.87，最大=29.02`

当绘制时，生成的模拟股价数据将类似于这样：

![intc_gbm](https://mhittesdorf.wordpress.com/wp-content/uploads/2013/12/intc_gbm.png)

一些评论：

该代码使用 QuantLib 的 [PathGenerator](http://quantlib.org/reference/class_quant_lib_1_1_path_generator.html) 类产生了一系列 255 个每日收盘价（美国股票市场每个交易日一个），该类是一个由 [RandomSequenceGenerator](http://quantlib.org/reference/class_quant_lib_1_1_random_sequence_generator.html) 参数化的 C++ 模板。RandomSequenceGenerator 需要一种随机性源，这是通过 QuantLib 的 [MersenneTwisterUniformRng](http://quantlib.org/reference/class_quant_lib_1_1_mersenne_twister_uniform_rng.html) 类提供的。PathGenerator 还需要作为其第一个构造函数参数的随机过程，其中传递了一个指向 [GeometricBrownianMotionProcess](http://quantlib.org/reference/class_quant_lib_1_1_geometric_brownian_motion_process.html) 实例的（共享）指针。该过程的起始价格是截至 2012 年 12 月 7 日 Intel 的收盘价。*mu* 参数绑定到 INTC 的年化回报率，而 *sigma* 参数则等于 INTC 在 2012 年 12 月 7 日至 2013 年 12 月 7 日期间的年化历史波动率。

Box-Muller 转换用于将一系列均匀分布的随机数转换为一系列正态分布的随机数。您可以在[这里](http://en.wikipedia.org/wiki/Box_Muller)了解有关 Box-Muller 转换的更多信息。

QuantLib 的[GeneralStatistics](http://quantlib.org/reference/class_quant_lib_1_1_general_statistics.html)类用于收集一些过程统计信息，以衡量模拟资产路径与 INTC 时间序列的拟合程度。按设计，模拟资产路径的年化收益和波动率应分别类似于*mu*和*sigma*过程参数。对于某些应用，例如回测依赖路径的交易策略或评估某些风险管理场景，我们可能还希望模拟的最小、最大和平均股价落在所需范围内。

在列表的末尾，模拟资产价格路径的数据点被写入文件，以便可以使用 gnuplot，一个开源图表软件包进行图表化。 gnuplot 脚本作为源代码列表的注释包含在末尾。

### 资产收益的**峰态模型**

现在让我们重新审视我之前提到的关于资产收益分布的概念。众所周知，资产收益呈“厚尾”，这是以一种直观的方式陈述的，即实践中观察到的每日收益更多地集中在其频率分布的下尾和上尾，而不是由正态概率分布函数（pdf）预测的。因此，资产收益可以被描述为*峰态*，意味着它们的频率分布相对于正态分布呈现出*过度* *峰度*，而正态分布的峰度值为 3。

我们如何改进资产价格模型以纳入我们在现实世界中看到的资产收益的峰态特性？基本上，我们希望模拟的资产价格路径表现出更多具有较高波动性的日子，与根据经典的、正态分布的资产收益模型生成的价格路径相比，同时实现相同的年化波动率。为了实现这一点，我们需要从具有过度峰度的非正态分布中抽样随机数。用于此目的的一种常用分布是[学生 t 分布](http://en.wikipedia.org/wiki/Student%27s_t-distribution)，它属于称为[柯西分布](http://en.wikipedia.org/wiki/Cauchy_distribution)的稳定分布族，其分布关于均值对称但有“厚尾”。学生 t 分布的形状由一个参数*v*确定，该参数被定义为*自由度*。自由度越大，学生 t 分布越接近正态分布，尾部越“胖”。

*那么，让我们对上面的代码进行必要的更改，以生成符合学生 t 分布的随机数。这是通过 QuantLib 的 [InverseCumulativeRsg](http://quantlib.org/reference/class_quant_lib_1_1_inverse_cumulative_rsg.html) 类来实现的，它是一个由随机序列生成器和反函数累积分布函数参数化的模板。学生 t 分布的实现由 Boost Math 库的 [boost::math::students_t_distribution](http://www.boost.org/doc/libs/1_35_0/libs/math/doc/sf_and_dist/html/math_toolkit/dist/dist_ref/dists/students_t_dist.html) 类提供，它使用五个自由度进行实例化，因此分布的形状具有所需的“厚尾”，如下图中的浅蓝色密度所示。请注意，浅蓝色密度的尾部质量比黑色标准正态密度更多。

![](img/89023d10525872fa37096dc42af92066.png)

修订后的源代码列表如下所示：

```
 #include <ql/quantlib.hpp>
#include <boost/math/distributions/students_t.hpp>

Real studentTInverse(boost::math::students_t_distribution d, const Real& p) {
    return quantile(d,p)
}

using namespace QuantLib;

BOOST_AUTO_TEST_CASE(testGeometricBrownianMotionStudentT) {

    Real startingPrice = 20.16; //closing price for INTC on 12/7/2012
    Real mu = .2312; //INTC one year historical annual return
    Volatility sigma = 0.2116; //INTC one year historical volatility
    Volatility scaledSigma = std::sqrt(sigma * sigma * 3/5); //scaled by reciprocal of Student T variance (v/(v-2))
    Size timeSteps = 255; //trading days in a year (U.S.)
    Time length = 1; //one year

    //instantiate Geometric Brownian Motion (GBM) stochastic process
    const boost::shared_ptr<StochasticProcess>& gbm =
        boost::shared_ptr<StochasticProcess> (new GeometricBrownianMotionProcess(startingPrice, 
        mu, scaledSigma));

    //random sequence generator uses Mersenne Twiseter to generate uniformly distributed
    //pseudo-random numbers
    BigInteger seed = SeedGenerator::instance().get();
    MersenneTwisterUniformRng mersenneRng(seed);
    RandomSequenceGenerator<MersenneTwisterUniformRng> rsg(timeSteps, mersenneRng);

    //instantiate Student T distribution from Boost math library
    boost::math::students_t_distribution<> studentT(5); //5 degrees of freedom - want fat tails!
    boost::function<Real (Real)> icd = boost::bind(studentTInverse, studentT, _1); 

    //sample random numbers from the Student T distribution		
    InverseCumulativeRsg<RandomSequenceGenerator<MersenneTwisterUniformRng>, 
        boost::function<Real (Real)> > invCumRsg(rsg, icd);

    //generates a single path
    PathGenerator<InverseCumulativeRsg<RandomSequenceGenerator<MersenneTwisterUniformRng>, 
        boost::function<Real (Real)> > > gbmPathGenerator(gbm, length, timeSteps, invCumRsg, false);
    const Path& samplePath = gbmPathGenerator.next().value;

    //calculate simulated sample returns using C++11 lambda expression
    boost::function<Real, (Real, Real)> calcLogReturns = [](Real x, Real y) {return std::log(y/x);};
    std::vector<Real> logReturns;
    Path::iterator samplePathBegin = samplePath.begin();
    Path::iterator samplePathEnd = samplePath.end();
    Path::iterator endMinusOne = std::prev(samplePathEnd);
    Path::iterator beginPlusOne = std::next(samplePathBegin);

    std::transform(samplePathBegin, endMinusOne, beginPlusOne,
         std::back_inserter(logReturns), calcLogReturns);		

    //calculate some general statistics
    GeneralStatistics statistics;

    //returns statistics
    statistics.addSequence(logReturns.begin(), logReturns.end());
    std::cout << boost::format("Standard deviation of simulated returns (Student-T): 
         %.4f") % (statistics.standardDeviation() * std::sqrt(255)) << std::endl;

    //price statistics
    statistics.reset();
    statistics.addSequence(samplePath.begin(), samplePath.end());
    std::cout << boost::format("Price statistics: mean=%.2f, min=%.2f, max=%.2f") %
         statistics.mean() % statistics.min() % statistics.max() << std::endl;  

    //write simulated path to a file for charting with gnuplot
    std::ofstream gbmFile;
    gbmFile.open("/tmp/gbm-student.dat", 
        std::ios::out);
    for (Size i = 0; i < timeSteps; ++i) {
        gbmFile << boost::format("%d %.4f") % i % samplePath.at(i) << std::endl;
    }

    gbmFile.close();

    /* gnuplot script to chart stock price path
   set key bottom center
   set key bottom box
   set xlabel "Time Step (Days)"
   set ylabel "Stock Price"
   plot "/tmp/gbm.dat" using 1:2 w lines 
   t "INTC Normal", "/tmp/gbm-student.dat" using 1:2 w lines t "INTC Student-T"
   */
}
} 
```

当运行测试用例时，将生成如下输出，尽管程序的运行结果会因每次运行而异：

`模拟收益（学生 t 分布）的标准差：0.2112

价格统计数据：均值=24.94，最小值=19.44，最大值=30.24`

如下图所示，`testGeometricBrownianMotionStudentT` 测试用例生成了一个时间序列，其中相对较大的上下波动比经典的正态模型要多。然而，学生 t 时间序列的实现波动性与正态分布并没有显著不同：

![intc_gbm_student](https://mhittesdorf.wordpress.com/wp-content/uploads/2013/12/intc_gbm_student.png)

资产价格动态建模远比我在这篇简短的文章中所能呈现的要复杂得多，但我希望我已经传达了基本概念，并解释了如何使用 QuantLib 用很少的努力就可以取得相当大的成就。

此外，为了您的方便，我现在已经将我的 Introducing QuantLib 系列的所有源代码都上传到 GitHub 上，网址为 [`github.com/mhittesdorf/allthingsfintech`](https://github.com/mhittesdorf/allthingsfintech)。我鼓励您下载并自行尝试代码。

感谢您阅读我的博客，并且，如常，欢迎在下方留下您的评论和问题。享受 QuantLib 的乐趣！*
