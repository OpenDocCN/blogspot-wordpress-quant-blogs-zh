<!--yml
category: 未分类
date: 2024-05-12 19:54:09
-->

# Visualizing the markets | Coding the markets

> 来源：[https://etrading.wordpress.com/2006/05/31/visualizing-the-markets/#0001-01-01](https://etrading.wordpress.com/2006/05/31/visualizing-the-markets/#0001-01-01)

## Visualizing the markets

### May 31, 2006

[Matt](mdavey.wordpress.com "Matt") [posted recently](http://mdavey.wordpress.com/2006/05/25/vol-surface-visualization/) on visualization. I worked in the oil industry in the 90s, and did some [visualization work](http://www.slb.com/content/services/software/reseng/eclipse_pre_post/floviz.asp), and I've often wondered why visualization isn't used more often in finance. After all, it is used heavily in many other domains that deal with high volumes of numerical data. For instance, medicine, science and engineering, and oil and gas.

Here are some factors that I reckon prevent visualization adoption on the trading floor…

*   Real time data: the domains that adopt visualization are often analysing static data sets that are produced by scanners (medicine) or simulators (oil). Timeliness is critical in the markets. Traders need to keep up with a flow of real time data. Visualizing real time data presents quite specific coding challenges, since rendering a 3D scene is computationally expensive.
*   No obvious spatial metaphors: I suspect it's no accident that visualization has taken off in sectors that deal with real physical objects, like the human body, or an oil reservoir. The visual representation of such objects is straightforward. The question of "what 3D form do I give this" doesn't arise.
*   Precious screen real estate: walk around our trading floor and you'll see traders with 6 flat screens driven by two PCs. All that screen real state is consumed with [Bloomberg](http://www.bloomberg.com) terminals, pricing blotters, RFQ blotters, trade blotters and Excel spreadsheets. If a trader is going to give up some space to a new tool, it better deliver real value, and not just seem like a 'nice to have'.

However, the search for competitive edge is unceasing in the markets, and there's always someone willing to try out a new technique. Cantor have a [viz offering](http://www.cantordirect.com/dataprod/g3/index.htm) for US fixed income markets. 4D Trading were a start up that had a viz product. They found it difficult to sell, and were eventually acquired by [GLTrade](http://www.gltrade.com).

There are some niches in trading that do lend themselves naturally to viz techniques. I've seen Excel charting used for 3D plots of volatility surfaces. Derman has a [great explanation](http://www.ederman.com/new/docs/euronext-volatility_smile.pdf) of the implied volatility surface. A 3D plot of a vol surface that's been pulled out of a database of yesterday's closes can be a very handy sanity check for a trader coding his own pricing model in a spreadsheet.