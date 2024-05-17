<!--yml
category: 未分类
date: 2024-05-18 04:43:53
-->

# Intelligent Trading: IBS Reversion (Stingray Plot) Intuition using R vioplot Package

> 来源：[http://intelligenttradingtech.blogspot.com/2013/04/ibs-stingray-reversion-intuition-using.html#0001-01-01](http://intelligenttradingtech.blogspot.com/2013/04/ibs-stingray-reversion-intuition-using.html#0001-01-01)

Fig 1\. Vioplot  of IBS filtered next day returns on SPY.

                 Fig 2\. Table of Summary of Results for rtn.tom vs. IBS.class (H,L,M)  

     A colleague and I were recently discussing ways to get intuition about the

[IBS classification method](http://intelligenttradingtech.blogspot.com/2013/01/ibs-reversion-edge-with-quantshare.html)

for reversion systems.  I thought I'd share a

[violin plot](http://cran.r-project.org/web/packages/vioplot/index.html)

I generated that might help to get some visual intuition about it. We can download and process next day returns for an asset like SPY and group classes into LOW (IBS < 0.2), HIGH(IBS > 0.8), and MID(all others). One thing you can see in the plots is the pronounced right skew in the LOW class, and left skew in the HIGH class (they sort of resemble opposing stingrays -- stingray plots might be a more apt term for the reversion phenomena); while the MID class tends to be more symmetrical. The nice thing about the vioplot visualization is that it includes the density shape of the return distribution, which adds intuition over more common box and whisker plots.