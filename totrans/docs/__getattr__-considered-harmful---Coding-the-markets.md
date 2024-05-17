<!--yml
category: 未分类
date: 2024-05-12 19:35:25
-->

# __getattr__ considered harmful | Coding the markets

> 来源：[https://etrading.wordpress.com/2011/03/08/__getattr__-considered-harmful/#0001-01-01](https://etrading.wordpress.com/2011/03/08/__getattr__-considered-harmful/#0001-01-01)

## __getattr__ considered harmful

### March 8, 2011

Today’s coding reminded me why avoid __getattr__ in Python. FYI, a class that implements a __getattr__ method overrides the member access operator “.”  So simply referencing object.member invokes object.__getattr__( member). A typical debugging technique in Python is to litter code with print object.member. Guess what happens if you use that debugging technique inside a __getattr__ method ?  Like, duh ?!  😉