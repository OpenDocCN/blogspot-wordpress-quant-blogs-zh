<!--yml
category: 未分类
date: 2024-05-12 19:33:29
-->

# LNK1120 | Coding the markets

> 来源：[https://etrading.wordpress.com/2013/04/05/lnk1120/#0001-01-01](https://etrading.wordpress.com/2013/04/05/lnk1120/#0001-01-01)

## LNK1120

### April 5, 2013

Just fixed one of those infuriating Visual Studio link errors. There’s lots of good stuff on stackoverflow, of course, but this one was a bit more subtle. It’s still probably quite common though, if you’re integrating code with differing build systems. The root of the problem is linking code built with Visual C++’s own STL with code using STLport. There are various tools and options in Visual Studio that will help you find the root of the error.

dumpbin: command line utility to dump all the symbols defined and referenced by a binary. You can use it on .exe, .lib and .obj files.

undname: command line utility to undecorate C++ names. Given a mangled name it will demangle it.

/P: compiler option to write pre-processor output to file as a .i file. Useful for seeing which headers are actually pulled into each unit of compilation.

/VERBOSE: linker option which will tell you which libraries and objects are searched, and which symbols they resolve.