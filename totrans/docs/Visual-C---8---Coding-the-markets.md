<!--yml
category: 未分类
date: 2024-05-12 19:48:25
-->

# Visual C++ 8 | Coding the markets

> 来源：[https://etrading.wordpress.com/2007/02/07/visual-c-8/#0001-01-01](https://etrading.wordpress.com/2007/02/07/visual-c-8/#0001-01-01)

## Visual C++ 8

### February 7, 2007

We’re in the process of moving our 600KLOC codebase from VC6 to VC8, so I moved my current development project to VC8\. After the usual snafus getting a working build I finally have a binary that I can build, run & debug in the IDE and at the command line. Getting a binary that links is always a struggle in a new environment, especially if the ground is moving under your feet with new versions of STLport, Boost and others. So I was relieved when the link finally came up with zero unresolved externals, and I could start to explore the most important part on an IDE: the debugger. It’s nice. The tabbed debug windows for browsing variables, threads, callstack work nicely. And you can click on a variable and pop up a view – very handy for those long strings that got truncated in the old VC6 debugger window.