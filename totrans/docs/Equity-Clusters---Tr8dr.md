<!--yml
category: 未分类
date: 2024-05-18 15:35:30
-->

# Equity Clusters | Tr8dr

> 来源：[https://tr8dr.wordpress.com/2009/12/30/equity-clusters/#0001-01-01](https://tr8dr.wordpress.com/2009/12/30/equity-clusters/#0001-01-01)

December 30, 2009 · 8:32 pm

I am putting together some portfolios to be auto-traded using a dynamic portfolio asset allocation algo.   I had put together a maximum spanning tree (shown in a previous posting) to observe relationships between securities.

In this iteration have gone further:

1.  Heatmap colors to indicate average volatility levels for a given security relative to others
2.  Maximum spanning tree clusters to reveal which diversification group a given asset belongs to
3.  Edge thickness indicates strength of relationship

I am interested in both the diversity and the volatility profile of the asset pool.   I will pick the majority of assets from the set with mid-range volatility (oranges), as opposed to low vol (reds), and high vol (yellows).    Classifying the asset set into clusters based on correlations provides an automated way of observing the diversification group the asset belongs to.

**Algorithm**
The algorithm is loosely as follows:

1.  calculate lower-triangular correlation matrix of returns for, say, s&p 500 stocks
2.  sort in descending order by correlation
3.  set up graph structure
4.  loop through correlations selecting pairs of assets
    1.  if neither in graph add as new cluster pair
    2.  if one in graph and other not, attach new to existing
    3.  if both in graph but size of clusters < min cluster size, merge clusters
5.  repeat until all assets accounted for **and** all clusters have size >= min cluster size
6.  annotate & plot

**Clusters (daily returns)**
Here are the clusters the algorithm produced:

Of course this can be applied to any asset set.  Thought is a useful visualization, though there are many other dimensions of interest.