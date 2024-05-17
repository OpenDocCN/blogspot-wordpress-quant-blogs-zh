<!--yml
category: 未分类
date: 2024-05-12 18:34:45
-->

# Livermore Active Issues Index for Friday, Mar 5th | CSSA

> 来源：[https://cssanalytics.wordpress.com/2010/03/05/livermore-active-issues-index-for-friday-mar-5th/#0001-01-01](https://cssanalytics.wordpress.com/2010/03/05/livermore-active-issues-index-for-friday-mar-5th/#0001-01-01)

March 8, 2010 1:29 pm

David,

in your last post, if you use ROC of moving average results seems to be better

Reason – ROC of 5 day is prone to sudden variation of volume ,but MA 5 day is much smoother.
Whats your thought

here is my code

// Set system variables
AvgVol5 = MA(V, 5);
MA200 = MA(C, 200);

//5dROC SPY volume >0, V 0 AND V 0 AND V < Ref(V,-1);

Sell = 0;
Short=0;
Cover=0;