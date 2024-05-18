<!--yml
category: 未分类
date: 2024-05-18 14:20:11
-->

# HFT: The Missing Data – Sniper In Mahwah & friends

> 来源：[https://sniperinmahwah.wordpress.com/2014/09/19/hft-the-missing-data/#0001-01-01](https://sniperinmahwah.wordpress.com/2014/09/19/hft-the-missing-data/#0001-01-01)

In April 2013 I visited the Trade Tech Europe event in London – it was my first immersion in the technical world of high-frequency trading (HFT). I collected some copies of [*Best Execution*](http://www.bestexecution.net) and because I am interested by the space-time issues of the market microstructure – for example: how orders are routed between the different lit exchanges/dark pools/crossing networks located in different places – I have found this [paper](http://www.bestexecution.net/viewpoint-darren-toulson-2/) quite absorbing.

Then I have learnt one thing : exchanges are not time synchronized. That means the matching engine of  NYSE is not time synchronized with the BZX matching engine, the matching engine of EDGX is not time synchronized with the Nasdaq matching engine, and so on, and that is problematic: without synchronization – in the HFT world microseconds count – it’s impossible to exactly know how and when an order was filled (here or there), which kind of order type was used, etc. So both academics and investors don’t have precise data. Data is missing.

In this previous [post](https://sniperinmahwah.wordpress.com/2014/01/13/about-timestamps-and-exchanges/) I talked about a proposition McKay Brothers co-CEO Stéphane Tyč made in Paris, in December 2013\. In short, the proposal was:

*Exchanges produce timestamps at the most important times of the matching cycle. They also identify every matched trade with a unique number. The regulators could define standards for this information and impose the end of day publication of the raw data from the exchanges. Every matched trade should have attached :*
*– the timestamp of the order that triggered the trade at the time of entry in the matching engine.*
*– the timestamp of the publication of trade in the publicly available data stream*
*– the anonymous trade id number.*
*All timestamps should be accurate to 1µs of the atomic time, which is readily available with PTP (Precision Time Protocol). This way, all the issues of synchronicity could be studied very precisely.*
*This should be made available in the raw market format at the end of each day. A simple code to read this data should be provided under an open source license.*
*Based on this information, any client of a broker could receive the collection of trade id numbers that constituted his execution and could go and find for himself if the execution was to his standards.*
*Open data, open formats, open source code, those would help further the debate [my emphasizing] and enable research to shed light on this very challenging problem.*

The amazing fact was after I published this post, I received a mail from the Autorité des Marchés Financiers (AMF, the French SEC) saying that they were working on the synchronization issues and they would have been happy to meet me in order to have my opinion on the topic. It was a little fun to see that a regulator was interested by my point of view, but I didn’t have a lot of things to say, even if I met the AMF people involved in these issues and told them to speak with Stéphane Tyč. They did and with the help of Stéphane they refined the proposition (about timestamps synchronization) they have sent to the European regulator ESMA. I was only a go-between, and I’m still a go-between here.

Since I know Stéphane quite well now (he helped me to understand the world of microwave networks used by some HFT players), he kindly asked me to read and comment a white paper he was working on about best execution, the time synchronization of exchanges, etc. I can’t define myself as a true specialist but I think what Stéphane Tyč proposes is a very interesting way to level the playing field. Here is the white paper:

[![A technological solution to best execution and excessive market complexity](img/35320cd864df42c92030b936c2c503cf.png)](http://www.quincy-data.com/wp-content/uploads/2014/09/Atechsolutiontobestexec.pdf)