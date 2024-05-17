<!--yml
category: 未分类
date: 2024-05-12 19:50:07
-->

# Still learning with R | Coding the markets

> 来源：[https://etrading.wordpress.com/2006/09/20/still-learning-with-r/#0001-01-01](https://etrading.wordpress.com/2006/09/20/still-learning-with-r/#0001-01-01)

## Still learning with R

### September 20, 2006

In all my R coding so far I’ve been referencing individual lists within a dataframe (trans: column in a table) with the frame$list syntax. Not very generic, especially when I’m trying to write a generic, multi dimensional bucketing function. So somewhat belatedly I’ve discovered the frame[[list]] syntax, which allows me to parameterise the column references I pass to my bucketing code. Phew!