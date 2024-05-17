<!--yml
category: 未分类
date: 2024-05-18 06:47:29
-->

# All things finance and technology… | Insights, rants and raves from the intersection of high finance and high tech

> 来源：[https://mhittesdorf.wordpress.com#0001-01-01](https://mhittesdorf.wordpress.com#0001-01-01)

Welcome back! In this post, I’ll show how classes from QuantLib’s [Monte Carlo framework](http://quantlib.org/reference/group__mcarlo.html) can be utilized to model the path an asset’s price can take over a period of time, such as that depicted in the one-year Intel (INTC) stock chart below. Why would we want a model of asset prices? There are a number of good reasons. One is that a model of asset price dynamics is essential to the valuation of derivatives, such as equity and index options. Secondly, such a model is a powerful tool for risk management. Simulated asset prices can be used to create a range of what-if scenarios with which to calculate a portfolio’s aggregate market risk exposure as measured by metrics such as Value at Risk (VaR). And thirdly, simulated prices that conform to historical asset return parameters (e.g. annualized mean and standard deviation) can be employed as market data for back-testing trading strategies.

[![intc-stock-chart](img/52fbaac27a2649f3e70ca47edcb13252.png)](https://mhittesdorf.wordpress.com/wp-content/uploads/2013/12/intc-stock-chart.png)

So now that we appreciate the why, let’s look at the how. To start, let’s briefly address the theoretical foundations of asset price dynamics- the s*tochastic process*.  Informally, a stochastic process is a function of one or more time varying parameters where at least one of the parameters is non-deterministic; its values correspond to a sequence of independent random variables drawn from a selected probability distribution.  More precisely, the particular stochastic process that describes the evolution of stock prices is termed Geometric Brownian Motion (GBM).

Geometric Brownian Motion can be formulated as a Stochastic Differential Equation (SDE) of the form:

![](img/68c2d37e8366208dcc744b07dabcb19c.png)

where *S* is the stock price at time *t*, μ (*mu)* represents the constant drift or trend (i.e. annual return) of the process and σ (*sigma) *represents the amount of random variation around the trend (i.e. annualized standard deviation of log returns). Intuitively, *mu* can be viewed as the ‘signal’, while *sigma* is the ‘noise’ of the GBM stochastic process.  What this equation tells us is that the change in a stock’s price over a small discrete time increment (*dt*) is a function of the stock’s return (*mu*) and the stock’s volatility (*sigma*), where the volatility is scaled by the output of a Wiener process (*dWt*).  The Wiener process essentially provides random numbers in accordance with a given (usually Gaussian) probability distribution. For more information on Geometric Brownian Motion,  I encourage you to check out the Wikipedia entry [here](http://en.wikipedia.org/wiki/Geometric_Brownian_motion).

### Normally Distributed Model of Asset Returns

With that brief exposition of the theory of Geometric Brownian Motion behind us, let’s proceed with the QuantLib C++ code.  First, I’ll present code that implements the classical model, in which stock returns are assumed to be normally distributed, even though empirical evidence demonstrates that asset returns are, in fact, ‘fat tailed’.  This means that, in reality, there are more stock market ‘crashes’ and ‘rallies’ than a strictly normal model of stock returns would suggest.  Shortly, I will show how the classical model can be extended to explicitly account for fat-tailed returns.

Here is the QuantLib C++ code to generate a  single stock price path under the assumption of normally distributed asset returns:

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

When executed, this code will produce output similar to the following, though the statistics will vary with each run of the program:
 `Standard deviation of simulated returns (Normal): 0.2105
Price statistics: mean=24.99, min=19.87, max=29.02` 

The resulting simulated stock price data, when charted, will look something like this:

[![intc_gbm](img/7cbc16a2b52119faf7f842d98f8ba3ab.png)](https://mhittesdorf.wordpress.com/wp-content/uploads/2013/12/intc_gbm.png)

A few comments:

The code produces a time series of 255 daily closing prices (one for each trading day in the U.S. equity markets), using QuantLib’s [PathGenerator](http://quantlib.org/reference/class_quant_lib_1_1_path_generator.html) class, which is a C++ template parameterized by a [RandomSequenceGenerator](http://quantlib.org/reference/class_quant_lib_1_1_random_sequence_generator.html). The RandomSequenceGenerator requires a source of randomness, which is provided by way of QuantLib’s [MersenneTwisterUniformRng](http://quantlib.org/reference/class_quant_lib_1_1_mersenne_twister_uniform_rng.html) class. The PathGenerator also requires a StochasticProcess as its first constructor argument to which a (shared) pointer to a [GeometricBrownianMotionProcess](http://quantlib.org/reference/class_quant_lib_1_1_geometric_brownian_motion_process.html) instance is passed. The starting price for the process is the closing price of Intel as of 12/7/2012\. The *mu* parameter is bound to INTC’s annualized return, while the *sigma* parameter is equated to INTC’s annualized historical volatility for the period from 12/7/2012 through 12/7/2013.

The Box-Muller transformation is employed to convert a sequence of uniformly distributed random numbers to a sequence of normally distributed random numbers. You can read more about the Box-Muller transformation [here](http://en.wikipedia.org/wiki/Box_Muller).

QuantLib’s [GeneralStatistics](http://quantlib.org/reference/class_quant_lib_1_1_general_statistics.html) class is applied to collect some process statistics in order to measure how accurately the simulated asset path approximates the INTC time series. By design, the simulated asset path’s annualized return and volatility should resemble the *mu* and *sigma* process parameters, respectively. For some applications, such as back-testing path-dependent trading strategies or evaluating certain risk management scenarios, we might also like the simulated minimum, maximum and mean stock prices to fall within a desired range.

Towards the end of the listing, the data points of the simulated asset price path are written to a file so that they can be charted with gnuplot, an open-source charting package. The gnuplot script is included at the end of the source code listing as a comment.

### Leptokurtic Model of Asset Returns

Now let’s revisit a concept I mentioned earlier regarding the distribution of asset returns. It’s well known that asset returns are ‘fat-tailed’, which is an intuitive way of stating that daily returns are observed in practice to fall more often in the lower and upper tails of their frequency distribution than would be predicted by the normal probability distribution function (pdf).   As such, asset returns can be characterized as *leptokurtic*, meaning that their frequency distribution exhibits *excess* *kurtosis *compared to the normal distribution, which has a kurtosis value of 3.

How can we improve our model of asset prices to incorporate the leptokurtic nature of asset returns that we see in the real-world?  Essentially, we would like the simulated asset price paths to exhibit more days with higher volatility compared to a price path generated in accordance with the classical, normally distributed model of asset returns, while realizing the same annualized volatility as the normal model*.  To achieve this we need to sample our random numbers from a non-normal distribution with excess kurtosis.  One such distribution often used for this purpose is the [Student’s t distribution](http://en.wikipedia.org/wiki/Student%27s_t-distribution), which belongs to a family of stable distributions known as [Cauchy distributions](http://en.wikipedia.org/wiki/Cauchy_distribution), which are symmetrical about the mean but with ‘fat tails’.  The shape of the Student’s t distribution is determined by a single parameter, *v*, which is defined as *degrees of freedom.* The greater the number of degrees of freedom, the more the Student’s t distribution resembles the normal distribution, the smaller the ‘fatter’ the tails.*

 *So let’s make the necessary changes to the code above to generate random numbers distributed in accordance with the Student’s t distribution.  This is accomplished with QuantLib’s [InverseCumulativeRsg](http://quantlib.org/reference/class_quant_lib_1_1_inverse_cumulative_rsg.html) class, which is a template parameterized by a RandomSequenceGenerator and an inverse cumulative distribution function.  The implementation of the Student’s t distribution is provided by the Boost Math library class [boost::math::students_t_distribution](http://www.boost.org/doc/libs/1_35_0/libs/math/doc/sf_and_dist/html/math_toolkit/dist/dist_ref/dists/students_t_dist.html), which is instantiated with five degrees of freedom, so the shape of the distribution  has the desired ‘fat tails’, as illustrated by the light blue density in the image below. Note that there is more mass in the tails of the light blue density than the black, standard normal density.

![](img/89023d10525872fa37096dc42af92066.png)

The revised source code listing is as follows:

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

The test case, when run, will produce output such as the following, though again, the statistics will vary from run to run of the program:
 `Standard deviation of simulated returns (Student-T): 0.2112
Price statistics: mean=24.94, min=19.44, max=30.24` 

As depicted in the chart below, the `testGeometricBrownianMotionStudentT` test case generates a time series that features more relatively large up and down moves than that of the classic, normal model.  However, the realized volatility of the Student’s t time series is not significantly different than the normal:

[![intc_gbm_student](img/ce8a491a5c1edff21c78954d68841f16.png)](https://mhittesdorf.wordpress.com/wp-content/uploads/2013/12/intc_gbm_student.png)

There is much more to the modeling of asset price dynamics than I can present in this brief post, but I hope that I’ve imparted the fundamental concepts and explained how you can accomplish quite a lot with very little effort using QuantLib.

Also, for your convenience, I have now made all of the source code from my Introducing QuantLib series available on GitHub at [https://github.com/mhittesdorf/allthingsfintech](https://github.com/mhittesdorf/allthingsfintech).  I encourage you to download and experiment with the code yourself.

Thanks for reading my blog and, as always, please feel free to leave your comments and questions below.  Have fun with QuantLib!*