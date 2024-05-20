<!--yml
category: 未分类
date: 2024-05-12 19:52:37
-->

# Bloomberg: the trader’s intranet | Coding the markets

> 来源：[https://etrading.wordpress.com/2006/06/15/bloomberg-the-traders-intranet/#0001-01-01](https://etrading.wordpress.com/2006/06/15/bloomberg-the-traders-intranet/#0001-01-01)

## Bloomberg: the trader’s intranet

### June 15, 2006

I’ve [mentioned before](https://etrading.wordpress.com/2006/05/31/visualizing-the-markets/) how precious screen real estate is on the trading floor. One of the things traders alway have running is their [Bloomberg](http://www.bloomberg.com) terminal. Unlike us coders, they won’t have web, email and chat clients consuming that precious screen space. Bloomberg does email and chat anyway. Consequently, when a trader wants to publish some stuff to their colleagues on the floor, they’ll want to publish it on Bloomberg. That stuff may be some indicative quotes or valuations.

Alongside their Bloomberg, traders will always have Excel running. So we support their publication requirements with an [XLL](https://etrading.wordpress.com/excel/) that can send an Excel worksheet to a Bloomberg GPGX page. That’s a GPGX, not a GDCO, which is for executable quotes. One click of a button and the trader’s free formatted sheet is out there on Bloomberg. Result: happy trader.

One consequence of this is that as an org, we are ever more locked into those Bloomberg fees: a grand a month for a terminal.