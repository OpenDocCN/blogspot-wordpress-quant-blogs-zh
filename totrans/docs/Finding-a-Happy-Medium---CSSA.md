<!--yml
category: 未分类
date: 2024-05-12 18:06:59
-->

# Finding a Happy Medium | CSSA

> 来源：[https://cssanalytics.wordpress.com/2012/02/15/finding-a-happy-medium/#0001-01-01](https://cssanalytics.wordpress.com/2012/02/15/finding-a-happy-medium/#0001-01-01)

One of the most important measures in finance is the notion of a central tendency. This is used in some form in both statistical applications and also in technical indicators. The most basic example is the mean– or the simple average of a set of data points. Other measures include the median– the middle or estimated middle value of the data set. There are those that like to debate the merits of each of the above measures, and of course those not mentioned. Personally, I think there is more value from looking at them all together in a blended fashion. Here is a way to calculate a central value that has a nice blend of the characteristics of each measure and tends to perform well on time series data:

Happy Medium= (average/mean, median, (max+min)/2, (95th percentile+5th percentile)/2)/4

This measure is more resistant to distributions of different shapes and also strange outliers in the data. It is not perfect, but it tends to strike a good balance without having to resort to complex statistical methods. One could also blend in the interquantile or interquartile range as well (average of 80th and 20th percentile and 75th and 25th percentile).
Also it is valuable to take these measures at different levels of fracticality– or perhaps just use mutliple time interval measurements within the sample length. In this case that might mean days, weeks etc.