<!--yml
category: 未分类
date: 2024-05-18 15:40:23
-->

# Evolution of Distribution | Tr8dr

> 来源：[https://tr8dr.wordpress.com/2008/01/20/evolution-of-distribution/#0001-01-01](https://tr8dr.wordpress.com/2008/01/20/evolution-of-distribution/#0001-01-01)

January 20, 2008 · 8:41 am

For a number of problems, understanding the evolution of the distribution over time is important. The distribution tends to be stable over longer periods and unstable over shorter periods.

The distribution is going to be measured from a sample over some time period. One may want to take a blend of distributions measured over different time periods, combined as basis functions with weights summing to 1.

The interesting bit is predicting the distribution forward with some statistical accuracy. The order book and momentum indicators should tell us something about how the distribution is going to transform over the next period or based on when a certain price level is achieved.

We are going to use a GA to calibrate the transformation function against historical data. There are many different functions we could use, so we use a GP approach to play with the permutations.