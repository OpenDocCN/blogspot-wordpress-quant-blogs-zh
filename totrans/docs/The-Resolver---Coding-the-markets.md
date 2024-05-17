<!--yml
category: 未分类
date: 2024-05-12 19:44:18
-->

# The Resolver | Coding the markets

> 来源：[https://etrading.wordpress.com/2008/02/01/the-resolver/#0001-01-01](https://etrading.wordpress.com/2008/02/01/the-resolver/#0001-01-01)

## The Resolver

### February 1, 2008

So I’ve had a little play with [Resolver One](http://www.resolversystems.com/), now that it’s out of beta and at 1.0\. To give a somewhat simplistic view, it’s an Excel clone implemented in IronPython. Where it scores big over Excel is in exposing its internals, specifically the calc model and worksheet in one seamless view. In Excel, we have several different APIs for injecting our own logic into a spreadsheet: Excel’s own internal C API for coding XLLs, VBA and COM. Those APIs allow us to express worksheet functionality in C, VB and any COM language. Resolver gives us one seamless view of its internals in our favourite programming language: Python. Simple example [here](http://www.resolversystems.com/documentation/index.php/The_Auto-Total).

This is attractive for those of us already using Python for front office systems. I’m not sure how much it will appeal to others though…