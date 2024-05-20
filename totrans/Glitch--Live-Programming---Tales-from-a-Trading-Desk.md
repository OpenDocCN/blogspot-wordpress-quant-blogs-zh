<!--yml
category: 未分类
date: 2024-05-18 06:00:26
-->

# Glitch: Live Programming | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2013/10/01/glitch-live-programming/#0001-01-01](https://mdavey.wordpress.com/2013/10/01/glitch-live-programming/#0001-01-01)

## Glitch: Live Programming

Interesting read from Microsoft Research on Live [Programming](http://research.microsoft.com/pubs/201333/rem13.pdf),  As referenced by the paper, [Bret](http://worrydream.com/) Victor’s work has thankfully been considered.  Now all we have to do is wait n years, and maybe Glitch will see the light of day in Visual Studio.

> Input changes are often handled by reactive and incremental constructs that are tedious to use or inexpressive, while changes to program code are typically not handled at all during execution, complicating support for “live programming.” We propose that change in code and input should be managed automatically, similar to how garbage collection eliminates memory management as an explicit programmer concern. Our programming model, Glitch, realizes such managed time by progressively re-executing nodes of program execution when they become inconsistent due input/code state changes. Unlike many reactive models, Glitch supports expressive shared-state procedural programming, but with one caveat: operations on shared state must be undoable and commutative to ensure re-execution efﬁciency and eventual consistency. Still, complex programs like compilers can be written in Glitch using mundane programming styles.

~ by mdavey on October 1, 2013.

Posted in [Languages](https://mdavey.wordpress.com/category/languages/)