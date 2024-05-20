<!--yml
category: 未分类
date: 2024-05-18 05:19:05
-->

# Magmasystems Blog: Comments Added and WMI Blues

> 来源：[http://magmasystems.blogspot.com/2006/08/comments-added-and-wmi-blues.html#0001-01-01](http://magmasystems.blogspot.com/2006/08/comments-added-and-wmi-blues.html#0001-01-01)

I spaced out on approving and publishing the moderated comments (thanks Craig). So now, there are about 30 commnents, dating back from late May.

I was wondering why nobody congratulated me on my new job :-)

Starting to play around with Microsoft's WMI for instrumenting applications. I need to beat up on Microsoft for not letting you author .NET-based WMI providers that allow method invocation and property setters. All you can do with .NET WMI providers are receive events and do property gets. You cannot change a value through a property setting, nor can you manage an application by calling a method on a provider.

Seems that if you want to write a fully-functional WMI provider, then you have to drop down to COM (even using ATL) and C++.

This limitation is severe. This means that I cannot write a .NET app that can be managed by a .NET provider. This means that, if I want to write a monitoring and management dashboard (for monitoring, let's say, a .NET-based trading system), I have to drag out my old COM/ATL books and write unmanaged code. Ugh!

It seems as if

[plenty of people](http://groups.google.com/groups/search?ie=UTF-8&q=WMI+.NET+provider+methods&qt_s=Search)

on the newsgroups share my pain.

©2006 Marc Adler - All Rights Reserved