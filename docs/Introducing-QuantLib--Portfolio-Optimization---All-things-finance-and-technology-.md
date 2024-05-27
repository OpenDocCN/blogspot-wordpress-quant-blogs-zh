<!--yml

分类：未分类

日期：2024-05-18 06:46:31

-->

# 介绍 QuantLib：组合优化 | 金融与科技一切事物…

> 来源：[`mhittesdorf.wordpress.com/2013/06/20/introducing-quantlib-portfolio-optimization/#0001-01-01`](https://mhittesdorf.wordpress.com/2013/06/20/introducing-quantlib-portfolio-optimization/#0001-01-01)

欢迎回来。如果您阅读了我的最后两篇帖子，您可能还记得我展示了如何使用 QuantLib 在债券组合构建问题中进行线性优化以及通过有效前沿概念进行均值-方差组合分析。在我“介绍 QuantLib”系列的这一部分中，我将结合这两篇帖子中的每个元素，以展示在组合构成存在约束的情况下，QuantLib 如何生成有效前沿。特别是，不允许进行卖空。在没有卖空的情况下找到有效前沿将需要反复解决一个非线性组合优化问题，其中组合中的每个资产都必须有非负权重。

像之前的帖子一样，我首先会在电子表格中建模问题，然后使用 QuantLib 库中的类在 C++中复制解决方案。该模型的基本要素借鉴了 Simon Benninga excellent book *[Financial Modeling, 2nd Edition](http://www.amazon.com/Financial-Modeling-2nd-Simon-Benninga/dp/0262024829/ref=sr_1_1?s=books&ie=UTF8&qid=1371528897&sr=1-1&keywords=financial+modeling+2nd+edition).* 特别是，必须确定四个资产（AAPL，IBM，ORCL，GOOG）的权重，以便在以下约束条件下最大化组合的[夏普比率](http://en.wikipedia.org/wiki/Sharpe_ratio):

+   组合中资产的权重必须总和为 1

+   组合中每个资产的权重必须大于或等于零

以下是完整电子表格的屏幕截图，您可以通过我的 Box 账户下载：[`www.box.com/s/7w4tvfqueqqu676vhz5l`](https://www.box.com/s/7w4tvfqueqqu676vhz5l)

如我在线性优化方面的早期帖子所述，所有优化问题都包含一个必须最大化或最小化的函数，这个函数称为目标函数。在投资组合优化问题中，*θ*是要最大化的目标函数的值。它被定义为超额回报与投资组合标准差的比率，其中超额回报是投资组合回报减去无风险利率，在电子表格中定义为常数 c。θ本质上与投资组合的 Sharpe 比率相同，对于给定的 c 值。更直观地说，θ是给定风险量的一种回报度量。在最大化θ时，我们寻求将资本分配给投资组合中的四只股票，以便以最小的风险获得最大的回报。这个目标与大多数投资者都是风险厌恶的事实一致。

![efnscalc](https://mhittesdorf.wordpress.com/wp-content/uploads/2013/06/efnscalc.png)

顺便说一下，您可能已经注意到这个电子表格是使用 OpenOffice 创建的，而不是我之前帖子中使用的 LibreOffice。我不得不切换到 OpenOffice，以便安装“[非线性规划求解器](http://extensions.openoffice.org/en/project/NLPSolver)”OpenOffice 扩展，而这个扩展目前在我笔记本电脑的 Ubuntu 12.04 操作系统上不被 LibreOffice 支持。没有非线性求解器扩展，LibreOffice 会检测到问题是非线性的，并无法找到解决方案：

![notlinear](https://mhittesdorf.wordpress.com/wp-content/uploads/2013/06/notlinear.png)

现在让我们看看如何在 QuantLib 中设置和解决此问题。以下是 C++代码：

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

当运行此代码时，它会为 c 的-0.035 和 0.16 之间的所有值求解最优权重。例如，当 c=0.05 时的输出结果为：

—————————————

解决方案类型：固定点

常数（c）：0.0500

AAPL 权重：0.5659

IBM 权重：0.1047

ORCL 权重：0.3294

GOOG 权重：0.0000

θ：0.1839

投资组合平均值：0.0876

投资组合标准差：0.2046

————————————

这个解决方案与使用非线性求解器扩展的 OpenOffice 电子表格得到的解决方案非常接近。所以，看起来 QuantLib 代码正在做正确的事情。太酷了！

在代码列表的末尾，我提供了生成无空头销售的 Efficient Frontier 图表的[gnuplot](http://www.gnuplot.info/)命令，如下所示：

![noshortsales](https://mhittesdorf.wordpress.com/wp-content/uploads/2013/06/noshortsales.png)

最后，我想提一下，我最初计划使用除了[Simplex](http://quantlib.org/reference/class_quant_lib_1_1_simplex.html)之外的 QuantLib [OptimizationMethod](http://quantlib.org/reference/class_quant_lib_1_1_optimization_method.html)类，比如[ConjugateGradient](http://quantlib.org/reference/class_quant_lib_1_1_conjugate_gradient.html)，因为我错误地认为 QuantLib 的 Simplex 类无法处理非线性优化问题。然而，当我查看 Simplex 类的注释时，在 Simplex.hpp 头文件中，我了解到它基于多维[Nelder Mead Simplex](http://en.wikipedia.org/wiki/Nelder%E2%80%93Mead_method)方法，该方法支持在多个变量中的非线性优化。

这就结束了我的“介绍 QuantLib”系列文章的这一部分。希望您喜欢。在我的下一篇文章中，我将偏离投资组合理论和优化，这是我的最后三篇文章的重点，转向讨论期权定价。很快就会更新，如往常一样，我鼓励您提交评论和/或问题。与此同时，请尽情享受 QuantLib 带来的乐趣！`关于 Mick Hittesdorf`##

我是一个多才多艺的技术领导者，对数据分析、数据科学和大数据技术充满热情。我在大型和小型组织中都有工作经验，担任过各种角色。我负责管理一个全球数据科学和分析平台，开发了低延迟的、专有的交易系统，管理软件开发团队，制定了企业架构策略，撰写了白皮书和博客，在行业期刊上发表文章，并以咨询和技术销售的身份向客户提供创新解决方案。我当前的关注领域包括大数据、数据工程、数据科学、R 和云计算。
