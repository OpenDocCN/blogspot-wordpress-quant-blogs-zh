<!--yml
category: 未分类
date: 2024-05-12 19:46:23
-->

# Python 2.5.1 | Coding the markets

> 来源：[https://etrading.wordpress.com/2007/06/18/python-251/#0001-01-01](https://etrading.wordpress.com/2007/06/18/python-251/#0001-01-01)

## Python 2.5.1

### June 18, 2007

The standard [Python 2.5.1](http://www.python.org/download/releases/2.5.1/) binaries in the Windows download are built with Visual C++ 7.1, which means that the python25.dll supplied references msvcr71.dll. If you’re linking python25.lib and building with Visual C++ 8, you’ll get a core dump.

Fortunately the source tarball has a VC8 project file that build right out of the box. So it was really no trouble to generate a python25.dll that uses msvcr80.dll. Kudos to the Pythonistas for having a well sorted build…