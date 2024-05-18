<!--yml
category: 未分类
date: 2024-05-18 14:17:46
-->

# A quick note – Sniper In Mahwah & friends

> 来源：[https://sniperinmahwah.wordpress.com/2014/12/02/a-quick-note/#0001-01-01](https://sniperinmahwah.wordpress.com/2014/12/02/a-quick-note/#0001-01-01)

A new academic paper about HFT titled [*High Frequency Trading and Extreme Price Movements*](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=2531122) came out on November 26, 2014\. Led by Jonathan Brogaard (University of Washington), Ryan Riordan (Queen’s School of Business), Andriy Shkilko and Konstantin Sokolov (Wilfrid Laurier University), the study focus on “the relation between high-frequency trading and extreme price movements” and conclude that HFTs perform a “stabilizing function in markets during periods of stress”, when prices move more than usual – in short, the paper claims that in volatile times HF traders don’t vanish and still provide liquidity. As usual, as soon as a new academic paper is published about high-frequency trading, the tension escalates and the findings are debated. Yesterday Themis Trading (not a pro-HFT) published a response to this paper, and [others](https://twitter.com/RemcoLenterman) replied to the response, and so on (by sheer coincidence,  Apple’s stock went wrong for a minute yesterday, allowing Matt Levine to write this [post](http://www.bloombergview.com/articles/2014-12-01/apple-had-a-rough-morning) both about Apple and this new study).

I won’t dispute the conclusions here as the way some HFTs disappear (or not) in volatile times is a very debated issue – even among academics. But in my (humble) opinion and once again, this new study (like others) raise questions about 1) the data set used and 2) the definition of “a HF trader”. The first thing I noticed is that the data set used study is the same Jonathan Brogaard, Terrence Hendershott and Ryan Riordan used for another article titled “[High Frequency Trading and Price Discovery](http://faculty.haas.berkeley.edu/hender/HFT-PD.pdf)” published earlier this year (but the first version of of the paper was available from [April 2013](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=1928510)). This data set, provided by Nasdaq, may be one of “the few U.S. datasets that identifies the trader types” but span 2008 and 2009 – in other words, the data is quite old. What’s more, it only includes 26 “firms that act as independent HFT proprietary trading firms”. That means some big banks having HFT desks are not included. Since these banks may be both non-HFTs and HFTs, it’s therefore normal to exclude them in order to have a more accurate data set by excluding non-HFTs activities, but that also means some data is missing.

Furthermore, the definition of a HF trader is rather ambiguous since it’s Nasdaq who “determines whether a participant is an HFT firm based on its knowledge of the firm’s activity”; so we have no information about the Nasdaq definition of a “high-frequency trader”. The new study states that “a firm is **more likely** to be identified as HFT if it trades frequently, holds small intraday inventory positions, and ends the day with **nearly zero inventory **[my bold]”. The words come from the authors, not from Nasdaq. Fair enough, but by discussing recently with the CEO of a big market maker (operating both in Europe and the US), I learnt the firm has huge overnight positions: several billion dollars. Even if these positions are not “directional” (in the sense that long/short positions are hedged with short/long positions – *i.e.* the positions are not liquidated, only the risk is liquidated), this major market maker doesn’t finish a day with a flat inventory. The question, then, arises: electronic market makers being HFTs (but not all HFTs are market makers), is this big market maker included in the Nasdaq data set? The answer is “yes”, but that means the definition of a “HF trader” given by the authors is probably not the one of Nasdaq (“nearly zero inventory” *versus* huge overnight positions). The way people define HFTs versus non HFTs is a crucial issue and I think one would expect more precise definitions.

So, the data set is old, includes 26 (prop) firms only and the paper studies 40 of the major stocks (by market capitalization). One of the author, Andriy Shkilko, admitted yesterday on [Twitter](https://twitter.com/AndriyShkilko/with_replies) that “there are no other large nonproprietary data on HFT available to” the academics, adding that “newer more extensive datasets have been hard to come by”, and that’s true. Data is missing (besides, I have been told that some data – from the CME for instance – is quite expensive), and that’s problematic. Just a few words about the Brogaard, Hendershott and Riordan study released last year, “[High Frequency Trading and Price Discovery”](http://faculty.haas.berkeley.edu/hender/HFT-PD.pdf). Again, I don’t dispute the conclusions of the study (HFTs improve price discovery) but this paper had a strange career. The first draft was posted in April 2013, and in November 2013 you could find it on the European Central bank [website](http://www.ecb.europa.eu/pub/pdf/scpwps/ecbwp1602.pdf) as a “working paper”.

It was strange because the ECB states that “this Working Paper should not be reported as representing the views of the European Central Bank (ECB). The views expressed are those of the authors and do not necessarily reflect those of the ECB.” It was strange because the data set used by the authors (the same as the one used for the new study published last week) includes “120 randomly selected stocks listed on NASDAQ and the NYSE”… nothing to do with stocks listed on European markets/MFTs/etc. Then the ECB version of the study was echoed by the [Financial Times](http://www.ft.com/intl/cms/s/0/82f5d7fe-4554-11e3-b98b-00144feabdc0.html#axzz3KlFgVIa1): “The ECB said the views expressed in the working paper were those of its authors and not necessarily those of the ECB. But the study’s conclusions could influence the thinking of the Frankfurt-based central bank, which is taking greater responsibility for bank supervision.” That’s interesting because the *FT* titled the article “High-speed trading ‘aids efficiency’, **ECB says**” [my bold]. Look at how an academic article studying HF traders and 120 stocks listed in the US suddenly became relevant for the EU market microstructure, whereas US and EU market structures are quite different. It is not the fault of the authors here, but the fact ECB put the study on their website conducted some journalists to write that “HFTs help price discovery” in general, and that’s a little bit problematic – again, no matter the truth, I only talk about the way a 2008-2009 US small data set become an absolute truth for some people in 2013.

Last week I was in Copenhagen for a workshop titled ”[Investigating High-Frequency Trading. Theoretical, social and anthropological perspectives](http://info.cbs.dk/crowds/workshop_series_investigating_high_frequency_trading)“. Most of the speakers were not from the HFT industry (they were mainly sociologists) but one representative of Bank of England was there. His presentation covered “material from two research papers on high frequency trading currently under production at the Bank of England. Both papers use unique transaction-level data from the UK equity market”. The talk was very interesting in the sense that these two studies “show how the informativeness of trades varies in the cross-section of HFT firms and also whether and how HFT activity is correlated within stocks and what this means for price efficiency”. I can’t seriously make a report with the notes I took (the studies compare passive *versus* agressive HFTs, intraday activities, etc.), but what was surprising is the fact the data set used only include the activities of 10 HFT firms – not even 26\. The two papers should be released in the public domain in the next couple of weeks, and I bet these studies will be much discussed.