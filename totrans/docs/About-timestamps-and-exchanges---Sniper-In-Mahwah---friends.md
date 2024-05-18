<!--yml
category: 未分类
date: 2024-05-18 14:23:48
-->

# About timestamps and exchanges – Sniper In Mahwah & friends

> 来源：[https://sniperinmahwah.wordpress.com/2014/01/13/about-timestamps-and-exchanges/#0001-01-01](https://sniperinmahwah.wordpress.com/2014/01/13/about-timestamps-and-exchanges/#0001-01-01)

Here is the whole proposition made by [McKay Brothers](http://www.mckay-brothers.com)‘ Stéphane Tyc at the Institut Louis Bachelier in Paris, about best execution, timestamps and exchanges (in this previous [post](https://sniperinmahwah.wordpress.com/2013/12/23/high-frequency-trading-liquidity-and-stability/) I only summarized his speech):

“The definition of best execution is fiendishly difficult. There are many approaches to the issue. In typical fashion the USA defines precisely what needs to be reported and also defines the mechanisms of order protection on various trading venues. On the other side of the Atlantic, the EU imparts on the Brokers an obligation to take “all reasonable steps to obtain, when executing orders on behalf of clients, the best possible result”. The challenge of “best execution” does not have a known solution, and the proliferation of order types makes the quest for a perfect solution unrealistic. The real time aspect of the problem makes it particularly intractable.There is, however, a possibility which could shed light on the best execution riddle. Exchanges produce timestamps at the most important times of the matching cycle. They also identify every matched trade with a unique number. The regulators could define standards for this information and impose the end of day publication of the raw data from the exchanges. Every matched trade should have attached :

– the timestamp of the order that triggered the trade at the time of entry in the matching engine.
– the timestamp of the publication of trade in the publicly available data stream
– the anonymous trade id number.

All timestamps should be accurate to 1µs of the atomic time, which is readily available with PTP (Precision Time Protocol). This way, all the issues of synchronicity could be studied very precisely.

This should be made available in the raw market format at the end of each day. A simple code to read this data should be provided under an open source license.

The incremental costs imposed on the industry would be very limited and the benefits for transparency very high. All dark pools, broker crossing networks and other alternative non public execution venues should also be required to publish their trades with the same mechanism.

Based on this information, any client of a broker could receive the collection of trade id numbers that constituted his execution and could go and find for himself if the execution was to his standards.

Open data, open formats, open source code, those would help further the debate and enable research to shed light on this very challenging problem.”