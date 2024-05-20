<!--yml
category: 未分类
date: 2024-05-12 19:34:37
-->

# Early vs late binding | Coding the markets

> 来源：[https://etrading.wordpress.com/2012/01/29/early-vs-late-binding/#0001-01-01](https://etrading.wordpress.com/2012/01/29/early-vs-late-binding/#0001-01-01)

## Early vs late binding

### January 29, 2012

I agree with pretty much [everything Jeff has to say](http://blog.jvroom.com/2012/01/28/choosing-your-programming-language-the-inside-scoop/) on strongly typed, statically bound languages vs weakly typed late binding systems. But I don’t agree that we must decide in favour of the former. There is no one size fits all language, and I believe the right approach is to use a mix of early and late binding. Early binding when we want efficiency, compactness and speed. And late binding when we want expressiveness and rapid time to market. Electronic trading systems are a perfect example of a class of problem where we want all those contradictory virtues in the same system. A combination of languages is the only way to satisfy all those requirements. Brad Cox laid all this out this approach with great prescience in [Planning the Software Industrial Revolution](http://virtualschool.edu/cox/pub/PSIR/) in 1990\. What we need a development environments that allows us to mix languages at will. Debuggers that cope seamlessly when we examine a stack with different languages in different frames. Consistent threading models across runtimes. And consistent memory management models. Microsoft have come closest to achieving this with the .Net CLR. The Java VM can host multiple languages too, but not with the same quality tooling.

Personally I like the combination of C++ and Python. But there are tensions implicit in building systems with that mix. The first is the threading model. If you’re doing server engineering you mus be GIL aware. A single C++ thread works well with Python. A limited number of C++ threads on dedicated tasks, with just one of them invoking Python works well too. Multiple C++ threads as pooled workers using locking to cooperate in executing identical logic and each invoking Python will not work well.

Another tension is the different memory management models. The Python C runtime organises it’s own memory pool of PyObject* allocations. There are separate sub pools for different types, with different rules for the management of strings, integers and larger objects. Python’s memory pool tends to only grow, unlike a C++ program who’s memory profile we can see fall when the C RT lib hands memory back to the OS.

So if we have multiple languages in the same run time one of the biggest challenges is making the right architectural decisions so that those languages cooperate despite drawing on the same OS provided resources in different ways.