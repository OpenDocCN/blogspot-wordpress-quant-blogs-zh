<!--yml

分类：未分类

日期：2024-05-12 19:45:27

-->

# IronPython | 编写市场代码

> 来源：[`etrading.wordpress.com/ironpython/#0001-01-01`](https://etrading.wordpress.com/ironpython/#0001-01-01)

关于 IronPython、CPython、.Net 和集成的的一些说明…

避免导入一些 CPython 模块：你可能不希望让你的 IronPython 代码组件依赖于 c:\python25\中的 CPython 安装。如果是这样，你必须避免导入许多 CPython 编程认为理所当然的模块…

+   类型 – 不要使用像 if type(myObj) == types.ListType 这样的表达式。应该使用 if type(myObj) == type([])。有时候隐式比显式更好！

+   字符串 – 如果你回到 CPython 1.5.2，你可能还习惯于编写字符串.split()或者字符串.join()。转向成员方法，例如“”.join()，并且你可以避免导入字符串模块。

一些模块可以在 IronPython 和 CPython 中以相同的方式导入…

泛型

+   使用 ContainsKey 而不是 has_key。Hashtable 和 Python 内置的字典都有它。
