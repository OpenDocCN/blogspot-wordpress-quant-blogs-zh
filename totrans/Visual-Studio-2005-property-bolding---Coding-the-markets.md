<!--yml
category: 未分类
date: 2024-05-12 19:38:45
-->

# Visual Studio 2005 property bolding | Coding the markets

> 来源：[https://etrading.wordpress.com/2009/10/05/visual-studio-2005-property-bolding/#0001-01-01](https://etrading.wordpress.com/2009/10/05/visual-studio-2005-property-bolding/#0001-01-01)

## Visual Studio 2005 property bolding

### October 5, 2009

VS dev trivia: if entries in your C++ project property pages show up as bold it means they have been given explicit overrides in the .vcproj XML. This broke my build today as the overrides stopped inherited values from .rules and .vsprops files being pulled in.