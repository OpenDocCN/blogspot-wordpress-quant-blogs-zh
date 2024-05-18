<!--yml
category: 未分类
date: 2024-05-18 14:12:23
-->

# HFT in the Banana Land – Sniper In Mahwah & friends

> 来源：[https://sniperinmahwah.wordpress.com/2016/01/26/hft-in-the-banana-land/#0001-01-01](https://sniperinmahwah.wordpress.com/2016/01/26/hft-in-the-banana-land/#0001-01-01)

###### *It’s beautiful outside*
*Looks like it’s raining money*
Dr. Dre*, For the love of money*

[Updated 1 on 01/27/2016 | Minor corrections + kmz [file](http://www.zones-sensibles.org/wp-content/uploads/2016/01/Vigilant-2016.kmz_.zip) added]

[Updated 2 on 01/27/2016 | This post was written before Vigilant submitted a real planning application, so I didn’t see it. It’s [there](https://planning.dover.gov.uk/online-applications/applicationDetails.do?activeTab=documents&keyVal=DCAPR_228292) – but nothing new though]

First of all, Happy New Year.

On January 4, 2016, I was checking the comments made on this blog and I realized one of them was just a link to a [website](http://www.richboroughmast.co.uk) detailing how Vigilant Global is seeking to build a mast in the Richborough (UK) in order to complete a microwave network between Frankfurt and London. As the news were impressive, I tweeted the link at the speed of light, and the event was covered by the [*Wall Stret Journal*](http://www.wsj.com/articles/high-speed-trader-drw-proposes-thousand-foot-plus-u-k-tower-1451937343) and even by [Matt Levine](http://www.bloombergview.com/articles/2016-01-05/a-tower-a-shoebox-and-a-maserati). I told a journalist once, “*I don’t want to appear as the ‘expert’ of the HFT microwave world*” but the answer was “*It’s too late!*”. Erf. Since the first season of “HFT in my backyard”, I continue to check out what is happening here in the air. I wanted to post a second season last November, but the events both in Paris and here in Molenbeek were too hard. As I don’t want this S02 to be too long, and as this new project in Richborough deserves explanations, here are some details about what may be in the future *the tallest tower ever built for high-frequency trading purposes in the world*. (Below I use “S01E0x” to refer to the old posts of “HFT in my backyard” season 1, and “S02” to indicate some developments will be made in the forthcoming season2.)

###### CONTEXT

For some trading firms, or HFT market-makers, or PTG firms, or whatever the name, latency has become critical. Each microsecond may count, and even a bit of data is important. In order to carry data faster than using optic fibres (most often not optimized to get the best latency), some HFT firms (Amsterdam-based firms Optiver or Flow Traders, or Chicago-based firms Jump Trading, Getco/KCG or DRW) and different microwave providers (such as McKay Brothers or Custom Connect) decided to build from scratch microwave networks to connect the main European exchanges: mainly Frankfurt in Germany (where Eurex is located), Slough in the West of London (where the Equinix data centre hosts Chi-X and other exchanges) and Basildon, of London (where the NYSE-Euronext data centre is). (But some also have microwave routes between Frankfurt and Zurich, between Zurich and Milano, etc.)

[![Capture d’écran 2014-07-26 à 15.19.40](img/2fcc078245449a11248cc18f323fc002.png)](https://sniperinmahwah.wordpress.com/wp-content/uploads/2014/07/capture-d_c3a9cran-2014-07-26-c3a0-15-19-40.png)

Such networks need (sometimes tall) structures (masts, buildings, water towers, churches, etc.) where dishes are placed, and the dishes need to have a direct “line-of-sight” with their nearest dishes (meaning that nothing should block the signal between two dishes). I previously (S01) tried to figure out where the different firms put their dishes in the UK, Belgium and Germany, so that it would be possible to rebuild the different paths of the competitors – in two words: the shortest paths you have, the faster you are. With the help of public data (at least in the UK and France, Belgium being dark), some fieldworks and tips coming from (sometimes anonymous) people involved in the HFT area, I came up with this first approximative map over a year ago:

[![](img/3f458da212cd17e26c6255cb9fb10ea8.png)](https://sniperinmahwah.wordpress.com/wp-content/uploads/2014/08/capture-d_c3a9cran-2014-09-22-c3a0-08-56-09.png)

###### THE CHANNEL

Between Germany and the UK there is the backyard where I live (Belgium) but also the English Channel. I wrote before (and perhaps I went too far [[S01E04/2](https://sniperinmahwah.wordpress.com/2014/11/18/hft-in-my-backyard-iv-episode-2/)]) that crossing the Channel is quite challenging for many reasons, one of them being that microwaves need good atmospheric conditions and don’t really like fog, humidity, rain, etc. Managing microwave signals in a damp area is not that easy. What’s more, as the Germany-UK route needs to deal with different countries, *i.e.* different regulations (frequencies available in Belgium may not be allowed in the UK, etc.), so working with these different parameters is quite a challenge. Las but not least, given the fierce competition for speed, some networks may have to be updated, meaning that competitors need to find better (*i.e.* shorter) paths to improve their networks. For instance, if a firm has found a better way to cross the Channel, competitors need to follow the trend/path.

The map below shows that between 2013 and 2016 some paths have been seriously improved around the Channel: in 2014-2015 most of the competitors went from Dunkerque (France) to Swingate (UK) before splitting the signal; but in 2016 good competitors have paths going (from North of France of Belgium) directly to the Ramsgate area; bypassing the Swingate “Three Sisters” towers may save a few dozens of microseconds (click to enlarge):

[![](img/77d023a549c06fda2cbaf97285c7b9d6.png)](https://sniperinmahwah.wordpress.com/wp-content/uploads/2016/01/channel-2013-2016.png)

In this kind of environment, tall towers may be important. That’s why a Jump Trading has spent $5 millions to buy an old 243-meter US military tower in Houtem, on the Belgian coast, back in December 2013 (check out [S01E02](https://sniperinmahwah.wordpress.com/2014/09/25/hft-in-my-backyard-ii/) to learn more about the epic auction). The tower looks like that:

![European Military Towers Used By Traders In Arms Race For Speed](img/964c7085e23f6a668f604123567861f2.png)

Jump tower in Houtem (Belgium)

This is what is called a “[guyed tower](https://en.wikipedia.org/wiki/Guyed_mast)” (a very thin mast held by cables) and it’s located close to the France-Belgium border, not so far from Dunkerque where other competitors are to cross the Channel:

![](img/f8cf5e1ad61c4290762a479178eef0d5.png)

By working on the history of the Houtem tower ([S01E02](https://sniperinmahwah.wordpress.com/2014/09/25/hft-in-my-backyard-ii/)), I dug up an old technical [article](http://permanent.access.gpo.gov/gpo29426/79-30_ocr.pdf) highlighting the advantages of such a tall tower (in short: much less problems with the atmospheric conditions), and I put the different HFT competitors on the drawing:

![jumpandtheothers](img/3f867bebe227b3095ee65caf704ea470.png)

Jump has installed dishes on their mast in Houtem (Jump is now using the tower for their New Line Networks project, check out this previous [post](https://sniperinmahwah.wordpress.com/2015/02/19/hft-in-my-backyard-new-line-networks/) about this joint-venture between Jump and KCG) but other competitors (at least Optiver, McKay and probably Vigilant) are on other kinds of (smaller) towers, the Tour du Reuze in Dunkerque, France (cf. [S01E04](https://sniperinmahwah.wordpress.com/2014/11/03/htf-in-my-backyard-iv/)).

![Reuze](img/89ae396920489facb34f98417d9fefde.png)

Tour de Reuze, Dunkerque. This photography was taken by Eline Benjaminsen, a photography student at the Royal Academy of Arts in The Hague who is working a on project about HFT in Europe. Eline was able to access the top of the tower, where she shoot this HFT dish ready for use. © Eline Benjaminsen

Another competitor, McKay Brothers, installed dishes in the port of Dunkerque, on a grain elevator, as seen in a recent (but very poor) French TV [documentary](https://www.youtube.com/watch?v=W68UOYK_-bk) on HFT:

![Capture d’écran 2016-01-25 à 11.14.07](img/a58fb378f73ec130c3f03c572eacacca.png)

![Capture d’écran 2016-01-11 à 15.59.50](img/8547eaf17abdb91f1e88abf8236f8aac.png)

Because of the lack of data, guessing where the Vigilant Global dishes are is not so easy but I had found this UK [planning application](https://planning.dover.gov.uk/online-applications/applicationDetails.do?activeTab=documents&keyVal=DCAPR_226165) in the name of Nova Scotia, which appears to be an [alias](http://listings.fta-companies-ca.com/l/110341605/3268120-Nova-Scotia-Company-in-Montreal-QC) for Vigilant (some HFT players love aliases). By corroborating the application (azimuts, etc.) with Ofcom [data](http://spectruminfo.ofcom.org.uk/spectrumInfo/licences?googloc=(51.13810919630982%2c+1.3364052772521973)&code=301010&se=(51.1364262262364%2c+1.3390874862670898)&googoffset=0.2&nw=(51.13979210503717%2c+1.3337230682373047)&unit=GHz&ne=(51.13979210503717%2c+1.3390874862670898)&service=Fixed+Links&sw=(51.1364262262364%2c+1.3337230682373047)&submit=Submit+search&groupKey=4), the Vigilant Global routes around the Channel may look like that: they go from Dunkerque to Swingate, and then they have two routes from there, one for Basildon, an other for Slough. If I am not mistaken, only three firms (McKay Bros, Optiver and Jump/New Line) are bypassing Swingate (planning applications in Ramsgate are available for [Optiver](https://planning.thanet.gov.uk/online-applications/applicationDetails.do?activeTab=documents&keyVal=ZZZZMPQEBJ619), [Jump](https://planning.thanet.gov.uk/online-applications/applicationDetails.do?activeTab=documents&keyVal=NUCXDFQEG4700) and [McKay](https://planning.thanet.gov.uk/online-applications/applicationDetails.do?activeTab=summary&keyVal=ZZZZMQQEBJ126)). Vigilant being considered as a fierce and very good competitor in the microwave area, a new move was expected. And it came in April 2015.

[![Vigilant-now](img/84a4f3f2a937531e23d962c98e0e0196.png)](https://sniperinmahwah.wordpress.com/wp-content/uploads/2016/01/vigilant-now1.png)

###### RICHBOROUGH

In April 2015, UK radio regulator Ofcom granted new [licences](http://spectruminfo.ofcom.org.uk/spectrumInfo/licences?googloc=(51.31135470844741%2c+1.338486671447754)&code=301010&se=(51.30767941763878%2c+1.3443660736083984)&googoffset=0.4&nw=(51.315029704889824%2c+1.3326072692871094)&unit=GHz&ne=(51.315029704889824%2c+1.3443660736083984)&service=Fixed+Links&sw=(51.30767941763878%2c+1.3326072692871094)&submit=Submit+search&groupKey=2) for Vigilant Global in Richborough, in the South of Ramsgate.

![Richborough](img/85f70468ec90480ea15a37f22fa72b45.png)

When I checked out the location last year, this was a surprise: there is no tower here (only wind turbines and old electric pylons); it’s just a field, and the location is only 2 meters above sea level. Given the atmospheric conditions around the Channel and the curvature of the earth, it’s obviously impossible to build a path from Richborough without something that doesn’t exist – yet.

[![](img/dad19780e5d55d46b2e7967887162db3.png)](https://sniperinmahwah.wordpress.com/wp-content/uploads/2016/01/capture-d_c3a9cran-2016-01-25-c3a0-11-18-20.png)

Back at the time I checked the other point of the path, in Belgium. It’s a ±40-meter residential building in Oostduinkerke:

![Capture d’écran 2016-01-11 à 16.11.38](img/a537dad86bdfc4ad1db6e4d30b07d7fb.png)

Ofcom data tells us the Vigilant path to cross the Channel would look like that:

[![Capture d’écran 2016-01-25 à 12.31.41](img/ad36d035874c82d05fc1fdc217f9cf99.png)](https://sniperinmahwah.wordpress.com/wp-content/uploads/2016/01/capture-d_c3a9cran-2016-01-25-c3a0-12-31-41.png)

This would be the longest path to cross the Channel (95,6 km), compared to the shortest (Mckay Brothers, 71 km). (Custom Connect may have a 106 km path from Hougham, UK, to Berthen, France, according to this [planning application,](https://planning.dover.gov.uk/online-applications/applicationDetails.do?activeTab=documents&keyVal=DCAPR_224609) but that’s not corroborated by the French regulator Arcep [data](http://www.cartoradio.fr/cartoradio/web/#bbox/2.66424927563943/50.7620657937806/2.70785486887889/50.7921568171954/2636) – it seems that no one really knows how Custom Connect crosses the Channel, but that is another matter).

As for Vigilant in Richborough, I was wondering: how is it possible to build a path from such a low point in the UK? I was expecting something, but not what Vigilant is seeking to do: erect a giant 324-meter guyed tower, taller than the Shard or the Eiffel tower, which would be unquestionably the tallest structure ever built for trading purposes in the world, a kind of answer to the 243-meter tower owned by Jump in Houtem:

![Channel-inverse](img/7645454d2be07e7f1525141741d7497e.png)

This is a new battle in the war of the tall towers around the Channel. Vigilant’s move is quite beautiful but, as you will read, the height of the Richborough tower is not the most spectacular.

###### IT’S ALL ABOUT EDUCATION

Vigilant Global is a trading firm from Montreal that was purchased by the powerful Chicago-based HFT firm DRW Trading Group (who also bought another HFT competitor last year, Chopper Trading). According to this legal [document](https://s3-eu-west-1.amazonaws.com/document-api-images-prod/docs/AJE7RiCL7GmP6Yy2KSIEUoHn4Fcfx2yGVc26dMtf26Q/application-pdf?AWSAccessKeyId=ASIAJ4I7MXRIM25XYBMA&Expires=1453720788&Signature=nzLDymC8FrlRYBr0MtiVXdqYmVA%3D&x-amz-security-token=AQoDYXdzEFsa4AOgUnwRoEeDrNLgIU64nEIiRGG3BbvWyMJdfsDjk2tGJM3sdo6FDgMQ3TWNhkR7EiG8VgLke24Qvw7uXMSg6%2BymBA7ylJ1nAB%2FfcxQgeYLX2rclUyYLLllXAXDYQCPvPpR6J9l9qZfN%2FXYkpCnHMdG7yVJQnC5eW2BUub7RqZdgxFL8jI6Am5dgeF8yseyEG%2FmUL6mZxTvzfCv8VBpEHumg2VmPj1NNWYI4FGzbtzkKhfd06n6aC04Kk9OgaTmfxGdOQ3Sg1zFRY63fEE%2FeIwSddaejv3l2ySV61pTY%2FCcIKIgzs2JLlPVndKFEIFtx2QJPo%2BP8Pydc7Ru58aJHqEHF8XdvoivtmZlBbtf30lIe0jhnIG5VKWxOy1OaB%2BE02vyfNIXE6PRGzhXKPXVCR9%2FXVo2X38RyoDfmbOt0P%2Bccz%2BiyNHqpUh5ICc7VNizAO6Oxt7d4eUVRnB6ffMzUAq466thbbNn2KJ4dnhPrWcSYpcUJ3%2FLp1UT262f00unCyF6yNkHjbf1877MUDRxzmTbw2NXYWmnaB0tPr9GmrUW6M4FHtSwjPvPN%2FRvUjR8Gze37SN4lif%2BqHobDmIySx%2BqfLJf0qQQsacGtV8OT8PEGHXS7DyaYca%2BrPJfJHilf2Log4uWXtQU%3D), Vigilant Global UK Limited has one shareholder only (DRW) and is managed by Josh Felker, one of the founders of Vigilant Global – meaning that even if the two founders of Vigilant, Josh Felker and Arvind Ramanathan, sold their firm, they may be still working on the design of the microwave networks. I didn’t work on the HFT microwave networks in the US but I have been told that through their aliases (Wireless Holdings, Qoncept Holdings, etc.) they have built very nice paths between New Jersey and Chicago/Aurora; as for the London-Frankfurt, I already noted ([S01E03](https://sniperinmahwah.wordpress.com/2014/10/02/hft-in-my-backyard-iii/)) that they have (or anticipated) very good routes; they may have been the first to have a complete route between the two cities (in 2012?), and are considered as a fierce (and admirable) competitor by most of their rivals.

On August 26, 2015, five months after Vigilant acquired Ofcom licences there, the company created a [website](http://www.richboroughmast.co.uk) dedicated to the future giant tower, where the firm explains to the residents of Richborough the importance of the mast. They also organized two meetings with locals on September 25 and 26, 2015\. After all, a new 324-meter mast in the landscape is well worth a justification, and the website is well done by giving some clear explanations on the infrastructure needed to send a signal above the Channel:

![](img/3e1950fe2ba3ba11b410caced8079f0a.png)

Above: why Vigilant need to build such a tall mast given the way waves travel between two points. Below: the drawing of the mast; a simulation of the view of the mast from Ramsgate road. From richboroughmast.co.uk. © Vigilant Global UK Limited

If Vigilant purposely avoids the words “trading” or “finance” in their statement (they only refer to “data transfer”), the website describes in detail the [benefits](http://www.richboroughmast.co.uk/benefits) that would be provided by the mast to the Richborough community (a fast wireless high-speed broadband; a support to the Dover Community Radio; and a sponsorship to the local Sandwich Technology School). This website and the two meetings are only the first step in what will probably be a long way: both residents and local authorities will have to approve the construction of the mast, and nothing is won in advance as a new giant tower in a country-style landscape is not insignificant. When the mast attracted attention just after I tweeted about it, the [*Daily Mail*](http://www.dailymail.co.uk/news/article-3386311/A-mast-taller-Shard-country-Angry-residents-attack-firm-s-plans-tower-help-transmit-data-saying-eyesore.html) (as expected, it’s the *Daily Mail*) has found a reluctant resident: “*They are greedy bankers. If this was to happen, even though we have lived here for 12 years, we would consider moving house*”. Lol. A local chairman added: “*We’ll reserve judgment as we haven’t got a proper planning application yet*”, and that’s true: there is no planning application for the mast, but another interesting public document.

###### THE BANANA LAND

The “[EIA Screening Opinion for a 320 m high Communications Mast](https://planning.dover.gov.uk/online-applications/applicationDetails.do?activeTab=relatedCases&keyVal=DCAPR_227388)” Vigilant submitted in August 2015 has an application form with more details about the tower. The mast will be erected in the western part of the Richborough Power Station, a place referred to as “The Banana Land” (I suppose the name comes from the pseudo-tropical climate created by the station?). The Richborough Power Station, quite famous in the UK, produced power between 1962 and 1996, and had three 93-meter cooling towers that were demolished in 2012:

![](img/e4b7beb5b1fd4ccc2826e6199159e3f0.png)

The demolition of the Richborough Power Station cooling towers in 2012

What is interesting is that before a HFT firm had the idea to build a mast in Richborough, other kinds of towers had been in the landscape for decades. When it was decided to demolish the cooling towers, some locals had campaigned to keep them as they were “*a part of the historical landscape and were used as a navigation point by boats wanting to enter the mouth of the river Stour, known to have a narrow channel of useful depth*”. This kind of arguments may help Vigilant: after all, a 324-meter thin guyed tower is much more discreet than a big cooling tower, and with this giant mast fisherman could easily have a new navigation point.

But on the other hand other plans at the Power Station may not help Vigilant. The new life of the station is named “[The Nemo Link](http://www.nemo-link.com)”, the first electricity interconnector between the UK and Belgium. Electricity will flow in either direction between the two countries, and a cable will pass under UK and Belgian waters (if some are building wireless networks to cross the Channel, others still need the good old cables). The landing stations of the cable will be in Zeebrugge (Belgium) and Richborough (UK):

![Capture d’écran 2016-01-25 à 14.07.39](img/9b0743f3e9ab0c0da84d8fe6a8af6f7b.png)

The Nemo grid will need 60 new pylons from Richborough to Canterbury, and a 53.6-meter pylon will be constructed in the Banana Land, right in front of the Vigilant tower…

![NemoProject](img/81563b9bfb770eb2d65786c76285c36d.png)

… as attested by Vigilant in the drawing of the tower found in the “[EIA Screening Opinion](https://planning.dover.gov.uk/online-applications/applicationDetails.do?activeTab=relatedCases&keyVal=DCAPR_227388)”(here in pink):

![Capture d’écran 2016-01-25 à 14.14.25](img/334cadb0fc5972c0768133546fa2a99a.png)

But given the height of the tower and the fact the dishes pointing to Belgium will be at the top of the it (at 320m and 210m)…

[![Capture d’écran 2016-01-25 à 14.22.59](img/fd6cf8655a811e329e81dca5404a3a63.png)](https://sniperinmahwah.wordpress.com/wp-content/uploads/2016/01/capture-d_c3a9cran-2016-01-25-c3a0-14-22-59.png)

… I don’t think HFT data will be disrupted by what will happen 270 meters below. But this is not the most important. What matters is: the Nemo grid is not well received – we may add: at all (check out [here](http://www.kentonline.co.uk/canterbury/news/pylon-plans-to-cut-a-31587/) or [there](http://www.bbc.com/news/uk-england-kent-35382712)). Both residents and members of the UK parliament don’t want new pylons (they prefer burried cables), and Vigilant comes at a time when high structures in the landscape are not trendy. What’s more, the Richborough residents/authorities will have to make two decisions: one about a giant but elegant mast carrying financial data between Frankfurt and Slough, and an other about a modest concrete tower carrying power between Richborough and Canterbury. They may decide to make a choice.

Beyond all of that there is one question: if a firm can spend enough money to build a structure taller than the Tour Eiffel, how much money is floating in the air? That was my question in 2014 when Jump purchased the Houtem tower. $5-6M to buy and rebuild a 243-meter tower in Belgium was quite an investment (one can estimate that this is the cost of a whole network between London and Frakfurt). It’s hard to evaluate how much money Vigilant will spend in Richborough; we may estimate the tower itself would cost ±$3M (depending on the prices of raw materials – the cables mainly) but additional costs should be considered (local taxes; cost of the broadband proposed to the community, etc.). Anyway, as microwave has become critical for HFT competitors in the Frankfurt-London route, there is probably enough money going through the air to justify the building of new tower. But a question remains : why Richborough?

###### THE MEET-ME ROOM

Before answering, there is an interesting story. If Vigilant succeeds in building their giant tower, the different wave signals of the Vigilant, Jump, Optiver and McKay will cross in the same area, above the Channel, ±20 kilometers off the England coast:

![Capture d’écran 2016-01-25 à 15.36.58](img/9c599bd04a6b323422dee7722f680bb7.png)

![Cross](img/aae5f4725dbebeb4e4a25a193d906acb.png)

Given that waves don’t move in a strict straight line (as explained in the drawings Vigilant put on the website, cf. above) but are affected by diffraction, even if the towers/dishes between two points must have a clear line of sight, microwave network builders need to take into account the [Fresnel Zone](https://en.wikipedia.org/wiki/Fresnel_zone), “*a zone* t*hat must remain unobstructed lest the microwave beam be partially attenuated*” according to two microwave experts I had questioned. “*Objects obstructing part of the fresnel zone lead to what are called ‘diffraction losses.’ Diffraction makes the amount received by the antenna complicated in general*”. I asked my two experts, Greg and Anthony, if we could figure out, given the heights of the different towers, what is going on in this 1,8 square kilometres area above the Channel (I don’t have the skills to work on that alone, so thank you my friends). My question was: is it possible to know which signal is above (or under) others. Anthony came out with these charts (click to enlarge):

[![Charts](img/56afc27e55812bd70d8b2ea17178c691.png)](https://sniperinmahwah.wordpress.com/wp-content/uploads/2016/01/charts.png)

If we put the four charts together, we have this (the black rectangle is the 1,8 square kilometres zone where the different signals cross):

![Montage](img/fe2b0db087b8def7d0dfc3a6928f5260.png)

“*Depending on the equipment, this could in principle be converted into a probability distribution for diffraction attenuation that can be put into assessing the reliability of the link.  With the above clearance rules obeyed, diffraction would only play a significant role a pretty small fraction of the time. The fact that all of the cross-channel links fail these rules means that they are non-negligibly affected by diffraction*…” but *hélas* “*the actual impact on their uptime would take a lot of modeling and data we don’t have*”. That means those charts may not be so accurate; however, we will try to do better later (S02). But one thing is sure here: if someone spreads out a very large aluminium foil in this small area of the Channel, that could block the waves (and the entire microwave network) of the high-frequency trading competitors, at once.

###### THE STRAIGHT LINE

Let’s answer to the question: why Vigilant wants to build a tower in Richborough… and not, for instance, in Ramsgate or in Swingate? This is the million-dollar question (or, for HF traders, the $0.01 question). With the mast in the Banana Land, Vigilant would have this path to cross the Channel:

[![Capture d’écran 2016-01-26 à 11.57.31](img/2dd1f43e275e2ea2e6fe8ba406f583ac.png)](https://sniperinmahwah.wordpress.com/wp-content/uploads/2016/01/capture-d_c3a9cran-2016-01-26-c3a0-11-57-31.png)

First surprise: contrary to Jump, McKay and Optiver, who are using the Ramsgate area to send microwaves to Basildon (through Benfleet), Ofcom [data](http://spectruminfo.ofcom.org.uk/spectrumInfo/licences?googloc=(51.31135470844741%2c+1.338486671447754)&code=301010&se=(51.30767941763878%2c+1.3443660736083984)&googoffset=0.4&nw=(51.315029704889824%2c+1.3326072692871094)&unit=GHz&ne=(51.315029704889824%2c+1.3443660736083984)&service=Fixed+Links&sw=(51.30767941763878%2c+1.3326072692871094)&submit=Submit+search&groupKey=2) tells that Vigilant (at least for now) will use the Banana Land tower to send microwaves to Shorne, towards Slough (and not Basildon):

[![Vigilant-Rich-Shorne](img/be7e9ea7771aaea6b8ab7266d85fc61e.png)](https://sniperinmahwah.wordpress.com/wp-content/uploads/2016/01/vigilant-rich-shorne.png)

It’s quite difficult to find the HFT dishes in ~~my backyard~~ Belgium (no public data available here) but I have heard that “Vigilant loves the [Norking network](http://en.norkring.be/transmitter-park/all-transmision-masts-charted/)”, so it’s quite possible the signal may be sent from Oosduinkerke to the Norkring tower in Egem (which is the tallest structure in Belgium – check out the review of my hilarious [visit](https://sniperinmahwah.wordpress.com/2015/02/03/hft-in-my-backyard-the-last-tower/) to this tower last year).

[![Capture d’écran 2016-01-26 à 12.16.51](img/4672cbc8baf5e3861f2a5136995985a9.png)](https://sniperinmahwah.wordpress.com/wp-content/uploads/2016/01/capture-d_c3a9cran-2016-01-26-c3a0-12-16-51.png)

Let’s have a look at the other side of Belgium. I was told that Vigilant has a path between Tirlemont and Welkenraedt, Belgium (these recents [dishes](http://theantennasite.com/locations/welkenraedt-chemin-du-moulin-vent/) in Welkenraedt may be the ones of Vigilant). It’s hard to tell where the HFT microwave competitors go from the Belgium-Germany border as there is not public data in Germany too, but I suppose they all pass through the Simmerath area before going to Weibern (Germany), where there is a huge mast which appears to be ideally situated between Simmerath and Frankfurt (the German industry!):

[![Capture d’écran 2016-01-26 à 12.27.47](img/c4d6331645a57aba53c32debbeb41f1c.png)](https://sniperinmahwah.wordpress.com/wp-content/uploads/2016/01/capture-d_c3a9cran-2016-01-26-c3a0-12-27-47.png)

Now let’s put the possible Vigilant route from Frankfurt to Slough through Richborough on the map I have been trying to draw (again, I may have some inaccurate data for Belgium but a Vigilant competitor told me: “*I’m pretty close*” and that’s enough for me):

[![Capture d’écran 2016-01-26 à 12.42.07](img/1b980339bf04dee1b7e8ba6d29c25e5d.png)](https://sniperinmahwah.wordpress.com/wp-content/uploads/2016/01/capture-d_c3a9cran-2016-01-26-c3a0-12-42-07.png)

The Vigilant route is not clear, so I did better:

[![Vigilant-Nearly](img/4ab3c2a3353fc1dc2b032b96d4479860.png)](https://sniperinmahwah.wordpress.com/wp-content/uploads/2016/01/vigilant-nearly.png)

And better (I added the perfect theoretical straight line in white):

[![Vigilant-Final](img/0498fad37d13427784256a5b610ea440.png)](https://sniperinmahwah.wordpress.com/wp-content/uploads/2016/01/vigilant-final.png)

This. This, my friends, this is art. A quasi perfect straight line between Frankfurt and Slough. That’s awesome. [Kmz file available [here](http://www.zones-sensibles.org/wp-content/uploads/2016/01/Vigilant-2016.kmz_.zip).] A fantastic route that explains why Vigilant/DRW wants to build a 324-meter tower in Richborough and not somewhere else. I’m pretty sure none of the HFT (microwave) competitors would be able to do better than that (and I’m pretty sure Vigilant has designed this route for a while). But of course there is a *if*: Richborough residents and authorities have to say “*yes*” and there are no guarantees they will. In my view, this is an anthropological issue.

It is one thing to purchase old and tall military towers and put new dishes on them, as Jump did in Houtem (the mast was there since the 1960’s, and the only person who has witnessed how high-frequency trading invaded Houtem was the farmer living at the foot of the tower). It is quite another to reshape the landscape of anthropocene with a new giant mast specially designed to trade at the speed of the light. They are two completely different things. For centuries, the tallest structures in the (occidental) world have been church steeples; they have been conceived not only to assist travelers (as a navigation point) but, above all, to place religion in the everyday landscape of men. Now that “*God is dead*” (as a philosopher once said), inhabitants of the Western world need to realize that the tallest structures they can see in the landscape are the face of what may be a new kind of God: finance.