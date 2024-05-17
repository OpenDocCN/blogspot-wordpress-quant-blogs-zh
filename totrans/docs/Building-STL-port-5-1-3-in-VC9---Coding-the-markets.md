<!--yml
category: 未分类
date: 2024-05-12 19:35:41
-->

# Building STL port 5.1.3 in VC9 | Coding the markets

> 来源：[https://etrading.wordpress.com/2011/02/01/building-stl-port-5-1-3-in-vc9/#0001-01-01](https://etrading.wordpress.com/2011/02/01/building-stl-port-5-1-3-in-vc9/#0001-01-01)

## Building STL port 5.1.3 in VC9

### February 1, 2011

It was a bit of a struggle to get STLport 5.1.3 to build with VC9/Visual Studio 2008\. I got some hints [here](http://blog.narahome.com/entry/STLPORT-VS2008), but also had to remove the .rc dependency from Makefile.inc and jiggle LIB and INCLUDE env vars to pick up headers and libs from an MS SDK dir separate from the Visual Studio dir. Then an nmake /fmsvc.mak dbg-shared did the trick. Of course I’m not building with debug iterators – I do value my sanity !