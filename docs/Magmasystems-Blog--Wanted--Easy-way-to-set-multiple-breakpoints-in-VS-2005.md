<!--yml

分类：未分类

date: 2024-05-18 05:17:21

-->

# Magmasystems 博客：想要的：在 VS 2005 中设置多个断点的简单方法

> 来源：[`magmasystems.blogspot.com/2006/10/wanted-easy-way-to-set-multiple.html#0001-01-01`](http://magmasystems.blogspot.com/2006/10/wanted-easy-way-to-set-multiple.html#0001-01-01)

我正在追踪一些遗留代码，其中某个类有大约 20 个不同的构造函数。我希望有一种方法可以让我告诉 VS.NET 2005 在每个构造函数上设置断点。

同样，给我一个方法的名字，我希望有一种方法可以在该方法的所有变体入口处设置断点。例如，如果我有一个名为 GetValue()的方法，我们有很多多态方法，比如

void GetValue(ref bool b)

void GetValue(ref int i)

void GetValue(ref double d)

void GetValue(ref string s)

应该有一种方法可以在每个 GetValue()方法的入口处用一次鼠标右键点击设置断点。

这听起来像是 Resharper 的一个可能的增强功能？或者也许有人写了 VS 宏来做这件事？

©2006 Marc Adler - 版权所有
