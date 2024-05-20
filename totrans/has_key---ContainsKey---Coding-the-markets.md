<!--yml
category: 未分类
date: 2024-05-12 19:45:33
-->

# has_key & ContainsKey | Coding the markets

> 来源：[https://etrading.wordpress.com/2007/10/11/has_key-containskey/#0001-01-01](https://etrading.wordpress.com/2007/10/11/has_key-containskey/#0001-01-01)

## has_key & ContainsKey

### October 11, 2007

Python’s built in dictionary type – {} – has a has_key method. C#’s System.Collections.Hashtable has ContainsKey. I’d like the same Python code to operate on dictionaries and hashtables regardless. Fortunately IronPython adds the ContainsKey method to the built in dictionary type, so a simple replacement of has_key invocations with ContainsKey does the trick.