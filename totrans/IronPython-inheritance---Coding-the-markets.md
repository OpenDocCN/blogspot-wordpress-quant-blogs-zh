<!--yml
category: 未分类
date: 2024-05-12 19:45:54
-->

# IronPython inheritance | Coding the markets

> 来源：[https://etrading.wordpress.com/2007/10/02/ironpython-inheritance/#0001-01-01](https://etrading.wordpress.com/2007/10/02/ironpython-inheritance/#0001-01-01)

## IronPython inheritance

### October 2, 2007

So I’m starting to make some progress with my C++/managed C++/C#/IronPython desktop stack. And I’ve discovered that inheritance only works one way in the CLR. Namely, Python classes can inherit from C# bases, but Python inheritance is opaque to C# relection code. If one has a Python class derived from a C# base class and a C# interface, then C# code that attempts to use reflection to get access to that Python class will fail. To understand why, use Lutz Roeder’s Reflector tool to look inside an IronPython assembly, and compare the symbols to a C# assembly doing similar inheritance from C# base classes. The IronPython assembly introduces its own runtime infrastructure that doesn’t meet the expectations of other CLR languages in terms.

So what’s the workaround ?  As ever in integration exercises, I introduced a shim in C# that meets the expectations of the C# code while dispatching into Python.