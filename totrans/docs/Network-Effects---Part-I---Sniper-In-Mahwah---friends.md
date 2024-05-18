<!--yml
category: 未分类
date: 2024-05-18 14:08:50
-->

# Network Effects | Part I – Sniper In Mahwah & friends

> 来源：[https://sniperinmahwah.wordpress.com/2017/06/07/network-effects-part-i/#0001-01-01](https://sniperinmahwah.wordpress.com/2017/06/07/network-effects-part-i/#0001-01-01)

##### INTRODUCTION

Since every ~~microsecond~~ nanosecond counts in our life, at the present time I have to spend each microsecond to other works rather than writing here about high-frequency trading and/or the world of microwave. That’s the reason I decided to offer the opportunity to different people involved (or not) in the HFT industry to write here. I thought the motto of this blog may become “*Where capital markets speak*” but another [organization](https://twitter.com/TabbFORUM) already took the headline – too bad. Anyway, I’m happy a couple of people agreed to replace me. Here is the first part of a new series, *Networks Effects*, written by my first guest I’m delighted to welcome here. I only slightly edited the text (a couple of photos, a few links, etc.) and added comments within [brackets], signed SIM. Happy reading.

##### NETWORK EFFECTS | PART I

Early last month, a reporter called me with a curious question.

“I’ve learned that Jump recently purchased a 31-acre field just across from the CME’s match in Aurora. And they paid a lot. Like $14 million, apparently. Any idea what could be going on?”

Prime Illinois farmland produces of order 200 bushels of corn per acre per year. At 4 dollars a bushel, Jump Trading LLC – the opaque high-frequency powerhouse, with the blank silvery [website](http://www.jumptrading.com) and the Twitter [account](https://twitter.com/jumptrading) with no tweets – could be looking at a cool $25K in yearly agricultural revenue from their parcel. 

“Which side of the data center?” I asked.

“It’s due North.”

Carteret, Mahwah, Secaucus, 350 Cermak and CoreSite all lie east or slightly southeast. North is not on the geodesics.

“Could be a shortwave set up?” I ventured, after a pause, but more or less completely at a loss. “Maybe they’re encrypting the E-mini ticks on one-time pads and broadcasting them worldwide. Tokyo, London, Frankfurt, Singapore, Sao Palo. Hey, are you on-line?”

He was.

“Pull up the Google Images of the `Rampisham Short Wave Radio Station’,” I said, “You’re looking for something like that; a field growing antennas instead of corn. If you drive out to Aurora and take pictures, it’ll give a sense of what they are up to.”

The next day, the photos popped up on my screen.

[![](img/e1cb2b812d1c4d0147786f4966a6e147.png)](https://www.bloomberg.com/news/articles/2017-05-12/mysterious-antennas-outside-cme-reveal-traders-furious-land-war)

Source: Brian Louis/Bloomberg

Jump’s newly purchased field was a bleak unplowed expanse, a jumble of early spring weeds. In the distance, trucks are visible, roaring by on I-88\. Fermilab is just over the horizon, having produced, for tiny flickering moments in the defunct 2 kilometer-wide Tevatron, temperatures that existed during the first microsecond of the Universe’s existence.

In the extreme southeast corner of the field stood a Kohler portable generator, a short, stubby pole with a millimeter-wave radio unit, and two small dish antennas pointing northeast.

***

More than a decade ago, I *did* know about Getco, and indeed, had marveled at the sheer audacity of that name. A friend of mine, a fellow physicist, worked at a 1990s-era desk that pioneered [statistical arbitrage](http://www.hedgefund-index.com/d_statarb.asp) and early versions of high frequency trading. In that now-distant time, split-seconds, open phone lines, and human reaction times were all still relevant. I knew that servers were migrating to co-location in data centers to gain proximity to the exchanges. I’d heard the delicious rumors of the staggering PNLs that a collection of firms, mostly located in Chicago, were generating. “$1M per day”, “Effectively infinite [Sharpe](http://www.investopedia.com/terms/s/sharperatio.asp).” [Once I read in a court document that a big “HFT” firm in Houston, in its early stages, around 2001, had a Sharpe ratio of a 20 to 40, “*which is extraordinarily high*” – SIM].  In late 2007, a person, perhaps in position to know, and after one too many margaritas, let slip what sounded like a key to a castle, “ETFs, Man, we’re unpacking the ETFs and arbing ‘em against the underlying.’ A few weeks later, a successful trader, completely sober, remarked cryptically, “Order of magnitude*, you need to think in dollars per millisecond*.” Another, “Read Lefevre’s [book](https://en.wikipedia.org/wiki/Reminiscences_of_a_Stock_Operator). Everything in there still works.” It was a view through an imperfect, entirely incomplete window into a mysterious exhilarating world that was completely out of reach.

Can a sprawl of clues and misinformation be arranged to form a glimpse of how HFT actually works? A few simple principles appeared to interpolate consistently through the rumors. (1) If latency is an issue, then the time scale over which one’s predictions are valid has to be short. That is, if you can somehow predict where a stock is going to be priced next week, then your concern is with order working and market impact, not with microsecond latencies or nanosecond time stamps.  (2) There’s simply no time to solve complicated equations during production. In the co-lo cage it has to be about heuristics and lookup tables. (3) The [Central Limit Theorem](https://en.wikipedia.org/wiki/Central_limit_theorem) and the [Law of Large Numbers](https://en.wikipedia.org/wiki/Law_of_large_numbers) will work to one’s advantage. Diffusion scales with the [square root of time](http://www.macroption.com/why-is-volatility-proportional-to-square-root-of-time/), so VIX of 20 deannualizes to price-changing tick on the E-mini every few seconds. So [queue positioning](https://www.kcg.com/uploads/documents/KCG_NeedForSpeed1-Report.pdf) must be critical, and market making, or its high-tech equivalents *must* be a core component of HFT.

***

The infamous Forbes [article](https://www.forbes.com/forbes/2010/0927/outfront-netscape-jim-barksdale-daniel-spivey-wall-street-speed-war.html) about Spread Networks was published in September 2010, but I didn’t see it until the first week of November, and so it’s clear that others had long since formulated all the thoughts I immediately had upon reading it: For a fiber that was so straight and so expensive, why was the Chicago to New York round trip travel time so excruciatingly slow? The distance is about 1200 km, so the minimum one-way signal propagation time should be about four milliseconds, not seven. Then I remembered from second-semester physics that the index of refraction in glass is something like *n*=1.5… Confusion.

Isn’t it faster and cheaper to send the signal through the air?

 A crash Google course in radio-frequency communication – a topic that I knew literally nothing about – suggested that there would be no show stoppers to either relaying a signal with a chain of microwave radios, or, at almost zero cost, using meteor burst communication. After convincing myself that I’d done enough due diligence to not make a fool of myself, I sent an e-mail floating those two schemes to a retired communications engineer whom I knew slightly. A week or so later, he wrote back.

> I think that the idea of using a radio link seems a good idea and could work, but I believe there may be some problems with doing it by meteor scatter. To my way of thinking, a standard microwave relay link chain may be the best bet, and there’s a possibility of using a two-hop tropospheric scatter link.
> 
> Keep in mind that radio has two separate issues: technical feasibility and obtaining use of the spectrum. For something like this, I’d guess cost would not be overwhelming. Another issue is whether the protocol used requires a response from the distant end, or whether that can be eliminated through some cleverness so the latency is essentially “open loop.”
> 
> First, about meteor scatter. The standard meteor scatter link has the unusual characteristic that the reflection from the ionized line doesn’t have the same geographic coverage as an ionized plane would, and so the number of useful meteor trails between two locations is greatly less than the total rate of meteors. Typical links are very narrow band, partly because they are generally low power. So a higher power link might resolve the burst rate issue, but even then, I believe there would not be sufficient aligned paths to provide real-time service.
> 
> A more sure-fire way would be to use the relay sites that were once employed in the old AT&T Long Lines 4 GHz and 6 GHz networks.
> 
> [![](img/52a919f6d26eadc7ca0c7a94147d766b.png)](https://www.reddit.com/r/technology/comments/fxuk2/this_is_a_map_of_the_1960s_era_att_long_lines/)
> 
> Many of these were up for sale a while ago, and I’d guess they have been acquired by outfits that lease tower and building space. In this situation, you could expect to have reasonable bandwidth, and the latency would of course be determined by the velocity of light in air, plus a little for the plumbing and circuitry. Modern equipment for this service is available, as are the antennas and feedlines. Because of the greater bandwidth and flexibility, and lower cost, of optical fiber, there hasn’t been a market for this particular technology. But I think the Chicago-New York one-way latency would be in the range of 4 ms for the 700 mile distance. See [http://long-lines.net/places-routes/1st_transcon_mw/LL0949/02.html](http://long-lines.net/places-routes/1st_transcon_mw/LL0949/02.html)
> 
> There are unlicensed 5 GHz bands that could provide this service, or it could be in the licensed bands of 4 and 6 GHz. There would possibly be some fade outages, but the system could be engineered against that.
> 
> Another possibility is a two-hop [troposcatter](http://www.militaryaerospace.com/content/dam/mae/online-articles/2013/07/Troposcatter%2026%20July%202013.jpg) link. This requires big antennas and high power, but that’s all been developed for satellite earth stations. There are 20 MB military systems, but the maximum range per hop is 400 miles, so you’d need an intermediate point. Given the reliance on the troposphere, there can be some outages, but the availability might be enough to be useful.

This reply seemed encouraging. I kept digging. Being two-hop, and nearly geometrically optimal, the troposcatter scheme looked like it would be the fastest option. A survey of the troposcatter provider websites, however, showed infrastructure that invariably ran to armored Humvees, ominously large dishes, shipping container-sized generators, and camouflage netting. The prospects of orchestrating the parking of such rigs in downtown Chicago seemed remote.

Microwave dishes on communication towers, however, are ubiquitous. They are so much a part of the landscape that one hardly notices them [that’s the reason I got interested in the HFT microwave world – SIM]. I sent out more inquiries, floating various ideas. Looking back through my notes, I have a printed-out e-mail from an engineer friend, dated December 8, 2010, that was remarkably prescient:

> Very interesting.  It got me thinking of other ways to pull it off.  Here’s an idea that is even less far-fetched. You could just use unlicensed spectrum, such as that used for Wi-Fi, and set up a mesh network and the number of hops you need.
> 
> I did some poking around online. There’s a company that sells spectrum license-exempt base-station equipment with up to 30km range.  The main purpose is enterprise or municipal/rural Wi-Fi networks.  But with that kind of range you could conceivably set up around 40ish hops to get from NY to Chicago.  I’m not sure how much latency would be introduced on each hop, but I’m guessing no more than 20us.  At my previous job I worked on hardware processing of the entire network stack (TCP/IP) and the internal latency was well under 5us.  Using a conservative figure of 20us per hop adds an additional 800us (1.6ms round-trip) to the 8ms speed-of-light time.  Still brings you in under 10ms total, which compared to the 13ms in the article is certainly a competitive advantage.   Also, the bandwidth should be respectable, something on the order of megabytes.  Nothing like fiber, but certainly enough to communicate trade information for some limited set of symbols.  The other advantage would be that it is somewhat scalable.  You could build multiple point-to-point hop links.  Since this stuff is line-of-sight, you could easily have parallel networks along very similar paths.  This would not only increase bandwidth, but add redundancy and reliability to the network.  The cost of this solution would be pretty minimal if the available products have reasonable performance.  I found another company, American Tower, that rents antenna tower space for cellular and radio (think of it as antenna hosting, similar to data-center hosting).  It seems like all the pieces are there to just go out and slap a solution together.  I’ve got to think the big players have done this, but again it’s one of those things that you could read about in the paper some day and think holy shit, we talked about that! After all, we talked about the tunnel to Chicago, and it turns out someone built it. And the minute it gets out that someone has done it, there would be a flood of people doing it, since it’s low-cost and straightforward.  The Wi-Fi spectrum along the straight-shot from NY to Chicago would get so crowded that nobody in rural Pennsylvania and Ohio would ever be able to use their Wi-Fi.  I’m sure at that point the government would have to step in.  So even if someone is using Microwave, I’m guessing the Wi-Fi idea is less likely.  There’s nothing liking hiding a top-secret super-low latency network in plain sight!

My last notebook entry from 2010 is a fragment with no attribution that had been forwarded, as if by a two-hop troposcatter link, from someone who was reportedly working in the industry.

> Actually… There is a Chicago firm that uses microwave to go over a town/area on the way from Chicago to NYC. (apparently some telco firm controls the switches in this area and they would have to go around so they decided to go over) supposedly their times are 13.9 vs 15 for the Spread Network direct line (and 16.5 for regular line)

Something about that last entry must have seemed confusing and daunting, and my interest drifted elsewhere for the next ten weeks.

###### A we say in French: “à suivre…”