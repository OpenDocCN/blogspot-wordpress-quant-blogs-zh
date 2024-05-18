<!--yml
category: 未分类
date: 2024-05-18 14:07:56
-->

# SHORTWAVE TRADING | PART II | FAQ AND OTHER CHICAGO AREA SITES – Sniper In Mahwah & friends

> 来源：[https://sniperinmahwah.wordpress.com/2018/06/07/shortwave-trading-part-ii-faq-and-other-chicago-area-sites/#0001-01-01](https://sniperinmahwah.wordpress.com/2018/06/07/shortwave-trading-part-ii-faq-and-other-chicago-area-sites/#0001-01-01)

> ##### [I pleased to share Part II of “Shortwave Trading” by Bob Van Valzah. Part I had more than 25,000 views, which is quite insane. Thank you for all the comments we got. Comments in brackets [] and in italics signed SIM (as for SniperInMahwah] are mine – Alexandre. Happy reading]

I have [previously claimed that trading over shortwave radio is real](https://sniperinmahwah.wordpress.com/2018/05/07/shortwave-trading-part-i-the-west-chicago-tower-mystery/) and presented the story of the first evidence I found of it. It was pleasantly surprising to see the story picked up by [IEEE Spectrum](https://spectrum.ieee.org/tech-talk/telecom/wireless/wall-street-tries-shortwave-radio-to-make-highfrequency-trades-across-the-atlantic), [Hacker News](https://news.ycombinator.com/item?id=17028892), [Hackaday](https://hackaday.com/2018/05/12/hft-on-hf-you-cant-beat-it-for-latency/), and others. But since I hadn’t anticipated such a diverse audience, I didn’t provide details needed to understand shortwave trading in context so a lot of questions were raised. I’ll provide some background here, answer the questions, and also document two other shortwave trading sites I’ve found around Chicago. Traders can skip ahead while I fill in the broader audience.

#### Why is there a latency race? Isn’t it just a waste of money?

Electronic trading technologist just take the latency race for granted, but it’s important to think about why it exists and what it means to the average person. When you want to fill your car with gasoline, you have the choice of going to the nearby gas station and accepting their price or perhaps comparing prices at stations a little farther away. We would all spend a lot more time comparison shopping if we didn’t have pretty good confidence that the prices at our local stations were competitive. But what keeps those prices competitive?

The analogy between your local gas station and electronic markets is admittedly imperfect, but I think it is helpful in understanding why latency matters and how you benefit. Nobody can buy a tanker of gasoline in New York and immediately sell it in Chicago. The laws of physics prevent us from economically moving such a heavy load over a long distance quickly. But a share of Apple stock weighs nothing. The Chicago price and the New York price can be compared and changed in an instant. Well, about 4 milliseconds is how long it takes for an updated price to make the trip. Prices can make about 250 one-way trips in a single second.

So when buying or selling Apple shares, you don’t have to shop around for the best price. Electronic trading companies have an incentive to build the fastest networks linking financial centers so that prices can move quickly between them. Buyers and sellers benefit because their local market has electronic traders who know the best prices on other markets and will be happy to do a local deal at the best global price (it’s market making). It doesn’t take a rocket surgeon to see the business opportunity in this type of trading, so high-speed traders have to be efficient because they’re competing against each other. The latency race has to happen for each market to have the best price. Competition between electronic traders limits their spend to the benefits that come with better pricing.

#### Why does radio help win the latency race?

Traders use radio because it can move prices faster than optical fiber.

![PenInWater](img/3d79162784bcf62acb86599e551d3ad0.png)

This straight pen appears to bend when it goes below the surface of the water.

I won’t bore you with the physics, but I will remind you of this elementary school experiment where a pencil appears to bend in a glass of water. This happens because light moves more quickly through air than it does through water. In the same way, radio waves move more quickly through air than light can move through an optical fiber. In trading parlance, radio is lower latency than fiber over a given distance.

But radio is also faster because it almost always covers a shorter distance. Fiber paths tend to follow roads and property lines that may not go exactly in the desired direction. Radio towers may be inconvenient, but they give the advantage that the signal can take the shortest-possible path allowed by physics, not the kinky path dictated by rights of way [*I explained that in the now famous “[HFT in my backyard](https://sniperinmahwah.wordpress.com/2014/09/22/hft-in-my-backyard-part-i/)” – SIM*].

The speed advantage of radio adds up as the distance increases. That 4 ms number I mentioned above is the microwave radio time of flight between Chicago and New York. (Well actually, it’s between the Chicago suburb of Aurora and the New York suburb of Secaucus that’s actually in New Jersey.) For comparison, the fastest fiber path on that route was 6.75 ms, for a radio advantage of 2.75 ms. On a Chicago to Europe shortwave path, the radio advantage is more like 10 ms.

The latency saved matters even over short distances. [Bloomberg observed](https://www.bloomberg.com/news/articles/2017-05-12/mysterious-antennas-outside-cme-reveal-traders-furious-land-war) that a trading company had purchased land adjacent to CME, likely to replace a fiber path with a radio path. I measured and found a fiber path length of about 1,400 feet, versus a radio path length of about 1,000 feet. See aerial photo [*I will detail what’s going on around the CME in Part IV, it’s quite amazing – SIM*].

[![RadioVsFiber](img/f871e82a1cf015a01b3bf4ccde5ce80f.png)](https://sniperinmahwah.wordpress.com/wp-content/uploads/2018/06/radiovsfiber1.jpeg)

Replacing 1400 feet of fiber with 1000-foot radio path saves about 1 µs.

The 400 foot advantage may not sound like much, but that works out to about a 1 µs advantage when you take into account both the straighter, shorter path and the faster flight time. That’s only a millionth of a second and may not sound like much, but a zippy Xeon CPU can do about 3,000 instructions in that amount of time. So getting back to the point about efficiency above, traders without the land and hence the shorter radio path have to get the same number crunching done with 3,000 fewer instructions if they want to stay competitive [*That’s what I will detail in Part IV – SIM*]. Returning to the extreme case of shortwave vs. fiber between Chicago and Europe, a trader without shortwave is at a 30,000,000 instruction disadvantage.

#### What’s the difference between microwave radio and shortwave radio?

I’ve been rather cavalier here in comparing shortwave and microwave, even though they’re quite different. Comments on the previous post showed that there’s some confusion that I’ll try to clear up. Most articles on this blog are about microwaves which travel only in a straight line. The line cannot be obstructed by trees or buildings or pretty much anything else. A cup of water gets hot in a microwave oven because the water absorbs microwaves. Trees are mostly water, so they too absorb microwaves. Hence microwave antennas go on tall towers or mountains that clear the tree tops.

As the length of a microwave link gets longer, you need taller towers and larger antennas. You reach a point where it’s smarter to add a relay tower in the middle and make a two-link chain. Relays add some latency and cost, so designing multi-link microwave chains involves many compromises and tradeoffs. The exact number of links in the chain on the 840 mile path from Chicago to New York is a closely-guarded secret for each network, but it’s most likely more than 20, but less than 30.

[![](img/23c1273118f2fd85caa482b91f1ad11e.png)](https://arxiv.org/pdf/1302.5966.pdf)

Some of the microwave networks between Aurora and New Jersey. (From Laughlin, Aguirre & Grundfest paper “Information Transmission Between Financial Markets in Chicago and New York”, 2013)

The microwave links between Chicago and New York cross the southern tips of Lake Michigan and Lake Erie, but they can’t cross oceans because the distances are too vast. For that, you need shortwave or microwave/fiber hybrid networks like [GoWest, covered previously on this blog](https://sniperinmahwah.wordpress.com/2016/09/23/once-upon-a-time-in-the-west/).

#### How does shortwave stack up against microwave and fiber?

Fiber reliability is essentially perfect, but microwave links will have bad days, typically related to weather. Rain, snow, and ice in the path can absorb the transmitted signal before it gets to the receiver. Antennas can be 6 feet in diameter, so there’s a lot of force on them in a strong wind that can knock them off course. Still microwave reliability can be pretty good. Low-latency microwave pioneers McKay Brothers have a saying: “It’s better to be fast 99% of the time than slow 99.999% of the time.”

Shortwave, on the other hand, is much less reliable than microwave, for a variety of reasons. Electrical storms or man-made interference near the receiver can make so much noise that the faint signal from a remote transmitter cannot be heard. Shortwave depends on the vagaries of [Earth’s ionosphere](https://en.wikipedia.org/wiki/Ionosphere), a part of the upper atmosphere. Shortwave signals would typically only go a few hundred miles. But when ionospheric conditions are just right, some small fraction of the signal bounces or “skips” off the ionosphere and is reflected back to Earth, instead of just blasting off into outer space. So traders hoping to use shortwave for trading are at the mercy of many physical forces they can’t control. I couldn’t make any reasonable guess at a reliability percentage, but shortwave is far less reliable than microwave—probably a couple of orders of magnitude less reliable.

Even when the conditions are right for shortwave to work well, I wouldn’t expect bandwidth much better than a dial-up modem. Compare that to a few hundred megabits over microwave and 10’s of gigabits over fiber.

The low bandwidth with shortwave has a subtle consequence: the latency advantage over fiber can easily be consumed by the time taken (serialization latency) to send even a small message measured by fiber standards. The entire 10 ms latency advantage can be consumed by the time it takes to send a single 64-byte packet at dialup speeds. So shortwave traders need to have ways to very tightly encode their prices or other information in just a few bytes or bits—yet another pressure toward efficiency mentioned above.

Bringing all of the above together, we can make a table that compares fiber, microwave, and shortwave.

![FiberMicrowaveShortwave](img/839c54723dda00b862c455b1ba059589.png)

A comparison of fiber, microwave, and shortwave. Green backgrounds highlight relative advantages while red backgrounds highlight relative disadvantages.

The quick summary is that shortwave has the limitless reach of fiber and the lowest-possible latency of microwave, but it’s highly unreliable, expensive, and has the bandwidth of dialup.

When explaining the relative advantages of radio links and fiber, I often use the two gun analogy. Imagine that you are a trader with a message to send to a remote site. You have to write the message on a bullet to send it. You have a “fiber gun” in one hand and a “radio gun” in the other.

Every bullet from the fiber gun will reach the target, but some percentage of bullets from the radio gun will explode in midair and never get there. Bullets from the radio gun fly 1.5 times faster than bullets from the fiber gun. You can pull the trigger on the fiber gun as often as you like, but you have to wait, to reload, after firing the radio gun. The reload time can be milliseconds, opening the possibility of “shooter’s remorse.” You decide to take a shot with the radio gun, then quickly get new information that makes you want to shoot again before your gun has reloaded.

#### If traders send signals over radio, can others hear them?

The threat that has to be considered is a competing company that manages to get a receiving antenna closer to an exchange and figures out how to decode your signal. Not every trade is a winner-take-all opportunity, but no trader wants the cost of their transmitter to benefit competitors.

Encryption is the only answer I see. It’s fast since it only requires that each bit be XORed on transmit and receive with a secret bit pattern known only to the owner of the transmitter and intended receivers. Cryptographers have shown that XORing an information stream with a pseudo-random bit stream produces a new bit stream which is indistinguishable from noise. In other words, all traces of information are removed from the stream. So a receiver that doesn’t have the secret bit pattern can only receive noise.

Given the low data rate on shortwave, the secret bit pattern only needs to be a few MB long for a whole trading day. It only takes a fraction of a second to send this over a secure fiber link while the markets are closed. Better yet, just send a 256 bit seed to a cryptographic-quality pseudo-random number generator and you’re done.

Note that most Internet encryption protocols require lossless transport and so they won’t work on lossy shortwave. This is easily handled by advancing the encryption bit stream by GPS clock rather than by bits received.

#### What about satellite?

Geostationary satellites are out of the question for trading. Lots of bandwidth, but it takes 270 milliseconds to travel the distance to the satellite and back. Physics gets in the way.

Low earth orbit satellites are a possibility because they fly so much closer to the earth. I’m not aware of any constellations flying today that would be suitable for trading. Some on the drawing board might sometimes have a latency advantage over fiber under oceans. But none are an unconditional win over fiber because the path length changes as the constellation moves relative to the ground stations. See the talk by Stéphane Tyč of McKay Brothers for more info on [the possible use of satellites for trading](https://stacresearch.com/STAC-Summit-1-Nov-2017-mckay).

The ionosphere is closer to earth than the lowest of the low-earth orbit satellites, so shortwave will always have a shorter hypotenuse, and hence lower latency, than satellite. However, microwave signals just graze Earth’s surface so chained microwave links are lower latency than shortwave, over the mostly-land paths where they’re possible.

#### Are you spilling secrets?

No. The possibility of shortwave trading has been discussed on this [blog](https://sniperinmahwah.wordpress.com/2015/01/14/hft-in-my-backyard-v/) and on [Meanderful](https://meanderful.blogspot.com/2017/05/lines-radios-and-cables-oh-my.html). I’ve just figured out how to find the FCC licenses in public records. The antennas are too big to hide. I’ve combined the above with maps, background info, and my analysis. It’s really no surprise, given that people want to have the best prices close to them so there will be a latency race. We should expect trading technology to shoot directly for the lowest latency allowable by the laws of physics. Put simply: Business + Physics = Shortwave.

#### When did this all start?

Some expired experimental licenses date back to late 2011\. However, software defined radios have come a long way since then. The current round of license applications were sent in mid- to late-2015 [*this is when I first heard about these projects– SIM*]. The towers in Indiana, discussed above, were built between October 2016 and April 2017.

In March 2018, I photographed the cardboard box for the software defined radios used at the [West Chicago tower](https://sniperinmahwah.wordpress.com/2018/05/07/shortwave-trading-part-i-the-west-chicago-tower-mystery/). It was sitting in the garbage pile, on top of a pile of leaves that were not badly decomposed, so I assume it was installed after the fall of 2017\. Further, the box was exposed to the elements of a Chicago winter and didn’t seem to be in bad shape at all. So I’m going to guess that it was actually installed more like February 2018\. Fresh stuff.

#### What else have you found around Chicago?

I went to the FCC Experimental license database and found nine current hits for shortwave licenses within 100 miles of CME’s data center in Aurora. Two were bogus; one was the West Chicago site I stumbled onto. I visited four sites and found no shortwave antennas there. But that still leaves two interesting sites.

The first is near Wanatah, Indiana ([41.457048°, -86.859156°](https://www.google.fr/maps/place/41%C2%B027'25.4%22N+86%C2%B051'33.0%22W/@41.457048,-86.8613447,713m/data=!3m1!1e3!4m5!3m4!1s0x0:0x0!8m2!3d41.457048!4d-86.859156)). This site looks interesting from above.

[![WanatahAerial](img/1f0f57bd5ca0dfdefb47d58b0594f67a.png)](https://sniperinmahwah.wordpress.com/wp-content/uploads/2018/06/wanatahaerial.jpg)

Compare the size of the antenna to the farmhouse and the 18-wheeler.

You can see a large square area of the cornfield that looks different. There’s an access road leading to a light-colored part of the square. Note the sizes relative to the farmhouse and the 18-wheeler to see the scale.

![](img/ec613ad466d253850be70f808a6f87f4.png)

That looked promising so I drove there and took this picture from the road at the bottom of the aerial shot above.

![WanatahFromRoad](img/2e7693a6c956ea14b428ff4ca0850308.png)

Wanatah antenna site as seen from nearest country road.

[The FCC database](http://wireless2.fcc.gov/UlsApp/AsrSearch/asrRegistration.jsp?regKey=2697146) says those two towers are 160 feet (49 meters) tall. They hold four monster log-periodic antennas according to [another FCC database](https://apps.fcc.gov/oetcf/els/reports/442_Print.cfm?mode=current&application_seq=66454&license_seq=67065). I could see from the feed line that the antennas were configured to operate as a single large antenna. The license shows a 10 kW transmitter with an effective radiated power (ERP) of 768 kW due to the antenna gain. The database also confirms what you can see by eye in the aerial photo: the whole antenna site is pointed at a 50º angle, which solidly hits Europe with the 26º beam width of the antenna.

There’s a microwave dish on one of the towers. FCC licenses show the tower owner has a series of three microwave hops west to a site in Oak Forest, Illinois.

![](img/7b8b58c07dbbfc9eb9094f400122ada2.png)

[![OakForest](img/0a0e355964bf3d4fbcab21f95cb73472.png)](https://sniperinmahwah.wordpress.com/wp-content/uploads/2018/06/oakforest.jpg)

Office building in Oak Forest, Illinois where Wanatah tower owner’s microwave licenses stop.

This is a point of presence for a local wireless ISP [UrbanCom.Net](http://UrbanCom.Net) which also has an antenna on a tower adjacent to CME. My hunch is that the shortwave trader just buys bandwidth from UrbanCom for the rest of the path from Oak Forest to CME [*When I parsed the FCC documents about the Wanatah facility, I was quite amazed to find the first name of an individual I like, that’s how I could figure out which trading firm is behind County Information Services, LLC, who built the antennas  – SIM*].

The second site is just outside of Elburn, Illinois ([41.926495, -88.499110°](https://www.google.fr/maps/place/41%C2%B055'35.4%22N+88%C2%B029'56.8%22W/@41.926495,-88.5012987,858m/data=!3m1!1e3!4m5!3m4!1s0x0:0x0!8m2!3d41.926495!4d-88.49911)). [The antennas here](http://www.datasheetarchive.com/pdf/download.php?id=5929674a837d08b565e6eb6c51022c2bc51d42&type=M) are log periodic like the others, but their structure is fundamentally different. Instead of using rigid aluminum tubing, this antenna is made from comparatively thin wire that is pulled taut by ropes and springs. The ropes attach to tall supporting trusses and to ground anchors to hold them in tension. This style of antenna is difficult to photograph because the wire doesn’t need to be very thick. I’ve overlaid blue surfaces on the photo to show the planes of the two stacked antennas.

![Elburn](img/9f0bce83011b1c5eaf392c3e0026fe34.png)

Shortwave trading antenna site near Elburn, IL. Blue highlighting shows planes of antenna wires.

A search of [the FCC experimental license database](https://apps.fcc.gov/oetcf/els/reports/442_Print.cfm?mode=current&application_seq=73823&license_seq=74541) shows this site is licensed (by a firm named 10Band LLC) for a 20 kW transmitter with an ERP of 808 kW. The shortwave antenna is pointed at a 48º angle and Europe is well within the 38º beam width.

There is clearly a microwave dish antenna at this site, but I haven’t yet been able to find the FCC license for it. But I have been able to get a heading for the dish by taking GPS coordinates of photos taken along the beam path. It points at CME.

[*When Bob and I started to map the shortwave antennas using the FCC database coordinates, my first move was to “watch” the facilities using Google Earth. For the Elburn site it’s useless…*

![](img/ac7a992565acca24f11065f4631c91dd.png)

Elbun, picture from Google Earth, 21/9/2015

*… but thanks to this picture we learn the antennas were not there in September 2015\. Someone told me to check another satellite imagery [website](http://gistech.countyofkane.org/PictometryIPA2/example.aspx?txtLat=41.9272686056401&txtLng=-88.498045437168159), which is more up to date than Google Earth, and the antennas are there:*

*By digging into the archive pictures, it seems like the antennas were erected in Elburn after May 2016\. I got another picture of the site, sent by someone who wants to stay anonymous. I really don’t know who is he, but he has a lot of pictures of the various “HFT” shortwaves antennas, both in US and UK…*

![](img/50f8ec006bd2eddb61f97967e4d26b5c.png)

Elburn, picture from someone

*That said, Bob’s picture below is more beautiful:*

[![](img/49bce0456b211bd97e09b7f0f3569e55.png)](https://sniperinmahwah.wordpress.com/wp-content/uploads/2018/06/10band.png)

Elburn, picture from Bob

*Last but not least, as always I was curious to know which trading firm is hiding behind the name 10Band LLC. Someone found that for me and sent me this ”Kane County Property Tax Inquiry“ [link](http://kaneil.devnetwedge.com/parcel/view/0724300005/2017), where we can learn that the field where the antennas were erected was sold in 2011 for $1,338,325.00 to 10Band LLC, a firm in Chicago – I smiled when I recognized the address – SIM] *

#### Are you sure these antenna sites are really for shortwave trading and not a beacon for space alien body snatchers or something else?

I’m going to assume that space alien body snatchers wouldn’t bother with FCC licenses for their beacons. The sites I’m documenting here are all licensed to transmit on shortwave frequencies that could cross oceans.

![Summary](img/35976a2733ae2fbd9a5593fa5c086fd7.png)

Shortwave trading sites around Chicago. Solid lines are paths to London. Dashed lines are microwave links with CME.

Their shortwave antennas are all pointed at Europe. They all have a microwave link to CME. The IEEE Spectrum article on shortwave trading has deep links into the FCC database revealing the name of a trading company owning one of these sites.

#### What’s next?

I’m headed to the areas around New Jersey data centers to see if I can find shortwave antennas there.

#### Post-scriptum

[*Nothing to do with shortwave trading here, but thanks to Bob I had a lot of fun with this [website](http://www.micronetcommunications.com/LinkRegistration/QueryResults.aspx). In the US the FCC database does not include the licences for millimeter waves – millimeter wave frequencies are often less crowded than microwave frequencies, so millimeter waves are interesting in urban environments. Traders use millimeter waves both in London and Chicago. I searched for all the millimeter waves licences around Aurora and got a long list starting with this:*

![](img/5c61a8f6af4bc5e601fe3561f5696dd8.png)

*Boring, but I clicked on the* kmz *button and got quite an amazing Google Earth map (click to enlarge):*

[![](img/4a9e2043c53498e45bc7c6108e90b40a.png)](https://sniperinmahwah.wordpress.com/wp-content/uploads/2018/06/aurora_3d.jpg)

Aurora <-> Cermak

*This map shows all the millimeter waves licences going from Aurora (CME) to Cermak (ICE) – including old licences that are far from the straight line between the two data centers. The line of sight is in yellow, and the first Fresnel Zone is in red. *

[![](img/af2a1303ca2bbe364a4974b43b020a6f.png)](https://sniperinmahwah.wordpress.com/wp-content/uploads/2018/06/capture-d_c3a9cran-2018-06-07-c3a0-12-11-30.png)

*Then I searched the licences for the (New Jersey) Equity Triangle (Mahwah-Secaucus-Carteret). From above the triangle looks like that…*

![](img/6d3260044de98420c313f727ef5fe351.png)

The Equity Triangle

*…but it’s more amusing to watch it more closely:*

[![](img/d399d7c1961b01988c99f988c1cb0ff8.png)](https://sniperinmahwah.wordpress.com/wp-content/uploads/2018/06/capture-d_c3a9cran-2018-06-07-c3a0-12-44-11.png)

The Equity Traingle millimeter waves networks, from Carteret (at the bottom)

[![](img/0450fb75f098d5aa8e1b7a8fa8c43b1b.png)](https://sniperinmahwah.wordpress.com/wp-content/uploads/2018/06/capture-d_c3a9cran-2018-06-07-c3a0-12-29-55.png)

The Equity Triangle millimeter waves networks, from Secaucus (at the bottom)

*By the way, I say hello to the boss of the China cat! Perhaps the cat is somewhere in this 2160p video made with a drone in my backyard:*

 [https://www.youtube.com/embed/e7ocPoizZGM?version=3&rel=1&showsearch=0&showinfo=1&iv_load_policy=1&fs=1&hl=en&autohide=2&wmode=transparent](https://www.youtube.com/embed/e7ocPoizZGM?version=3&rel=1&showsearch=0&showinfo=1&iv_load_policy=1&fs=1&hl=en&autohide=2&wmode=transparent)

VIDEO

*That’s all folks – SIM*]