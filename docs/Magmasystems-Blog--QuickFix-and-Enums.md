<!--yml

category: 未分类

date: 2024-05-18 05:10:14

-->

# Magmasystems Blog: QuickFix and Enums

> 来源：[`magmasystems.blogspot.com/2007/03/quickfix-and-enums.html#0001-01-01`](http://magmasystems.blogspot.com/2007/03/quickfix-and-enums.html#0001-01-01)

It seems that the latest version of QuickFix has a .NET assembly and FIX 4.4 support, so I am going to be using it in an OMS demo that I am putting together to show off my .NET client-side framework.

One thing that I wish that the QuickFix guys did was to use enums instead of static const chars. For example, here is the definition of the OrdType class (this class is written in Managed C++, but a lot of the other .NET classes are in C#).

`public __gc class OrdType : public CharField

{

public:

static const int FIELD = 40;

static const __wchar_t MARKET = '1';

static const __wchar_t LIMIT = '2';

static const __wchar_t STOP = '3';

static const __wchar_t STOP_LIMIT = '4';

.............

OrdType() : CharField(40) {}

OrdType(__wchar_t data) : CharField(40, data) {}

};`

我 completely understand why they used const chars, but for data-binding purposes, it is easier for me to use enums.

我 wonder if I should reflect over a few classes and translate these classes to corresponding enumerated types.

I'm supposed to be a manager .. I have to find other people to do this kind of stuff for me. However, in my group, I am the only .NET person in a vast sea of Java-ness.

©2007 Marc Adler - All Rights Reserved
