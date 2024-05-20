<!--yml
category: 未分类
date: 2024-05-12 19:32:48
-->

# C++ libs & ABI compatilibilty | Coding the markets

> 来源：[https://etrading.wordpress.com/2014/05/14/c-libs-abi-compatilibilty/#0001-01-01](https://etrading.wordpress.com/2014/05/14/c-libs-abi-compatilibilty/#0001-01-01)

## C++ libs & ABI compatilibilty

### May 14, 2014

When you’re building a server product that will support C++ APIs you need to consider your ABI – the binary interface. Typically, C++ APIs are distributed as headers and libs. If the functions your API exports include parameters that use, for instance, std::string, you immediately have a problem, as you’re requiring client code to use the same STL implementation as you did to build the lib. That’s OK if client code has access to the source, and can rebuild. But commercial, proprietary products, tend not to distribute source. So how to avoid forcing dependencies on API client code? I went searching for some resources, and found two especially good ones I had to flag.

Here’s  [Thiago Macieira on binary compatibility](http://events.linuxfoundation.org/sites/events/files/slides/Binary_Compatibility_for_library_devs.pdf): an excellent presentation with guidelines for library authors. Here’s a summary of Thiago’s recommendations…

1.  Use pimpl idiom to hide object size
2.  Use plain old data types in function signatures
3.  Don’t hand out ptrs or refs to internals
4.  No inline funcs
5.  All classes need one non inline virtual; probably the dtor
6.  Avoid virtuals in template classes
7.  Do not reorder or remove public members, or change access levels

2 means no STL or Boost types in function parameters. I’ll address 6 by avoiding templates in my API.

[This article](http://www.agner.org/optimize/calling_conventions.pdf) by [Agner Fog](http://www.agner.org) is a superb detailed survey of data sizes & alignments,  stack alignment, call conventions for register usage and parameter handling, name mangling schemes and object file formats inc COFF for all the major x86 & x64 OSes and C++ compilers. Strongly recommended.