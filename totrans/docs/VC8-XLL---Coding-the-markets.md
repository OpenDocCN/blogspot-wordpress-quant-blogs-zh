<!--yml
category: 未分类
date: 2024-05-12 19:48:10
-->

# VC8 XLL | Coding the markets

> 来源：[https://etrading.wordpress.com/2007/03/25/vc8-xll/#0001-01-01](https://etrading.wordpress.com/2007/03/25/vc8-xll/#0001-01-01)

## VC8 XLL

### March 25, 2007

So if you’re building an XLL in VC8, and you’re using a .def file to specify the exported symbols, make sure you give the linker a /DEF:myaddin.xll switch. Unlike the VC6 linker, VC8 doesn’t automatically pick up the .def. Took me a good few hours to figure that, using depends and filemon to look for missing dependencies etc. All the time depends was telling me that my XLL was exporting no symbols, but I couldn’t see it, so fixated was I on more subtle possible problems.