<!--yml

分类： 未分类

日期：2024 年 5 月 18 日 06:48:58

-->

# HOXO-M - 日本匿名数据分析小组 - : 使用 R 在 Excel 中进行 .NET 编程的另一种方式

> 来源：[`mockquant.blogspot.com/2011/07/another-way-to-use-r-in-excel-for-net.html#0001-01-01`](http://mockquant.blogspot.com/2011/07/another-way-to-use-r-in-excel-for-net.html#0001-01-01)

你知道的，

[RExcel](http://sunsite.univie.ac.at/rcom/)

为我们提供了一种将 R 与 Excel 结合使用的方式。

但是，这只是为了安装一些 COM 组件，可能不是编程，而是 Excel 操作的麻烦事！

如果你是 .NET 程序员，还有另一种方法可以从 Excel 中调用 R。

我想给你展示一个简单的例子。

我们需要两个库来执行这个操作。

1.  [Excel-DNA](http://exceldna.typepad.com/)

1.  [R.NET](http://rdotnet.codeplex.com/)

首先，你需要从这里下载 ExcelDNA

[这里](http://exceldna.codeplex.com/releases/view/66405)

。

然后，转到"分销"文件夹。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgkPZVZbyFUI-bGpjXvuS0sEecq4ULl7gk3Q1OhYcxnWKvFQNm41ojGt7UpSQ4m7ydVMLbEUeWy0aF5kHEBZ0NMDOkUWCQoNXueHn0ycHHUwBv1Rpj-nh18180QJL3WAWeYvvugrcj6a6c/s1600/20110704_1.PNG)

这个文件夹中你只需要这三个文件（ExcelDna.dna, ExcelDna.xll, ExcelDna.Integration.dll）。

（我假设你的操作系统是 32 位的 windows。）

其次，你需要从这里下载 R.NET

[这里](http://rdotnet.codeplex.com/releases/view/61617)

。

你可以把这些文件设置（或者复制）到你喜欢的任何文件夹中。

接下来，启动你的 IDE。这次我使用了 VC#。

当然，你也可以像使用 VB.NET 一样使用其他 .NET 语言。

创建新项目，选择"Class library"作为模板，并按如下编写程序。

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using ExcelDna.Integration;
using RDotNet;

namespace CSLib
{
    public class CSLib
    {
        static REngine rengine = null;
        static CSLib()
        {
            // Set the folder in which R.dll locates.
            REngine.SetDllDirectory(@"C:\Program Files\R\R-2.13.0\bin\i386");
            rengine = REngine.CreateInstance("RDotNet", new[] { "-q" });
        }            
        [ExcelFunction(Description = "get random numbers obey to normal distribution")]
        public static double [] MyRnorm(int number)
        {
            return (rengine.EagerEvaluate("rnorm(" + number + ")").AsNumeric().ToArray());
        }
    }
} 
```

在这种情况下，我定义了一个函数，该函数生成遵循标准正态分布的随机数。如果你使用或安装了其他版本的 R，修改"SetDllDirectory"函数调用。

所有源代码和解决方案文件都在这里

[这里（github）](https://github.com/teramonagi/CS-EX_RDotNET_ExcelDNA)

。

接下来，添加

R.NET.dll

还有

ExcelDna.Integration.dll

作为你项目的参考。

现在，一切都准备就绪。让我们来编译吧！

编译完成后，你需要修改你的 ExcelDna.dna 文件。

使用记事本编辑这个文件，像下面这样。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgMdd12ZiGDdDvSQJY-xPp17hGR_dbaFi95yqJ5GzJUI6dthyphenhyphenkAGH6APz_ZuOTCGFWMogq8Wed6hlug0orHqHuwKe0kTyb6OSSuaDLGVMwJX5OHRVHA-J8KpHZOnprTLAHVhOYrVoEUbm0/s1600/201110704_3.PNG)

(v4.0 指的是你的 .NET framework 版本。如果需要的话，修改这个数字)

(如果你的 DLL 的相对路径不是从 ExcelDNA.xll 开始的 "CSLib.dll"，那么你需要更正这个名字)

（我在同一个文件夹中部署了 CSLib.dll, ExcelDna.xll, ExcelDna.dna）

在那之后，双击你的 ExcelDna.xll 并创建一个新的 Excel 表格。

正如你下面所看到的，你可以使用自己在 C# 语言中定义的函数！

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgzO0hUb4IGw2le-eqv3AHoh17Z4agvMzua8rKd3Pg6adc0BdBB-_G3zPoYC_Osk2yMfrxbHg46mMSOGgosTRfZ5w1a5htyQ9vLKmJLKHZdqCcc8ZcUKQHCENB0ryO2DhtQyC5TgwkMK48/s1600/20110704_2.PNG)

Enjoy !
