<!--yml
category: 未分类
date: 2024-05-18 14:10:47
-->

# HFT (not) in the Banana Land | Part 4 – Sniper In Mahwah & friends

> 来源：[https://sniperinmahwah.wordpress.com/2016/07/27/hft-not-in-the-banana-land-part-4/#0001-01-01](https://sniperinmahwah.wordpress.com/2016/07/27/hft-not-in-the-banana-land-part-4/#0001-01-01)

This blog has been quite silent for a while (too much bloody work) but that does not mean the “HFT in the Banana Land” series is finished. Quite the contrary: what was dubbed “[The Case of the Small English Town vs The Large HFT Tower](http://blog.themistrading.com/2016/02/the-case-of-the-small-english-town-vs-the-large-hft/)” by Themis should be renamed “The Case of the Small English Town vs The **Two** Large HFT Tower**s**” as there is now a fierce battle between Vigilant Global/DRW and New Line Networks (KCG/Jump) in Richborough, each firm seeking to build a 300-meter mast in the same area, as close as one kilometer apart – a third (and concerned) party recently [said](http://www.mckay-brothers.com/exchanges-vs-networks/) in Chicago: “*It’s crazy*”. What was going on the last weeks around the Banana Land (and in Belgium) is captivating; a lot has happened and it’s hard to summarize, but I’ll try to make a not-too-long and clear summary on the current situation in in the next episode.

[![Richborough](img/63ce50f152d9c8b3d221158147924006.png)](https://sniperinmahwah.wordpress.com/wp-content/uploads/2016/07/capture-d_c3a9cran-2016-07-26-c3a0-08-36-27.png)

Vigilant Global and New Line Network in Richborough, where the Eiffel Towers battle is going on.

(By the way, when Themis’ Joe Saluzzi posted “[The Case of the Small English Town…](http://blog.themistrading.com/2016/02/the-case-of-the-small-english-town-vs-the-large-hft/)”, his tweet was liked by @RemcoLenterman and retweeted by @nanexllc, and that is real *a tour de force. *Congrats Joe, being endorsed by both Remco and Nanex is a quite a challenge).

###### **SLOUGH**

All the HFT firms (Vigilant, Optiver, etc.) or microwave providers (Custom Connect) having a network between London and Frankufrt have to deal with at least two different locations in London (LHC and Interxion aside): Basildon (where the ICE/NYSE/Euronext exchange is located) and Slough (the Equinix LD4 where the matching engine of, for instance, BATS (ex-)Chi-X, is located). In the London metro area waves are not micro (MW) but millimeter (MMW). MMW are faster than MW but they are not good for long distance transmissions due to higher signal loss, so a path between two points is several kilometers only (compared to a 100-kilometer path you can get with MW). That means there are *a lot* of MMW dishes between Slough and Basildon. And that means every location is important if you need, let’s say, to build a mast. According to the McKay Brothers [website](http://www.quincy-data.com/product-page/), it takes less than *one millisecond* for a MMW signal to travel between the two data centres (273 microseconds exactly). Every microsecond counts.

[![Capture d’écran 2016-07-26 à 09.47.26](img/01f923bf7e7429b688b68efcea383098.png)](https://sniperinmahwah.wordpress.com/wp-content/uploads/2016/07/capture-d_c3a9cran-2016-07-26-c3a0-09-47-26.png)

Microwave networks in London. Straight paths are in white. (Note that this map is not up to date)

Back in February 2013, Equinix decided to erect a 25-meter mast next to their data centre. The planning application is [there](http://www.sbcplanning.co.uk/sbcp/slough01/planapp/A27C89E7/A27C89E7.pdf#pagemode=thumbs) and this part is interesting: “*The Equinix worldwide network of data centres and international business exchanges are currently connected by fibre optic cables. However within the UK in recent years, metal and cable theft has extended to almost epidemic levels. In the last couple of years, this has become one of the fastest growing national menaces with the Home Secretary and HM Treasury estimating the annual cost to industry to be in the region of £1bn for just the replacement of the metal/cable. These numerous fibre cuts have caused both Equinix and its customers, particularly in the UK  financial services sector, a significant reduction in speed of service which, considering the UK as one of the most globalized economies in the world and The City of London as one of the world’s three command centres of the global economy, is unacceptable. Indeed with financial services contributing such a large proportion of the UK’s GDP, any slow down or potential disruption to service is of national importance. Consequently many of Equinix’s customers are now implementing a wireless network to avoid any such outages and the subsequent loss of important services and reduction to GDP*.” If I understand correctly, the high-frequency traders decided to use wireless networks because some villain cable thieves reduced UK’s gross domestic product… Good story.

![Capture d’écran 2016-07-26 à 10.35.32](img/72479b0ad56adfa28a1e73c6ceb96ec4.png)

High-speed traders on the Equinix/LD4 data centre mast

The application includes an interesting document I missed when I started to investigate the HFT networks, a document with the names of the different “operators” who put (or were supposed to) dishes on the Equinix mast:

![Capture d’écran 2016-07-26 à 11.09.01](img/6bc6a679961f205cf05ec7b4f17ea1de.png)

As expected we meet familiar names: Vigilant Global, Jump Trading, Global Connect/Flow Traders, Getco – now KCG –, Custom Connect, and Virtu Financial – but it seems Virtu never built a proprietary wireless network in Europe. I don’t know who is TTX – TTX Trading LLP, an English company [dissolved](https://beta.companieshouse.gov.uk/company/OC366902/filing-history) in 2015? or this other [TTX Trading](https://offshoreleaks.icij.org/nodes/10140705)? Whatever. Note that this table, dated 2013, does not include other familiar names/operators/firms such as McKay Brothers, Optiver or Tixos. Tixos is an interesting case. They play the Slough-Basildon route only, they don’t have the full London-Frankfurt network, so my suspicion was: Tixos is more interested by equities than derivatives. Tixos was the only network I could not identify when I started to figure out who were the very low-latency actors sending waves above our heads. Tixos did not seem to be a trading firm nor a publicized micro/milli/waves provider. I suspected Tixos to be a private wireless provider working for a single market maker/high-frequency trader (and I was right). But the [public data](https://beta.companieshouse.gov.uk/company/08659771/filing-history) about this UK company does not mention names related to trading. Since *tixos* means “wall” in Greek, I thought the firm behind Tixos was from *Wall* Street (and I was wrong). I asked around to my industry contacts, some of them knew the answer but didn’t want to tell me (that’s the usual and fun game between them and me: I have to find information myself ;). At some point I got a lead from London saying “Look at the [Modern Markets guys](http://modernmarketsinitiative.org/about/about-modern-markets-initiative/)”. Funny.

So, Equinix erected a mast and rented spaces to different HFT-related companies. But some other exchanges didn’t, perhaps because they have high roofs (pure speculation) like the Deutsche Börse one in Frankfurt:

[![](img/1641c7da950a634bab778d7741fd376f.png)](https://sniperinmahwah.wordpress.com/wp-content/uploads/2016/07/cdlvpnkwoaawcs-large.jpg)

The roof of the Deutsche Börse data centre in Frankfurt at night. Thanks to [censured] for the photo.

###### BASILDON

It is the same in Basildon, as can be seen in this photography twetted by a financial engineers (there are far more dishes on this roof now):

[![Capture d’écran 2016-07-26 à 13.43.42](img/9c5862a93da3ee0bb2b2dcdce62f2cc0.png)](https://sniperinmahwah.wordpress.com/wp-content/uploads/2016/07/capture-d_c3a9cran-2016-07-26-c3a0-13-43-42.png)

I visited Basildon twice but the array is at the center of the roof – once I was there with (bad French) TV journalists and I asked them if they could bring a drone so that they could shoot the dishes, but they refused – too bad. Now let’s talk a little bit about sport. Because the HFT firms love sport. Here is a map of the eastern area around Euronext:

[![Capture d’écran 2016-07-26 à 14.47.31](img/8b071a0d22e73f6d6f0431239d82c66f.png)](https://sniperinmahwah.wordpress.com/wp-content/uploads/2016/07/capture-d_c3a9cran-2016-07-26-c3a0-14-47-31.png)

Two sport centres are in this area: the [Basildon Sport & Leisure Club](https://www.facebook.com/Basildon-Sport-and-Leisure-Club-166215233431941/) and the [Basildon Rugby Football Club](http://www.pitchero.com/clubs/basildon/contact/). Back in August 2013, Jump Trading filed a [planning application](http://planning.basildon.gov.uk/online-applications/applicationDetails.do?activeTab=documents&keyVal=MODTE0CQ32000) to build a 20-meter mast on one of the Basildon Sport & Leisure Club fields – if you don’t find buildings or towers available exactly where you need to, you just have to build your own facility. “*The bearings at which the dishes are proposed to be installed would reflect the direction of the microwave transmission links and facilitate high speed data transfer from overseas across the United Kingdom, enabling UK based businesses to be more competitive in the global economy*”.

[![](img/ac0859b07d0da0a271d2e99087516a7e.png)](https://sniperinmahwah.wordpress.com/wp-content/uploads/2016/07/capture-d_c3a9cran-2016-07-26-c3a0-19-12-29.png)

The Jump Trading 20-meter mast in Basildon

The [Ofcom licences](http://spectruminfo.ofcom.org.uk/spectrumInfo/licences?service=Fixed+Links&code=301010&freqStart=&freqStop=&unit=GHz&ngrloc=&offset=&nw=%2851.58944283871291%2C+0.4777336120605469%29&ne=%2851.58944283871291%2C+0.4799652099609375%29&se=%2851.58805634325151%2C+0.4799652099609375%29&sw=%2851.58805634325151%2C+0.4777336120605469%29&googloc=%2851.58874959627155%2C+0.4788494110107422%29&googoffset=0.1&submit=Submit+search) granted to Jump in 2013 (and to New Line Networks in 2015) shows the path from this new mast to the Euronext data centre, and three possible paths going to Slough:

[![](img/9db12a34d6edd5548cbb5b6d41e178fc.png)](https://sniperinmahwah.wordpress.com/wp-content/uploads/2016/07/capture-d_c3a9cran-2016-07-26-c3a0-16-57-24.png)

“*The site owner has future plans to re-develop the site, and therefore only a 2 year lease has been agreed for the proposed telecommunications equipment*” Jump stated. That’s true: the firm filed a new [application](http://planning.basildon.gov.uk/online-applications/applicationDetails.do?activeTab=documents&keyVal=NOEEF0CQ06B00) in July 2015 (“*Renewal of planning permission”,* etc.), and said again that “*the property owner has future plans to potentially re-develop the site*.”

In the meantime, in October 2014, another HFT firm showed interest for the local sport centres and filed an [application](http://planning.basildon.gov.uk/online-applications/applicationDetails.do?activeTab=documents&keyVal=NCRD61CQFUQ00) to build a 35-meter mast (15 meters higher than the Jump one) on the Basildon Rugby Football Club ground. The name of this competitor? Vigilant Global. What is happening in Richborough nowadays is only a sequel of what happened in Basildon before – but with higher towers. Vigilant stated in the document that “*with this site, Vigilant Global is committed to contribute to the community through its compensation of the local Rugby Club*… *should this application be rejected, the negative impact on Vigilant Global’s financial returns would have a similar impact on the local community through a trickledown effect*… *there is an existing 20 metre lattice tower of a similar nature to this proposal sited approximately 300 metres north of the site within the grounds of the Selex Sports and Leisure Club” – *hello Jump – but Vigilant added that the Jump mast was an “*unsuitable structure for the proposal as it is too low, therefore, the required line-of-sight for the network path will not be achievable*” (note that Vigilant never writes the unsuitable mast is owned by a competitor – discretion is advised). With this new 35-meter mast in Basildon, Vigilant is getting closer to the perfect straight line between Basildon and Slough. Nice done.

[![](img/802c28f5986e49d75b5a932b3302a015.png)](https://sniperinmahwah.wordpress.com/wp-content/uploads/2016/07/capture-d_c3a9cran-2016-07-26-c3a0-16-58-312.png)

Jump and Vigilant in Basildon. Straight line between Basildon and Slough in white.

The local landscape should look like this now:

[![Capture d’écran 2016-07-26 à 16.52.18](img/554c2ade2bee427f303a78f2d8b2349c.png)](https://sniperinmahwah.wordpress.com/wp-content/uploads/2016/07/capture-d_c3a9cran-2016-07-26-c3a0-16-52-18.png)

Before HFT. After HFT.

(Compared to the high and very elegant guyed tower, this little tower is quite ugly but it’s a matter of personal taste). But this is not the end. In January 2016 Jump decided to fight back and filed a new [application](http://planning.basildon.gov.uk/online-applications/applicationDetails.do?activeTab=documents&keyVal=O1KHV0CQJJ100) (through New Line Networks), saying that they wanted to improve their mast: “*Temporary permission is now required for a larger structure to improve the network and provide a new link for a limited period*”. “*Larger structure*” means the new mast would be 34-meter high (1 meter less than the Vigilant tower, though). The residents living around the Banana Land will love this part: “*On 5th February 2015 planning permission was granted for a 35m high lattice tower with 4 no. 0.6m diameter telecommunications dishes, 1 no. equipment cabinet and ancillary development” –* the Vigilant mast*. “Consideration was given to sharing this site*” – did Vigilant and Jump/NLN have a little discussion? “*However, as the landlord has signed exclusivity contract with the tenant* [Vigilant]*the site is not available for a site share” –* too bad. End of the story. (In April 2016 Jump/NLN withdraw the application, it seems they gave up on heir new mast).

Some of those little towers are temporary and will be removed when/if the HFT firms find some better locations/paths. But the 300-meter masts Jump/NLN and Vigilant seek to build around the Banana Land will be there to stay (at least for 25 years). It’s quite a different story. “*We are unwilling to support any mast there and suggest it goes somewhere like the garden of Goldman Sachs CEO!!*” wrote a resident of Richborough in a comment. The battle will be fierce. Stay tuned and happy summer.