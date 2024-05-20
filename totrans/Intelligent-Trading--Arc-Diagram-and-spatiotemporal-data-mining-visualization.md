<!--yml
category: 未分类
date: 2024-05-18 04:44:37
-->

# Intelligent Trading: Arc Diagram and spatiotemporal data mining visualization

> 来源：[http://intelligenttradingtech.blogspot.com/2011/09/arc-diagram-and-spatiotemporal-data.html#0001-01-01](http://intelligenttradingtech.blogspot.com/2011/09/arc-diagram-and-spatiotemporal-data.html#0001-01-01)

I won't spend too much time discussing this fascinating topic other than to say it relates very much to prior discussions about pattern discovery via visual data mining (see lexical dispersion plots for example).  I happened across an interesting visualization method called the Arc Diagram, developed by Martin Wattenberg. Working for data visualization groups at IBM and later Google, he developed some interesting visual representations of spatiotemporal data.

Fig 1\. Arc Diagram and legend with example of discretized pattern archetype.

The resulting plot generates some fascinating temporal signatures, similar to what one might see in  phase-space portraits from chaos. However, they have been frequently utilized to look for spatiotemporal signatures in music.  One might discern a type of underlying order or visual signature of complexity as well as recurring patterns in sequential objects ranging from text based lyrical information to musical sheet notes.

 Figure 1 shows an example of how one might utilize this tool towards temporal pattern discovery in time series. A weekly series from SPY has been discretized into alphabet tokens, based upon the bin ranges in the included legend. The small chart in the example would decode an archetypal pattern for the following sequence: ECDCECCD, into a time series representation of the 8 week data symbol. The following interactive java tool from another blogger, Neoformix, was then used to translate the data into an Arc Diagram.  http://www.neoformix.com/Projects/DocumentArcDiagrams/index.html  .  Read from top to bottom, one can look at recurring and related patterns that are repeated over time; certain behavior might warrant further investigation.

You can copy the following data stream into the tool to toy around with the tool to get a feel for the possibilities of visual pattern discovery.*  I won't go into too much more detail about utilizing it, other than to say it appears to be a very useful tool in temporal based pattern discovery.

Please see the following for more ideas on arc diagrams and musical signatures:

http://www.research.ibm.com/visual/papers/arc-diagrams.pdf

http://turbulence.org/Works/song/mono.html

Blog mentioned:

http://www.neoformix.com/

* Not sure how to attach .xls file here, but if anyone wants a copy of the .xls file, you can send me an email and I'll try to get it out to you.  Otherwise, you can simply grab a song lyric off the web to play with the tool.