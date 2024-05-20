<!--yml
category: 未分类
date: 2024-05-18 05:17:21
-->

# Magmasystems Blog: Wanted: Easy way to set multiple breakpoints in VS 2005

> 来源：[http://magmasystems.blogspot.com/2006/10/wanted-easy-way-to-set-multiple.html#0001-01-01](http://magmasystems.blogspot.com/2006/10/wanted-easy-way-to-set-multiple.html#0001-01-01)

I am tracing through some legacy code where a certain class has about 20 different constructors. I would like some way where I can tell VS.NET 2005 to set a breakpoint on each of the constructors.

Likewise, given the name of a method, I would like a way to set a breakpoint at the entry to all of the variants of the method. For instance, if I have a method called GetValue(), and we have a large number of polymophic methods such as

void GetValue(ref bool b)

void GetValue(ref int i)

void GetValue(ref double d)

void GetValue(ref string s)

there should be a way to set a breakpoint at the entry point to each one the GetValue() methods with one one right-click of the mouse.

Sounds like a possible enhancement for Resharper? Or maybe, someone has written a VS macro to do this?

©2006 Marc Adler - All Rights Reserved