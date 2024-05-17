<!--yml
category: 未分类
date: 2024-05-12 19:45:27
-->

# IronPython | Coding the markets

> 来源：[https://etrading.wordpress.com/ironpython/#0001-01-01](https://etrading.wordpress.com/ironpython/#0001-01-01)

Some notes on IronPython, CPython, .Net and integration…

Avoiding importing some CPython modules: you may not want to make your IronPython coded assemblies depend on an installation of CPython at c:\python25\. If so you must avoid importing a lot of modules that CPython coding takes for granted…

*   types – don’t use expressions like if type(myObj) == types.ListType. Use if type(myObj) == type([]) instead. Sometimes implicit is better than explicit !
*   string – if you go back to CPython 1.5.2 you may still be in the habit of coding string.split() or string.join(). Switch over to member methods eg “”.join( ) andyou can avoid importing the string module.

Some modules can be imported just the same in IronPython and CPython…

Genericity

*   Use ContainsKey, not has_key. Both Hashtable and Python’s built in dictionary have it.