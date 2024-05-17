<!--yml
category: 未分类
date: 2024-05-18 04:44:49
-->

# Intelligent Trading: Simulating Win/Loss streaks with R rle function

> 来源：[http://intelligenttradingtech.blogspot.com/2011/05/simulating-winloss-streaks-with-r-rle.html#0001-01-01](http://intelligenttradingtech.blogspot.com/2011/05/simulating-winloss-streaks-with-r-rle.html#0001-01-01)

The following script allows you to simulate sample runs of Win, Loss, Breakeven streaks based on a random distribution, using the run length encoding function, rle in R. Associated probabilities are entered as a vector argument in the sample function.

You can view the actual sequence of trials (and consequent streaks) by looking at the trades result.  maxrun returns a vector of maximum number of Win, Loss, Breakeven streaks for each sample run. And lastly, the prop table gives a table of proportion of run transition pairs from losing streak of length n to streak of all alternate lengths.

Example output (max run length of losses was 8 here):

100*prop.table(tt)

    lt.2

lt.1      1      2      3      4      5      6      7      8

   1 41.758 14.298  5.334  1.662  0.875  0.131  0.000  0.044

   2 14.692  4.897  1.924  0.787  0.394  0.087  0.131  0.000

   3  4.985  2.405  0.525  0.350  0.000  0.000  0.044  0.000

   4  1.662  0.875  0.306  0.087  0.000  0.000  0.000  0.000

   5  0.831  0.219  0.175  0.000  0.000  0.044  0.000  0.000

   6  0.087  0.131  0.044  0.000  0.000  0.000  0.000  0.000

   7  0.087  0.087  0.000  0.000  0.000  0.000  0.000  0.000

   8  0.044  0.000  0.000  0.000  0.000  0.000  0.000  0.000

maxrun

 B  L  W

 3  8 17

-----------------------------------------------------------------------------------------

#generate simulations of win/loss streaks use rle function

trades<-sample(c("W","L","B"),10000,prob=c('.6','.35','.05'),replace=TRUE)

traderuns<-rle(trades)

tr.val<-traderuns$values

tr.len<-traderuns$lengths

maxrun<-tapply(tr.len,tr.val,max)

#streaks of losing trades

lt<-tr.len[which(tr.val=='L')]

lt.1<-lt[1:(length(lt)-1)]

lt.2<-lt[2:(length(lt))]

#simple table of losing trade run streak(n) frequencies

table(lt)

#generate joint ensemble table streak(n) vs streak(n+1)

tt<-table(lt.1,lt.2)

#convert to proportions

options(digits=2)

100*prop.table(tt)

maxrun