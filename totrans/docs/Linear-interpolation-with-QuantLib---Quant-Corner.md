<!--yml
category: 未分类
date: 2024-05-18 08:10:18
-->

# Linear interpolation with QuantLib | Quant Corner

> 来源：[https://quantcorner.wordpress.com/2011/02/14/linear-interpolation-with-quantlib/#0001-01-01](https://quantcorner.wordpress.com/2011/02/14/linear-interpolation-with-quantlib/#0001-01-01)

 ***QuantLib** includes numerous mathematical and function-related tools. And, it often makes the things very easy for us. As an illustration, we implement the **linear interpolation** function.
 *In the example code below, we compute linearly interpolated **f(x)** values for the corresponding **x** = 1,5 and 3,5.**

 **| **x** | **0** | **1** | **1.5** | **2** | **3** | **3,5** | **4** |
| **f(x)** | **2** | **3.5** | **?** | **3** | **2.75** | **?** | **5** |

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