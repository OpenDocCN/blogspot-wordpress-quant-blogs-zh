<!--yml
category: 未分类
date: 2024-05-12 19:51:32
-->

# The power of R, pt I | Coding the markets

> 来源：[https://etrading.wordpress.com/2006/08/01/the-power-of-r-pt-i/#0001-01-01](https://etrading.wordpress.com/2006/08/01/the-power-of-r-pt-i/#0001-01-01)

A small illustration culled from the R intro…

# 30 elements in each array..
# ..a salary and an Aussie state
incomes <- c(60, 49, 40, 61, 64, 60,
  59, 54, 62, 69, 70, 42, 56,
  61, 61, 61, 58, 51, 48, 65,
  49, 49, 41, 48, 52, 46, 59, 46, 58, 43)
state <- c(“tas”, “sa”,  “qld”, “nsw”,
  “nsw”, “nt”,  “wa”,  “wa”,  “qld”,
  “vic”, “nsw”, “vic”, “qld”, “qld”,
  “sa”,  “tas”, “sa”,  “nt”,  “wa”, 
  “vic”, “qld”, “nsw”, “nsw”, “wa”, 
  “sa”,  “act”, “nsw”, “vic”, “vic”, “act”)

# Categorise the states and categorise the incomes
# into buckets using cut(). Then use table() to
# generate a table of counts for each category
# combination…
statef <- factor( state)
incomef <- factor( cut( incomes, breaks = 35 + 10*(0:7)))
table( incomef, statef)

 statef
incomef   act nsw nt qld sa tas vic wa
  (35,45]   1   1  0   1  0   0   1  0
  (45,55]   1   1  1   1  2   0   1  3
  (55,65]   0   3  1   3  2   2   2  1
  (65,75]   0   1  0   0  0   0   1  0