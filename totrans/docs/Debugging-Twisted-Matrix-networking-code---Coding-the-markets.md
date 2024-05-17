<!--yml
category: 未分类
date: 2024-05-12 19:36:08
-->

# Debugging Twisted Matrix networking code | Coding the markets

> 来源：[https://etrading.wordpress.com/2011/01/24/debugging-twisted-matrix-networking-code/#0001-01-01](https://etrading.wordpress.com/2011/01/24/debugging-twisted-matrix-networking-code/#0001-01-01)

## Debugging Twisted Matrix networking code

### January 24, 2011

Debugging Twisted code is an exercise in lateral thinking. The error messages and exceptions can be opaque, especially when code wrapped inside a Deferred fails. When you get an unhandled error inside a Deferred, check your code for basic errors: parameter mismatches, references to undefined variables, or unimported types or modules etc. And where you’re deriving from a Twisted base class, check that you’re not accidently overriding a member variable. For instance, don’t have a member variable called ‘clients’ !