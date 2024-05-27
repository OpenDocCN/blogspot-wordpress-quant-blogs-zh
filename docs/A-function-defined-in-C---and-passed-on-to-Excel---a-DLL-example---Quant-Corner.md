<!--yml

类别：未分类

日期：2024-05-18 08:10:26

-->  

# 在 C++中定义的函数并传递到 Excel：一个 DLL 示例 | 量化角

> 来源：[`quantcorner.wordpress.com/2011/04/02/afunction-defined-in-c-and-used-in-excel-a-dll-exampl/#0001-01-01`](https://quantcorner.wordpress.com/2011/04/02/afunction-defined-in-c-and-used-in-excel-a-dll-exampl/#0001-01-01)

想象一下，你需要的函数在**Excel**中不可用，而且你更喜欢用**C++**而不是**Excel VBA**编程。在这种情况下，您将希望将自己定义的函数封装到一段**C++**代码中，并编写一个接口，以便在**Excel**中使用它。这样，您将同时拥有**C++**的强大和快速计算能力以及**Excel**的用户友好性。

这是这篇文章的目的。我们将写一个**DLL**，由标准的***.cpp**文件和一个***.def**文件（模块定义文件）组成。然后，我们将通过几行**Excel VBA**代码告诉**Excel**有关这个**DLL**。

我们集成到**Excel**（2007 版）中的一个简单**DLL**的示例源自*期权、期货和其他衍生品 7^(th)*（J.C Hull）, p.109。作者在那里解释了如何计算提供无收入的投资资产的远期合同的价值。我们将编写相应的代码。

J.C Hull 给出了这样一个例子，一个投资者在不支付股息的标的上持有了一个长期远期头寸，交割价格为$24（K=24）。到期时间长度为 6 个月（T=0,5）。今天标的物的价格为$25（S[0]=25），无风险利率（连续复利）为年利率 10%（R = 10%）。

让**f**是今天的长期远期合同的价值，f = (F[0] – K ) e ^(–rT) 其中 F[0] = S[0] e^(rT)

_______

S[0] = 25

K = 24

r = 10%

T = 0,5

_______

请参考[使用 MS Visual Basic 2010 创建 DLL 项目](https://quantcorner.wordpress.com/2011/03/28/creating-a-dll-project-with-ms-visual-basic-2010)来开始创建一个**MS Visual Studio 2010**的**DLL**项目。

首先，我们的***.cpp**文件将包含计算**f**的函数的定义是：

```
#include<math.h>

double _stdcall discountingLongForward(
	double underlying,
	double K,
	double rate,
	double timeToMaturity)
{
double forward = underlying * (exp (rate * timeToMaturity));
double discountedLongForward = (forward - K) * (exp (-rate * timeToMaturity));
return discountedLongForward;
}
```

关键字**_stdcall**是一个函数调用关键字。在这里，**discountingLongForward**是要由**Excel**调用的函数。

现在，***.def**文件列出了必须传递给**Excel**的函数。

这很直接

```
LIBRARY
EXPORTS
	discountingLongForward
```

**LIBRARY**一行在添加***.def**时会自动写入。就让它。

在这个阶段，你已经有了你的***.cpp**和***.def**文件。是时候按照通常的方式进行编译了。

我们现在转向**Excel**。我们必须告诉它我们的**DLL**存在，它位于哪里，以及其输入和输出的性质。

```
Declare Function discountingLongForward Lib _
"C:\ [folder] ... [your_DLL_file_name.dll]" _
(ByVal underlying As Double, ByVal K As Double, _
ByVal rate As Double, ByVal timeToMaturity As Double) As Double
```

注意这里的**ByVal**关键字，因为**Excel**的默认模式是**ByRef**。这是为了确保计算结果正确。但是，有人可能认为对于这个非常基本的例子来说这是不必要的。

就是这样！

最后，我们展示了我们的**DLL**在工作中的表现。毫无意外，它得到了与 J.C Hull 的书中所读相同的计算结果。

![](https://quantcorner.wordpress.com/wp-content/uploads/2011/04/discountinglongforward_formula.jpg)

![](https://quantcorner.wordpress.com/wp-content/uploads/2011/04/discountinglongforward_calculation_result.jpg)
