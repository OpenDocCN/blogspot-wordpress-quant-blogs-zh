<!--yml
category: 未分类
date: 2024-05-18 15:00:17
-->

# Timely Portfolio: Banging on the JGBs

> 来源：[http://timelyportfolio.blogspot.com/2013/04/banging-on-jgbs.html#0001-01-01](http://timelyportfolio.blogspot.com/2013/04/banging-on-jgbs.html#0001-01-01)

Since I have not posted in quite a while, I wanted to let everyone know that I am still alive and kicking.  The resurrection of excitement (opportunity) in the markets, quarterly reporting cycle, and the overwhelming number of unbelievable R/javascript releases have kept me from writing something good enough to justify a post.   In the markets, Japan and gold bring a smile to my face.    Nothing particularly new on the quarterly reporting cycle, but I have been watching the interesting ideas at [http://axysreporting.com](http://axysreporting.com) closely, and I have enjoyed learning a little about [http://addepar.com](http://addepar.com).  Nothing though impresses me as much as all of the R and javascript packages that have been announced over the last two weeks.  I mentioned them in my post [d3 Lifeline from vega and clickme](http://timelyportfolio.blogspot.com/2013/04/d3-lifeline-from-vega-and-clickme.html), but I forgot to include [Introducing the healthvis R package – one line D3 graphics with R](http://simplystatistics.org/2013/04/02/introducing-the-healthvis-r-package-one-line-d3-graphics-with-r/) from Jeff Leek who taught [https://www.coursera.org/course/dataanalysis](https://www.coursera.org/course/dataanalysis), and [rCharts](http://ramnathv.github.io/rcharts) was not yet released.  [rCharts](http://ramnathv.github.io/rcharts) reminded me of the very special [slidify](http://ramnathv.github.io/slidify) package that I have to my own detriment not used until now.  I **strongly, strongly recommend readers** to thoroughly look at  [**rCharts**](http://ramnathv.github.io/rcharts)**and** [**slidify**](http://ramnathv.github.io/slidify).  Just to make sure everyone sees all of these, I have relisted them and added new links below with the Twitter announcements.

> [vega](http://trifacta.github.io/vega)
> 
> Announcing Vega, a new visualization grammar built on [#d3js](https://twitter.com/search/%23d3js)! Design reusable chart components in a JSON format [trifacta.github.com/vega](http://t.co/GuNbXu3jtv "http://trifacta.github.com/vega")
> 
> — Jeffrey Heer (@jeffrey_heer) [April 2, 2013](https://twitter.com/jeffrey_heer/status/319109814926073857)
> 
> [rCharts](http://ramnathv.github.io/rcharts) from the same creator as [slidify](http://ramnathv.github.io/slidify/)
> 
> @[lisaczhang](https://twitter.com/lisaczhang) I wrote an R package wrapping functionality of Polycharts for R users. [ramnathv.github.io/rCharts](http://t.co/1Pcyp6E8wL "http://ramnathv.github.io/rCharts")
> 
> — Ramnath Vaidyanathan (@ramnath_vaidya) [April 10, 2013](https://twitter.com/ramnath_vaidya/status/322127777669201920)
> 
> [clickme](http://github.com/nachocab/clickme)
> 
> @[xieyihui](https://twitter.com/xieyihui) I'd love your feedback on clickme, an R package to populate JS visualizations using [#knitr](https://twitter.com/search/%23knitr) [bitly.com/vizbi_clickme](http://t.co/zazjjM3tDo "http://bitly.com/vizbi_clickme")
> 
> — Nacho Caballero (@nachocaballero) [March 24, 2013](https://twitter.com/nachocaballero/status/315652318123139072)
> 
> rhealthvis
> 
> Our package is announced today! [healthvis.org](http://t.co/iItsC0Snlh "http://healthvis.org")
> 
> — rhealthvis (@rhealthvis) [April 2, 2013](https://twitter.com/rhealthvis/status/319096283711291392)

Now to show some of the results from my experiments, I will list some bl.ocks below.  The primary data source for all of these has been the Japanese Government Bond (JGB) yield data provided by the [Japanese Ministry of Finance](http://www.mof.go.jp/english/jgbs/reference/index.html).  I will discuss the reasons for choosing JGBs in a much more thorough later post.  I would love thoughts on JGBs and my experiments.

1.  [http://bl.ocks.org/timelyportfolio/5407807](http://bl.ocks.org/timelyportfolio/5407807)  JGB Yields in Small Multiples with clickme ractive
2.  [http://bl.ocks.org/timelyportfolio/5405240](http://bl.ocks.org/timelyportfolio/5405240)  JGB Yield Curve with a vega spec and clickme ractive
3.  [http://bl.ocks.org/timelyportfolio/5398614](http://bl.ocks.org/timelyportfolio/5398614)  JGB Yields Line Chart with a vega spec and clickme ractive

Some of my other more basic experiments are here.  These might be helpful to anyone not yet familiar with these new resources.

1.  [http://bl.ocks.org/timelyportfolio/5351448](http://bl.ocks.org/timelyportfolio/5351448)
2.  [http://bl.ocks.org/timelyportfolio/5342818](http://bl.ocks.org/timelyportfolio/5342818)
3.  [http://bl.ocks.org/timelyportfolio/5322390](http://bl.ocks.org/timelyportfolio/5322390)
4.  [http://bl.ocks.org/timelyportfolio/5316682](http://bl.ocks.org/timelyportfolio/5316682)

I’ll be back soon with what I hope is a very impressive [slidify](http://ramnathv.github.io/slidify) created market-related post.  Until then, please let me know what you think, or show your relevant experiments.

Thanks to everyone that has worked so hard creating these great open source projects.