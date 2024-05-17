<!--yml
category: 未分类
date: 2024-05-18 05:04:14
-->

# Magmasystems Blog: KDB Consulting Redux

> 来源：[http://magmasystems.blogspot.com/2008/01/kdb-consulting-redux.html#0001-01-01](http://magmasystems.blogspot.com/2008/01/kdb-consulting-redux.html#0001-01-01)

I have gotten some private emails from people over the past few weeks who have been intrigued about my posts about KDB+, and wanting to know how to be a KDB+ consultant. It may be easier to apply to medical school and become a heart surgeon than it is to bootstrap yourself in a KDB consulting career.

I certainly do not hold myself out as a career counselor. You should not look to me as the key to future riches. All I do is observe the marketplace. I deal alot in hiring people for our own needs, and I get a lot of calls from recruiters. I have a lot of colleagues on Wall Street and in The City. So I am able to gather a lot of different data points, some of which I share on this blog.

Google everything you can about KDB+. Apply to KX Systems for access to the coding areas. Grab a copy of "Q for Mortals" by Jeff Borror. Find the pockets of KDB people in your company and get them to explain their source code for you.

If you have gotten this far....

You will need to get a copy of KDB+, which is not easy to get. Most likely, you cannot go onto LimeWire or Kazaa and find a copy of KDB floating around. Even if you did, you need to find a license key.

You need to go [here](http://www.kx.com/developers/software.php), and think about how you will convince Niall Dalton or Simon Garland to let you play around with KDB. Or, wait for the next SIFMA conference, find the KDB booth, and offer to take the KDB guys to the lounge at the Hilton. Or, come up with a product that might compliment KDB (like Panopticon did) and try to show Simon that it will increase the popularity of KDB. Maybe an English-to-Q translator? Maybe a true ODBC driver for KDB? Maybe a Q code obsfuscator?

Another avenue is try to approach First Derivatives. They are the primary partner for KX Systems, and the Yin to KX Systems' Yang. Hint .. they love Guiness.

Lest you think that I am picking on KDB ... the same thing can apply to any niche product. I suppose that you would not be able to wake up one day and decide that you will be a Vhayu consultant. In order to specialize in any kind of niche product, you need to leverage the existing resources for that product. This is one of the advantages of being employees of large financial firms or large consulting firms that specialize in financial services.

You need to get yourself into the proper mindset to deal with KDB. It is a very spartan product, hand-tuned and lightning fast at processing real-time flows of tick and order data. The actual Q.exe engine is about a 150K file. You do not get any of the nice, cushy bloat that you have with something like SQL Server and Oracle. Working with KDB brings you back to the days when you were writing DOS TSRs using good old INT 21H (for those of you born after 1980, a TSR is a Terminate and Stay Resident program .... and DOS was an ancient operating system that made Microsoft lots of money).

As if you are not convinced already .... the following code is from a Q file called holiday.q. Once you understand this code, send email to Niall or Simon of KX Systems, or to the people at First Derivatives, and show them that you can write this stuff without even looking (and this is mild ... wait until you get into the juicy stuff).

 `/day:(day;year)
dy:{"D"$string[y],x}

/residue
r:{y-x*y div x}

/adjust sat/sun
a:{d+0^(x,1)r[7]d:dy[y]z}

/goto dayofweek
b:{d+r[7]x-d:dy[y]z}

/good friday(1900-2099)
g:{d+:e:r[7](6*d:r[30]24+19*a:r[19]x)+5+2*r[4;x]+2*r[7]x;dy["0320";x]+d-7*(d=35)(d=34)&(e=6)&a>10}

/nyse holidays
nyse:(a[2]"0101";b[2]"0115";b[2]"0215";g;b[2]"0525";a[-1]"0704";b[2]"0901";b[5]"1122";a[-1]"1225")

nyse@/:\:2007 2008`  
©2008 Marc Adler - All Rights Reserved