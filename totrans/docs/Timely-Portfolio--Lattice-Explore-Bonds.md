<!--yml
category: 未分类
date: 2024-05-18 15:09:52
-->

# Timely Portfolio: Lattice Explore Bonds

> 来源：[http://timelyportfolio.blogspot.com/2011/12/lattice-explore-bonds.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/12/lattice-explore-bonds.html#0001-01-01)

Since my fifth most popular post has been [Bond Market as a Casino Game Part 1](http://timelyportfolio.blogspot.com/2011/04/bond-market-as-casino-game-part-1.html), I thought I would use Vanguard Total US Bond Market mutual fund (VBMFX) monthly returns to build our skills in the lattice R package and help visualize the unbelievable run of U.S. bonds ([Calmar Ratio 1.37 over the past 20 years](Bonds%20Tumble%20and%20Questions%20Start%20Getting%20Asked)).

Although I have primarily graphed with R base graphics, PerformanceAnalytics charts, and ggplot, the lattice package provides an extremely powerful set of charting tools.

We can start with a basic qqplot of the entire set of monthly returns.

Then, we can group by year.

Or, we can also very easily split each year into its own panel.

Here is a little different look with a density plot.

Now let’s build boxplots and dotplots.

Add an annual dotplot to a boxplot for the entire period.

Or we can add a boxplot for each year.

See [http://timelyportfolio.blogspot.com/search/label/bonds](http://timelyportfolio.blogspot.com/search/label/bonds "http://timelyportfolio.blogspot.com/search/label/bonds") for all my posts on bonds.

[R code from GIST:](https://gist.github.com/1487949)