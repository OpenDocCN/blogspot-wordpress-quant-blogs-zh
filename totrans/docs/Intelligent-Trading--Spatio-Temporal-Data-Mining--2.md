<!--yml
category: 未分类
date: 2024-05-18 04:44:33
-->

# Intelligent Trading: Spatio-Temporal Data Mining: 2

> 来源：[http://intelligenttradingtech.blogspot.com/2011/10/spatiotemporal-data-mining-2.html#0001-01-01](http://intelligenttradingtech.blogspot.com/2011/10/spatiotemporal-data-mining-2.html#0001-01-01)

There are many visual methods used to identify patterns in space and time. I've discussed some in prior threads and will show a few others briefly here. One of the most difficult questions I often hear from others regarding markov type approaches, is how to identify states to be processed.

It is a similar problem that one encounters using simple linear type factor analysis. Unfortunately, there is no simple answer; however, because data streams are becoming so vast it becomes almost impossible to enumerate over all possible state sets. Visual mining techniques can be incredibly helpful in narrowing down that space as well as feature reduction.  I often use these types of visualizations back and forth with unsupervised classification type learners to converge on useful state identifications.

                                       Fig 1\. Spatio-Temporal State plot

Figure 1 gives an idea on visualizing states with respect to time. But having such knowledge in isolation doesn't give us much use. We are more interested in looking for Bayesian type relationships between states that give some probabilities between linked states in time.

                                              Fig 2\. Fluctuation Plot

Several visual methods exist to capture the relationships visually. One common plot used in language processing and information theory, is a fluctuation plot. The above plot was built using the same state data as the first graph. It is often used to determine conditional relationships between symbols such as alphabet tokens. The size of each box is directly proportional to the weight of the transition probabilities between row and column states in tabular data. An example would be to think of the letters yzy more commonly followed by g (as in syzygy) than any other state token; thus, one would expect to quickly spot a larger box across a row of states representing the 'yzy' row token n-gram and 'g' column token .

Both plots were produced in R.  ggflucuation() is a plot command utilized from ggplot2.  I am currently investigating how much easier and faster it might be to process such visualizations in tools like protovis and processing.  I've been especially inspired by reading some of Nathan Yau's excellent visualization work in his book, 'Visualize This.' I included it in the link to the right for interested readers.