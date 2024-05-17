<!--yml
category: 未分类
date: 2024-05-18 06:46:31
-->

# Introducing QuantLib: Portfolio Optimization | All things finance and technology…

> 来源：[https://mhittesdorf.wordpress.com/2013/06/20/introducing-quantlib-portfolio-optimization/#0001-01-01](https://mhittesdorf.wordpress.com/2013/06/20/introducing-quantlib-portfolio-optimization/#0001-01-01)

Welcome back. If you read my last two posts, you may recall that I showed how to use QuantLib to do linear optimization in the context of a bond portfolio construction problem and mean-variance portfolio analysis by way of the concept of the Efficient Frontier, respectively.  In this installment of my ‘Introducing QuantLib’ series, I will combine elements of each of these two posts in order to demonstrate how QuantLib can be used to generate the Efficient Frontier in the presence of constraints on a portfolio’s composition. Specifically, short sales will not be allowed.   Finding the Efficient Frontier with no short sales will require the repeated solution of a non-linear portfolio optimization problem in which every asset in the portfolio must have a non-negative weighting.

As in previous posts, I will first model the problem in a spreadsheet and then replicate the solution in C++ using classes from the QuantLib library.  The essentials of the model are borrowed from Chapter 11 of Simon Benninga’s excellent book *[Financial Modeling, 2nd Edition](http://www.amazon.com/Financial-Modeling-2nd-Simon-Benninga/dp/0262024829/ref=sr_1_1?s=books&ie=UTF8&qid=1371528897&sr=1-1&keywords=financial+modeling+2nd+edition).* Specifically*,* the weightings on each of four assets, AAPL, IBM, ORCL, GOOG, must be determined such that [Sharpe Ratio](http://en.wikipedia.org/wiki/Sharpe_ratio) of the portfolio is maximized subject to the following constraints:

*   The portfolio’s asset weightings must sum to 1
*   Every asset weighting in the portfolio must be greater than or equal to zero

A screen shot of the full spreadsheet is below, which can be downloaded from my Box account at [https://www.box.com/s/7w4tvfqueqqu676vhz5l](https://www.box.com/s/7w4tvfqueqqu676vhz5l)

As stated in my earlier post on linear optimization, all optimization problems feature a function that must be either maximized or minimized.  This function is called the objective function. In this portfolio optimization problem, *Theta* is the value of the objective function that is to maximized.  It is defined as the ratio of excess return to portfolio standard deviation, where excess return is the portfolio return over and above the risk-free rate, defined as the constant, c, in the spreadsheet.  Theta, is then essentially, the same thing as the portfolio’s Sharpe Ratio for a given value of c.  More intuitively, Theta is a measure of reward for a given amount of risk.  In maximizing Theta, we seek to allocate our capital amongst the four stocks in the portfolio such that we accrue the greatest reward for the least amount of risk.  This goal is consistent with the fact that most investors are risk-averse.

[![efnscalc](img/8ad59a4efefdb5bbb5da278323465159.png)](https://mhittesdorf.wordpress.com/wp-content/uploads/2013/06/efnscalc.png)

On a side note, you may have noticed that this spreadsheet was created using OpenOffice, not LibreOffice, which I employed in previous posts.  I had to switch to OpenOffice in order to install the ‘[Solver for Nonlinear Programming](http://extensions.openoffice.org/en/project/NLPSolver)‘ OpenOffice extension, which is currently not supported by LibreOffice on my laptop’s operating system, Ubuntu 12.04.  Without the non-linear solver extension, LibreOffice detects that the problem is non-linear and fails to find a solution:

[![notlinear](img/2eb89004a93adaae7232e3b230c64e82.png)](https://mhittesdorf.wordpress.com/wp-content/uploads/2013/06/notlinear.png)

Now let’s see how to set up and solve this problem in QuantLib. The C++ code is below:

```
 #include <iostream> 
#include <cstdlib>
#define BOOST_AUTO_TEST_MAIN
#include <boost/test/unit_test.hpp>
#include <boost/detail/lightweight_test.hpp>
#include <ql/quantlib.hpp>
#include <boost/format.hpp>
#include <functional>
#include <numeric>
#include <fstream>

namespace {

using namespace QuantLib;

//aggregates all constraint expressions into a single constraint
class PortfolioAllocationConstraints : public Constraint {

public:

PortfolioAllocationConstraints(const std::vector& expressions)  : Constraint(boost::shared_ptr(new
    PortfolioAllocationConstraints::Impl(expressions))) {}

private:
// constraint implementation
class Impl : public Constraint::Impl {
public:

Impl(const std::vector& expressions) :
    expressions_(expressions) {}

bool test(const Array& x) const {
    for (auto iter = expressions_.begin(); 
    iter < expressions_.end(); ++iter) {
        if (!(*iter)(x)) {
            return false;
        }
    }
    //will only get here if all constraints satisfied
    return true;
}

private:

const std::vector expressions_;        
};
}; 

class ThetaCostFunction: public CostFunction {

    public:
	ThetaCostFunction(const Matrix& covarianceMatrix, 
	    const Matrix& returnMatrix) : covarianceMatrix_(covarianceMatrix),
	    returnMatrix_(returnMatrix) {
	}

    	Real value(const Array& proportions) const {
    	    QL_REQUIRE(proportions.size()==3, "Four assets in portfolio!");
            Array allProportions(4);
            allProportions[0] = proportions[0];
            allProportions[1] = proportions[1];
            allProportions[2] = proportions[2];
            allProportions[3] = 1 - (proportions[0] + proportions[1] + proportions[2]);
	    return -1 * ((portfolioMean(allProportions) - c_)/portfolioStdDeviation(allProportions));	
       	}

	Disposable values(const Array& proportions) const {
            QL_REQUIRE(proportions.size()==3, "Four assets in portfolio!");
            Array values(1);
            values[0] = value(proportions);
            return values;
       	}

       	void setC(Real c) { c_ = c; }
       	Real getC() const { return c_;}
        Real portfolioMean(const Array& proportions) const {
	    Real portfolioMean = (proportions * returnMatrix_)[0];
            //std::cout << boost::format("Portfolio mean: %.4f") % portfolioMean << std::endl;
            return portfolioMean;
	}

	Real portfolioStdDeviation(const Array& proportions) const {
            Matrix matrixProportions(4,1);
	    for (size_t row = 0; row < 4; ++row) {
	        matrixProportions[row][0] = proportions[row];
	    }

	    const Matrix& portfolioVarianceMatrix = transpose(matrixProportions) * covarianceMatrix_ * matrixProportions;
	    Real portfolioVariance = portfolioVarianceMatrix[0][0];
	    Real stdDeviation = std::sqrt(portfolioVariance);
            //std::cout << boost::format("Portfolio standard deviation: %.4f") % stdDeviation << std::endl;
            return stdDeviation;
	}

	private:	
        const Matrix& covarianceMatrix_;
	const Matrix& returnMatrix_;
	Real c_;
    };

    BOOST_AUTO_TEST_CASE(testNoShortSales) {

        Matrix covarianceMatrix(4,4);

        //row 1
        covarianceMatrix[0][0] = .1; //AAPL-AAPL
        covarianceMatrix[0][1] = .03; //AAPL-IBM
        covarianceMatrix[0][2] = -.08; //AAPL-ORCL
        covarianceMatrix[0][3] = .05; //AAPL-GOOG
        //row 2
        covarianceMatrix[1][0] = .03; //IBM-AAPL
        covarianceMatrix[1][1] = .20; //IBM-IBM 
        covarianceMatrix[1][2] = .02; //IBM-ORCL
        covarianceMatrix[1][3] = .03; //IBM-GOOG
	//row 3
        covarianceMatrix[2][0] = -.08; //ORCL-AAPL 
        covarianceMatrix[2][1] = .02; //ORCL-IBM
        covarianceMatrix[2][2] = .30; //ORCL-ORCL
        covarianceMatrix[2][3] = .2; //ORCL-GOOG
       	//row 4
        covarianceMatrix[3][0] = .05; //GOOG-AAPL
        covarianceMatrix[3][1] = .03; //GOOG-IBM
        covarianceMatrix[3][2] = .2; //GOOG-ORCL
        covarianceMatrix[3][3] = .9; //GOOG-GOOG

        std::cout << "Covariance matrix of returns: " << std::endl;
        std::cout << covarianceMatrix << std::endl;

       	//portfolio return vector         
	Matrix portfolioReturnVector(4,1);
        portfolioReturnVector[0][0] = .08; //AAPL
        portfolioReturnVector[1][0] = .09; //IBM
        portfolioReturnVector[2][0] = .10; //ORCL
        portfolioReturnVector[3][0] = .11; //GOOG

        std::cout << "Portfolio return vector" << std::endl;
        std::cout << portfolioReturnVector << std::endl;

        //constraints
	std::vector<std::function >  noShortSalesConstraints(2);

        //constraints implemented as C++ 11 lambda expressions
        noShortSalesConstraints[0] = [] (const Array& x) {Real x4 = 1.0 - ( x[0] + x[1] + x[2]);  return (x[0] >= 0.0 && x[1] >= 0.0 && x[2] >= 0.0 && x4 >= 0.0);}; 
        noShortSalesConstraints[1] = [] (const Array& x) { Real x4 = 1.0 - ( x[0] + x[1] + x[2]); return 1.0 - (x[0] + x[1] + x[2] + x4) < 1e-9;};

	//instantiate constraints
	PortfolioAllocationConstraints noShortSalesPortfolioConstraints(noShortSalesConstraints);

	Size maxIterations = 100000;
	Size minStatIterations = 100;
	Real rootEpsilon = 1e-9;
	Real functionEpsilon = 1e-9;
	Real gradientNormEpsilon = 1e-9;
	EndCriteria endCriteria (maxIterations, minStatIterations, 
		rootEpsilon, functionEpsilon, gradientNormEpsilon);	

        std::map<Rate, std::pair > mapOfStdDeviationToMeanNoShortSales;

	Rate startingC = -.035;
	Real increment = .005;

        for (int i = 0; i < 40; ++i) {
            Rate c = startingC + (i * increment);  
            ThetaCostFunction thetaCostFunction(covarianceMatrix, portfolioReturnVector);
	    thetaCostFunction.setC(c);
            Problem efficientFrontierNoShortSalesProblem(thetaCostFunction, noShortSalesPortfolioConstraints, Array(3, .2500));
	    Simplex solver(.01);
            EndCriteria::Type noShortSalesSolution = solver.minimize(efficientFrontierNoShortSalesProblem, endCriteria);
            std::cout << boost::format("Solution type: %s") % noShortSalesSolution << std::endl;

    	    const Array& results = efficientFrontierNoShortSalesProblem.currentValue();
            Array proportions(4);
            proportions[0] = results[0];
            proportions[1] = results[1];
            proportions[2] = results[2];
            proportions[3] = 1.0 - (results[0] + results[1] + results[2]);
            std::cout << boost::format("Constant (c): %.4f") % thetaCostFunction.getC() << std::endl;
	    std::cout << boost::format("AAPL weighting: %.4f") % proportions[0] << std::endl;  
	    std::cout << boost::format("IBM weighting: %.4f") % proportions[1] << std::endl;  
	    std::cout << boost::format("ORCL weighting: %.4f") % proportions[2] << std::endl;  
	    std::cout << boost::format("GOOG weighting: %.4f") % proportions[3] << std::endl;
	    std::cout << boost::format("Theta: %.4f") % (-1 * efficientFrontierNoShortSalesProblem.functionValue()) << std::endl;
            Real portfolioMean = thetaCostFunction.portfolioMean(proportions); 
            std::cout << boost::format("Portfolio mean: %.4f") % portfolioMean << std::endl;
            Volatility portfolioStdDeviation = thetaCostFunction.portfolioStdDeviation(proportions); 
            std::cout << boost::format("Portfolio standard deviation: %.4f") % portfolioStdDeviation << std::endl;
            mapOfStdDeviationToMeanNoShortSales[c] = std::make_pair(portfolioStdDeviation, portfolioMean); 
            std::cout << "------------------------------------" << std::endl;
        }

        //write efficient frontier with no short sales to file
	std::ofstream noShortSalesFile;
	noShortSalesFile.open("/tmp/noshortsales.dat", std::ios::out);
	for (std::map<Rate, std::pair >::const_iterator i=mapOfStdDeviationToMeanNoShortSales.begin(); i != mapOfStdDeviationToMeanNoShortSales.end(); ++i) {
	    noShortSalesFile <first % i->second.first % i->second.second << std::endl;
	}
	noShortSalesFile.close();

	//plot with gnuplot using commands below Run 'gnuplot' then type in: 
	/*
         set terminal png
         set output "/tmp/noshortsales.png"
         set key top left
	 set key box
	 set xlabel "Volatility"
	 set ylabel "Expected Return"
	 plot '/tmp/noshortsales.dat' using 2:3 w linespoints title "No Short Sales"
	*/
    }
} 
```

When run this code solves for the optimal weightings for all values of c between -.035 and .16.  For example, the ouput for c = .05 is:

 `————————————
Solution type: StationaryPoint
Constant (c): 0.0500
AAPL weighting: 0.5659
IBM weighting: 0.1047
ORCL weighting: 0.3294
GOOG weighting: 0.0000
Theta: 0.1839
Portfolio mean: 0.0876
Portfolio standard deviation: 0.2046
————————————

This solution is in very close agreement with the solution arrived at by the OpenOffice spreadsheet with the non-linear solver extension.  So, it looks like the QuantLib code is doing the right thing. Cool!

Towards the end of code listing, I provide the [gnuplot](http://www.gnuplot.info/) commands that render the chart for the Efficient Frontier with no short sales, pictured below:

[![noshortsales](img/c2f40b04952857ad0201a71e4a2100b3.png)](https://mhittesdorf.wordpress.com/wp-content/uploads/2013/06/noshortsales.png)

Lastly, I want to mention that I originally planned to use a QuantLib [OptimizationMethod](http://quantlib.org/reference/class_quant_lib_1_1_optimization_method.html) class other than [Simplex](http://quantlib.org/reference/class_quant_lib_1_1_simplex.html), such as [ConjugateGradient](http://quantlib.org/reference/class_quant_lib_1_1_conjugate_gradient.html), because I mistakenly believed that QuantLib’s Simplex class could not handle non-linear optimization problems.  However, when I looked at the comments for the Simplex class in the Simplex.hpp header, I learned that it is based on the multidimensional [Nelder Mead Simplex](http://en.wikipedia.org/wiki/Nelder%E2%80%93Mead_method) method, which does support non-linear optimization in several variables.

That concludes this installment of my ‘Introducing QuantLib’ series. I hope you enjoyed it.  In my next post, I will be steering away from portfolio theory and optimization, which have been the focus of my last three posts, and transitioning to a discussion of option pricing.  Check back soon and, as always, I encourage you to submit comments and/or questions.  In the meantime, have fun with QuantLib!`  `## About Mick Hittesdorf

I'm a versatile technical leader with a passion for data analytics, data science and Big Data technology. I have experience working for both large and small organizations, in a variety of roles. I've been responsible for the management and operations of a global data science and analytics platform, developed low latency, proprietary trading systems, managed software development teams, defined enterprise architecture strategies, written white papers and blogs, published articles in industry journals and delivered innovative solutions to clients, both in a consulting and technical sales capacity. My current areas of focus include Big Data, data engineering, data science, R, and Cloud computing`