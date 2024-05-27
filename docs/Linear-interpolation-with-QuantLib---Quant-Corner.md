<!--yml

分类：未分类

日期：2024-05-18 08:10:18

-->

# 线性插值法与 QuantLib | 量化角

> 来源：[`quantcorner.wordpress.com/2011/02/14/linear-interpolation-with-quantlib/#0001-01-01`](https://quantcorner.wordpress.com/2011/02/14/linear-interpolation-with-quantlib/#0001-01-01)

***QuantLib** 包含了许多数学和函数相关的工具。而且，它经常让我们的事情变得非常简单。作为一个示例，我们实现了**线性插值**函数。

*在下面的示例代码中，我们对相应的**x** = 1,5 和 3,5 计算了线性插值的**f(x)**值。*

**| **x** | **0** | **1** | **1.5** | **2** | **3** | **3,5** | **4** |

| ** | **f(x)** | **2** | **3.5** | **?** | **3** | **2.75** | **?** | **5** |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |

```
#include<ql\quantlib.hpp>
#include<vector>

using namespace QuantLib;
using std::vector;
using std::cout;
using std::endl;

int main (int, char*[]){

	// Vector creation
	double xVectorData[]= {0, 1, 2, 3, 4};
	double yVectorData[]= {2, 3.5, 3, 2.75, 6};
	vector<double>xVector(xVectorData, xVectorData+5);
	vector<double>yVector(yVectorData, yVectorData+5);

	// Implementation of the Linear interpolation function
	LinearInterpolation linInt (
		xVector.begin(),
		xVector.end(),
		yVector.begin());

	// Outputting
	cout << "Linearly interpolated value for :" << endl;
	cout << "x = 1.5 is " << linInt (1.5) << endl;
	cout << "x = 3.5 is " << linInt (3.5) << endl;

	return 0;
}
```**
