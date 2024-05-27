<!--yml

分类：未分类

日期：2024-05-18 06:46:39

-->

# 引入 QuantLib：有效前沿 | 金融与科技的一切事物…

> 来源：[`mhittesdorf.wordpress.com/2013/05/25/introducing-quantlib-the-efficient-frontier/#0001-01-01`](https://mhittesdorf.wordpress.com/2013/05/25/introducing-quantlib-the-efficient-frontier/#0001-01-01)

不是的，我最新博客文章的标题并不是什么晦涩的星际迷航引用。实际上，有效前沿是现代投资组合理论的核心概念。现代投资组合理论的奠基人哈里·马科维茨将有效前沿定义为所有有效投资组合的集合，有效投资组合是指在给定风险水平下，最大化投资组合预期回报的资产权重组合，该风险水平由投资组合回报的标准差衡量。绘制每个有效投资组合的波动性与其预期回报产生的图形如下：![efficient](https://mhittesdorf.wordpress.com/wp-content/uploads/2013/05/efficient.png) 这为什么重要呢？大多数人都是风险厌恶者。因此，人们更愿意投资于在较低风险下产生最大回报的资产。有效前沿上的所有投资组合都满足这一要求。没有其他投资组合能在给定风险水平下产生比有效前沿上的投资组合更高的回报。

在许多方面，现代投资组合理论与其开创性思想——有效前沿，以及布莱克-斯科尔斯期权定价公式，可以被认为赋予了定量金融领域诞生的灵感。所以即使 QuantLib 库中没有太多与有效前沿直接相关的内容，我觉得如果不涉及有效前沿我会感到很遗憾。

像我之前的文章一样，我首先通过一个在电子表格中计算的示例来激发接下来的 C++代码。然后使用 QuantLib 在 C++中重现这些结果。但在那之前，让我先介绍一些基本定义和一些简单的方程式，这些方程式对于理解分析是必要的。

**预期回报：** E(Rp) – 与投资组合历史表现一致的资产回报百分比增加/减少，其中总权重必须等于 1。计算两个资产（即两只股票）投资组合的预期回报的公式如下：

投资组合的预期回报 E(Rp) = w1*R1 + (1 – w1)*R2 ，其中 Rp 是投资组合的预期回报，R1 是资产 1 的平均回报，w1 是资产 1 在投资组合中的百分比权重，R2 是资产 2 的平均回报。

**方差：（Vp）**——投资组合回报的历史平均回报与投资组合中资产权重的偏差、各自方差以及资产回报的协方差程度。计算两资产投资组合方差的公式为：

Vp = w1²*V1 + (1-w1)²*V2 + 2*w1*(1-w1)*cov(R1,R2)，其中 Vp 是投资组合的方差，V1 是资产 1 回报的方差，V2 是资产 2 回报的方差，cov(R1,R2)是衡量资产 1 和资产 2 回报同时同向移动或不移动程度的指标。

**波动性（σ）‘sigma’**——最被广泛接受的风险度量。它不过是方差的缩放，计算公式为：σp = sqrt(Vp)

生成有效前沿需要在不改变投资组合方差的情况下最大化投资组合的回报，或者在不改变回报水平的情况下最小化投资组合的方差。因此，计算有效投资组合相当于解决一个优化问题。如果你读过我上篇关于线性优化的帖子，你可能还记得投资组合优化并不是一个线性优化问题。现在你看到了投资组合风险和回报的公式，你可能就会明白为什么了。计算方差的公式是非线性的，它是一个二次多项式函数。因此，我们不能用我上篇帖子中展示的线性规划方法来找到有效前沿。我们可以采用非线性的二次规划方法逐一求解所有有效投资组合，保持投资组合风险恒定并最大化回报函数，或者等价地，保持投资组合回报恒定并最小化投资组合方差函数。正如我上篇帖子所暗示的，我将在未来的帖子中展示这种方法。然而，在这篇帖子中，我将应用经典的程序，用矩阵表示法来表示问题，然后解决一个线性方程组，以计算给定资产权重的最小方差/最大回报值表格。

该问题可以用矩阵表示法表示如下：

R – c = Sz 使得 z = inverse(S) {R – c}，其中 R 是资产回报的向量，c 是一个常数回报率，S 是协方差矩阵，z 是导致有效投资组合权重解决方案的向量，定义为：

x = {x1….xn} 其中每个 xi 代表投资组合中相应资产的权重，所有 xi 的和等于 1；其中特定的权重 xi = zi/所有 zi 的和。

解决这个问题需要相当多的线性代数和矩阵操作。我创建了一个 LibreOffice 电子表格来展示这个过程，我已经将其上传到我的 Box 账户中：[`www.box.com/s/zgl8qm0ujcw0xf05rehu`](https://www.box.com/s/zgl8qm0ujcw0xf05rehu)。以下是截图：

![efcalc](https://mhittesdorf.wordpress.com/wp-content/uploads/2013/05/efcalc.png)

该问题和解决方法的具体信息来自 Simon Benninga 的优秀著作，[*Financial Modeling*, 2nd Edition](http://www.amazon.com/Financial-Modeling-2nd-Edition-Includes/dp/0262024829/ref=sr_1_1?ie=UTF8&qid=1369539924&sr=8-1&keywords=Financial+Modeling+2nd+edition)，我强烈推荐。我发现自己一次又一次地回头看它。为了节省时间和空间，我不会详细介绍电子表格。因此，我鼓励您下载电子表格并自行查看。

总之，电子表格为四支股票（AAPL、IBM、ORCL 和 GOOG）定义了收益的协方差矩阵。它还为 Returns 向量中的每支股票定义了平均收益。常数 c 被相对任意地定义为 5%。

注意：在这个过程的变体中，c 被等同于无风险利率 rf，而在这种情况下，从无风险收益率到有效边界的切线上的有效投资组合（即资本市场线（CML））被称为市场组合。有关这些概念的更多信息，请再次参考 Simon Benninga 的书籍。

过剩收益向量定义为收益 - c。然后计算两个有效组合，组合 A 和组合 B。给定这两个组合，可以通过将这两个组合以各种比例组合起来生成整个有效边界，这些比例总和为 1（例如，在组合 A 中投资 80%，在组合 B 中投资 20%）。

实际上，两个有效组合是上面定义的预期收益和方差公式中定义的 asset1 和 asset2。再次强调，有关程序的具体信息，请查看我的电子表格。

哎呀！这需要大量的工作来为本文的真正重点做准备，即展示如何使用 QuantLib 在 C++ 中生成有效边界。不多说了，这是代码：

```
 #include <iostream> 
#include <cstdlib&gt
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
double calculatePortfolioReturn(double proportionA, double expectedReturnA, double expectedReturnB) {
	return proportionA * expectedReturnA + (1-proportionA) * expectedReturnB;
}

Volatility calculatePortfolioRisk(double proportionA, Volatility volatilityA, Volatility volatilityB, double covarianceAB) {
	return std::sqrt(std::pow(proportionA,2) * std::pow(volatilityA,2) + std::pow(1-proportionA,2) * 
	std::pow(volatilityB,2) + (2 * proportionA * (1-proportionA) * covarianceAB)); 	
}

BOOST_AUTO_TEST_CASE(testEfficientFrontier) {

Matrix covarianceMatrix(4,4);

//row 1
covarianceMatrix[0][0] = .40; //AAPL-AAPL
covarianceMatrix[0][1] = .05; //AAPL-IBM
covarianceMatrix[0][2] = .02; //AAPL-ORCL
covarianceMatrix[0][3] = .04; //AAPL-GOOG
//row 2
covarianceMatrix[1][0] = .05; //IBM-AAPL
covarianceMatrix[1][1] = .20; //IBM-IBM 
covarianceMatrix[1][2] = .01; //IBM-ORCL
covarianceMatrix[1][3] = -.06; //IBM-GOOG
//row 3
covarianceMatrix[2][0] = .02; //ORCL-AAPL 
covarianceMatrix[2][1] = .01; //ORCL-IBM
covarianceMatrix[2][2] = .30; //ORCL-ORCL
covarianceMatrix[2][3] = .03; //ORCL-GOOG
//row 4
covarianceMatrix[3][0] = .04; //GOOG-AAPL
covarianceMatrix[3][1] = -.06; //GOOG-IBM
covarianceMatrix[3][2] = .03; //GOOG-ORCL
covarianceMatrix[3][3] = .15; //GOOG-GOOG

std::cout << "Covariance matrix of returns: " << std::endl;
std::cout << covarianceMatrix << std::endl;

//portfolio return vector         
Matrix portfolioReturnVector(4,1);
portfolioReturnVector[0][0] = .10; //AAPL
portfolioReturnVector[1][0] = .03; //IBM
portfolioReturnVector[2][0] = .07; //ORCL
portfolioReturnVector[3][0] = .08; //GOOG

std::cout << "Portfolio return vector" << std::endl;
std::cout << portfolioReturnVector << std::endl;

//constant 
Rate c = .05;

//portfolio return vector minus constant rate
Matrix portfolioReturnVectorMinusC(4,1);
for (int i=0; i<4; ++i) {
    	portfolioReturnVectorMinusC[i][0] = portfolioReturnVector[i][0] - c;
}

std::cout << boost::format("Portfolio return vector minus constantrate (c = %f)") % c << std::endl;
std::cout << portfolioReturnVectorMinusC << std::endl;

//inverse of covariance matrix
const Matrix& inverseOfCovarMatrix = inverse(covarianceMatrix);

//z vectors
const Matrix& portfolioAz = inverseOfCovarMatrix * portfolioReturnVector;
std::cout << "Portfolio A z vector" << std::endl;
std::cout << portfolioAz << std::endl;
double sumOfPortfolioAz = 0.0;
std::for_each(portfolioAz.begin(), portfolioAz.end(), & {
	sumOfPortfolioAz += n;	
});

const Matrix& portfolioBz = inverseOfCovarMatrix * portfolioReturnVectorMinusC;
std::cout << "Portfolio B z vector" << std::endl;
std::cout << portfolioBz << std::endl;
double sumOfPortfolioBz = 0.0;
std::for_each(portfolioBz.begin(), portfolioBz.end(), & {
	sumOfPortfolioBz += n;	
});

//portfolio weights
Matrix weightsPortfolioA(4,1);
for (int i=0; i<4; ++i) {
	weightsPortfolioA[i][0] = portfolioAz[i][0]/sumOfPortfolioAz;
}		

std::cout << "Portfolio A weights" << std::endl;
std::cout << weightsPortfolioA << std::endl;

Matrix weightsPortfolioB(4,1);
for (int i=0; i<4; ++i) {
	weightsPortfolioB[i][0] = portfolioBz[i][0]/sumOfPortfolioBz;
}		

std::cout << "Portfolio B weights" << std::endl;
std::cout << weightsPortfolioB << std::endl;

//portfolio risk and return
const Matrix& expectedReturnPortfolioAMatrix = transpose(weightsPortfolioA) * portfolioReturnVector;	
double expectedReturnPortfolioA = expectedReturnPortfolioAMatrix[0][0];
const Matrix& variancePortfolioAMatrix =  transpose(weightsPortfolioA) * covarianceMatrix * weightsPortfolioA;
double variancePortfolioA = variancePortfolioAMatrix[0][0];
double stdDeviationPortfolioA = std::sqrt(variancePortfolioA);
std::cout << boost::format("Portfolio A expected return: %f") % expectedReturnPortfolioA << std::endl;
std::cout << boost::format("Portfolio A variance: %f") % variancePortfolioA << std::endl;
std::cout << boost::format("Portfolio A standard deviation: %f") % stdDeviationPortfolioA << std::endl;

const Matrix& expectedReturnPortfolioBMatrix = transpose(weightsPortfolioB) * portfolioReturnVector;	
double expectedReturnPortfolioB = expectedReturnPortfolioBMatrix[0][0];
const Matrix& variancePortfolioBMatrix =  transpose(weightsPortfolioB) * covarianceMatrix * weightsPortfolioB;
double variancePortfolioB = variancePortfolioBMatrix[0][0];
double stdDeviationPortfolioB = std::sqrt(variancePortfolioB);
std::cout << boost::format("Portfolio B expected return: %f") % expectedReturnPortfolioB << std::endl;
std::cout << boost::format("Portfolio B variance: %f") % variancePortfolioB << std::endl;
std::cout << boost::format("Portfolio B standard deviation: %f") % stdDeviationPortfolioB << std::endl;

//covariance and correlation of returns
const Matrix& covarianceABMatrix = transpose(weightsPortfolioA) * covarianceMatrix * weightsPortfolioB;
double covarianceAB = covarianceABMatrix[0][0];
double correlationAB = covarianceAB/(stdDeviationPortfolioA * stdDeviationPortfolioB);
std::cout << boost::format("Covariance of portfolio A and B: %f") % covarianceAB << std::endl;
std::cout << boost::format("Correlation of portfolio A and B: %f") % correlationAB << std::endl;

//generate envelope set of portfolios
double startingProportion = -.40;
double increment = .10;
std::map<double, std::pair<Volatility,double> > mapOfProportionToRiskAndReturn;
std::map<Volatility, double> mapOfVolatilityToReturn;
for (int i=0; i<21; ++i) {
	double proportionA = startingProportion + i*increment;
	Volatility riskEF = calculatePortfolioRisk(proportionA, stdDeviationPortfolioA, stdDeviationPortfolioB, covarianceAB);
	double returnEF = calculatePortfolioReturn(proportionA, expectedReturnPortfolioA, expectedReturnPortfolioB);
	mapOfProportionToRiskAndReturn[proportionA] = std::make_pair(riskEF, returnEF);
	mapOfVolatilityToReturn[riskEF] = returnEF;
}

//write data to a file
std::ofstream envelopeSetFile;
envelopeSetFile.open("/tmp/envelope.dat",std::ios::out);
for (std::map<double, std::pair<Volatility,double> >::const_iterator i=mapOfProportionToRiskAndReturn.begin(); i != mapOfProportionToRiskAndReturn.end(); ++i) {
	envelopeSetFile << boost::format("%f %f %f") % i->first % i->second.first % i->second.second << std::endl;
}
envelopeSetFile.close();

//find minimum risk portfolio on efficient frontier
std::pair<Volatility,double> minimumVariancePortolioRiskAndReturn = *mapOfVolatilityToReturn.begin(); 
Volatility minimumRisk = minimumVariancePortolioRiskAndReturn.first; 
double maximumReturn = minimumVariancePortolioRiskAndReturn.second;
std::cout << boost::format("Maximum portfolio return for risk of %f is %f") % minimumRisk % maximumReturn << std::endl;

//generate efficient frontier
std::map<Volatility, double> efficientFrontier;
for (std::map<double, std::pair<Volatility,double> >::const_iterator i=mapOfProportionToRiskAndReturn.begin(); i != mapOfProportionToRiskAndReturn.end(); ++i) {
	efficientFrontier[i->second.first] = i->second.second;
	if (i->second.first == minimumRisk) break;
}

//write efficient frontier to file
std::ofstream efFile;
efFile.open("/tmp/ef.dat", std::ios::out);
for (std::map<Volatility, double>::const_iterator i=efficientFrontier.begin(); i != efficientFrontier.end(); ++i) {
	efFile << boost::format("%f %f") % i->first % i->second << std::endl;
}
efFile.close();

//plot with gnuplot using commands below. Run 'gnuplot' then type in: 
/*
set key top left
set key box
set xlabel "Volatility"
set ylabel "Expected Return"
plot '/tmp/envelope.dat' using 2:3 with linespoints title "Envelope", '/tmp/ef.dat' using 1:2  w points pointtype 5 t "Efficient Frontier"
*/

}

}
```

该代码产生以下输出

`收益的协方差矩阵：

| 0.4 0.05 0.02 0.04 |
| --- |
| 0.05 0.2 0.01 -0.06 |
| 0.02 0.01 0.3 0.03 |

| 0.04 -0.06 0.03 0.15 |`

`Portfolio return vector

| 0.1 |
| --- |
| 0.03 |
| 0.07 |

| 0.08 |`

`投资组合收益向量减去常数率（c = 0.050000）

| 0.05 |
| --- |
| -0.02 |
| 0.02 |

| 0.03 |`

`Portfolio A z vector

| 0.150387 |
| --- |
| 0.27627 |
| 0.156862 |

| 0.572366 |`

`Portfolio B z vector

| 0.122915 |
| --- |
| -0.0977877 |
| 0.0499195 |

| 0.118124 |`

`Portfolio A weights

| 0.130105 |
| --- |
| 0.239012 |
| 0.135707 |

| 0.495176 |`

`Portfolio B weights

| 0.636303 |
| --- |
| -0.506224 |
| 0.258422 |

| 0.611499 |`

`Portfolio A 预期收益率：0.069294

Portfolio A 方差：0.059949

Portfolio A 标准差：0.244845

Portfolio B 预期收益率：0.115453

Portfolio B 方差：0.338835

Portfolio B 标准差：0.582096

组合 A 和 B 的协方差：0.099883

组合 A 和 B 的相关性：0.700817

在风险为 0.227896 的情况下，投资组合的最大收益为 0.060063`

在源代码列表的末尾，您可以看到所有 env 包组合都被写入磁盘。env 包组合构成了由此过程生成的所有组合的超集，其中一些并不是有效的。最后，位于有效前沿的组合被写入磁盘。我这样做是为了使用我最喜欢的开源绘图工具[gnuplot](http://www.gnuplot.info/)绘制有效前沿。在我的代码列表的注释部分，您可以找到我编写的创建图表的 gnuplot 脚本。

正如您可能已经注意到的，在这个例子中我大量使用了 QuantLib 的[Matrix](http://quantlib.org/reference/class_quant_lib_1_1_matrix.html)类。Matrix 类支持最常用的线性代数函数，包括逆、转置、行列式以及矩阵的乘法/除法/加法/减法。与 Matrix 类相辅相成的是一个[Array](http://quantlib.org/reference/class_quant_lib_1_1_array.html)类，它可以用来表示向量，尽管在这个例子中我没有实际使用 Array 类。实际上，我发现直接使用 nx1 矩阵更容易且更一致。QuantLib 还提供了一些定义在`<ql/math/matrixutilities/... />`中的矩阵分解实用类，可以操作 Matrix 类，如[SVD](http://quantlib.org/reference/class_quant_lib_1_1_s_v_d.html)。此外，QuantLib 还提供了一些命名空间级别的函数，可以操作 Matrix 实例，如 factorReduction()和 CholeskyDecomposition()。

至此，我将结束这篇相当长的帖子。希望您喜欢它，并且和往常一样，请提出问题、评论和建议。祝您使用 QuantLib 愉快！
