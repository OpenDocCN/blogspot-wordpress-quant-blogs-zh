<!--yml

分类：未分类

date: 2024-05-12 19:45:54

-->

# IronPython 继承关系 | 编码市场

> 来源：[`etrading.wordpress.com/2007/10/02/ironpython-inheritance/#0001-01-01`](https://etrading.wordpress.com/2007/10/02/ironpython-inheritance/#0001-01-01)

## IronPython 继承关系

### 2007 年 10 月 2 日

所以我开始在我的 C++/托管 C++/C#/IronPython 桌面栈中取得一些进展。我发现 CLR 中的继承只能单向工作。具体来说，Python 类可以从 C# 基类中继承，但 Python 继承对 C# 反射代码是透明的。如果一个人有一个从 C# 基类和 C# 接口派生的 Python 类，那么尝试使用反射来访问该 Python 类的 C# 代码将会失败。为了理解原因，使用 Lutz Roeder 的 Reflector 工具查看 IronPython 程序集的内部，并将符号与从 C# 基类中进行类似继承的 C# 程序集进行比较。IronPython 程序集引入了自己的运行时基础设施，这不符合其他 CLR 语言的期望。

那么有什么解决办法？正如在集成练习中一如既往，我在 C# 中引入了一个符合 C# 代码期望的垫片，同时将其转发到 Python。
