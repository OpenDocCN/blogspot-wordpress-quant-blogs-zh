<!--yml
category: 未分类
date: 2024-05-12 19:35:57
-->

# LMAX conference | Coding the markets

> 来源：[https://etrading.wordpress.com/2011/01/28/lmax-conference/#0001-01-01](https://etrading.wordpress.com/2011/01/28/lmax-conference/#0001-01-01)

## LMAX conference

### January 28, 2011

So I’ve signed myself for the [LMAX UCL algo trading conference](http://community.lmaxtrader.com/conversations/topics/lmax-and-ucls-computer-science-department-host-conference-algorithmic-trading) – see you there !  I’m looking forward to Martin Thompson’s talk, and hoping I can bend his ear on a few server engineering questions over drinks at the end of the afternoon. I’m also keen to know more about the LMAX market design. In the [infoq presentation](http://www.infoq.com/presentations/LMAX) I linked earlier there are some intriguing comments about ensuring low and stable latency for market makers. This makes me wonder what the terms are for market maker participation on the LMAX order books. Do market makers have a different API than market takers ? Do makers get processing priority for placing, pulling and amending orders ? Can maker orders cross with other maker orders, or only market taker orders ?