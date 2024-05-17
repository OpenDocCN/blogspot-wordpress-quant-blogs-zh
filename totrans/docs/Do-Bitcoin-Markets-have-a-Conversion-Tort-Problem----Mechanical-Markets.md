<!--yml
category: 未分类
date: 2024-05-18 06:38:05
-->

# Do Bitcoin Markets have a Conversion Tort Problem? | Mechanical Markets

> 来源：[https://mechanicalmarkets.wordpress.com/2017/11/05/bitcoin-nemo-dat/#0001-01-01](https://mechanicalmarkets.wordpress.com/2017/11/05/bitcoin-nemo-dat/#0001-01-01)

In many jurisdictions, a buyer of stolen goods does not acquire their legal title. This principle, “[nemo dat](https://www.artsy.net/article/artsy-editorial-how-not-to-sell-stolen-art)“, often applies regardless of whether the buyer knows the goods were stolen. The rightful owner can sue the current holder and take possession.

Bitcoins (and other cryptocurrencies) are [well-known](https://www.theguardian.com/technology/2014/mar/18/history-of-bitcoin-hacks-alternative-currency) to be stolen in large quantities. Bitcoin thieves are usually hard to identify or outside the reach of developed markets’ courts, so victims believe they have no recourse. But the Bitcoin blockchain allows coins to be traced with high precision, and it seems possible for stolen coins to be returned once they re-enter the regulated domain. I’m not a lawyer and don’t understand the relevant intricacies, so this post is just intended to start a discussion. I may be wrong, but buying coins of unknown provenance could be a major risk for Bitcoin holders and intermediaries.

# Pro-rata Tracking

All transfers between Bitcoin addresses are recorded and publicly accessible. In principle, this audit trail should make it easy for victims to track stolen coins and reclaim them if they enter the custody of an identifiable entity. There are, however, a few complications. Bitcoin transactions can have multiple inputs and outputs, so if only some inputs are stolen, it may be difficult to determine the portions of the outputs that should be returned.

Bitcoin is frequently called “[digital gold](https://www.theverge.com/2015/6/10/8751933/the-shy-college-student-who-helped-build-bitcoin-into-a-global),” and perhaps that analogy is useful for tracking ownership across multi-party transactions. As a toy example, say that Tom steals 1 bar of gold from Val. Tom then melts Val’s gold, combines it with another bar of gold, and sells the two resulting bars to unsuspecting buyers, Bob and Barbara (who buy 1 bar each). How should we determine how much of Bob’s and Barbara’s purchases belong to Val? I think the intuitive choice is that each of them should return half a bar. This pro-rata allocation seems fair even though we don’t know which of the individual gold atoms were previously Val’s, or how thoroughly Tom stirred the melted gold.

In some circumstances there could be documentation that suggests an alternate allocation. Suppose Tom steals a bar from Val, then entrusts it to a gold broker, who melts it with other bars. The broker then sells a bar of the blended gold to Bob on Tom’s behalf, recording a trade between them, and giving Tom the cash. Even though “Bob’s” bar doesn’t contain the same gold atoms as Val’s did, perhaps a sensible outcome is for Bob to return the entire bar to Val?

Applying the same intuition to Bitcoin, we could determine which current holders should return which fractions of their holdings, to which victims. The default flow of ownership would be pro-rata, unless there’s documentation proving otherwise — such as trades facilitated by an exchange with client coins in its custody. [[1](#bottom1btcnemo)]

# Legal Venue

Every jurisdiction deals with this liability differently. Many don’t follow “nemo dat” at all, instead using versions of the “market overt” rule. [[2](#bottom2btcnemo)] Other venues only return stolen property if it’s tangible. [[3](#bottom3btcnemo)] The statute of limitations can vary dramatically between venues. Another question is to what extent a “merchant exemption” applies to misappropriated coins. [[4](#bottom4btcnemo)]

So, could lawsuits proceed in a victim-friendly venue like New York? You can argue that Bitcoin is inherently pan-jurisdictional. Bitcoins’ value derives from the consensus of participants on the network, who download the blockchain to confirm that coins are authentic and not part of a fork. If some coins were left out of the version downloaded by NY residents, those coins would be worth much less. Thus, every coin’s value is dependent on NY activity. [[5](#bottom5btcnemo)]

# Potential Consequences for Market Participants

If the above reasoning applies, then victims have a good chance of recovering their stolen coins. It’d be logistically complex, but I can imagine a group of victims demanding that major exchanges, custodians, and intermediaries return the appropriate amounts, if coins with certain address-chains come into their control.

If enforced by a powerful court, demands like this could have serious effects on the Bitcoin market. Many people would have coins — that they innocently bought — seized. These people might then sue their counterparties and exchanges. Depending on the number of stolen Bitcoins circulating, some exchanges could go bankrupt (if they have assets within the reach of the relevant court). OTC market makers, which may account for over half of volume [[6](#bottom6btcnemo)], could have massive liabilities to their customers.

Bitcoins would have different values depending on their transaction history. [[7](#bottom7btcnemo)] Coins considered “suspicious” [[8](#bottom8btcnemo)] or sold without a guarantee from a well-capitalized counterparty [[9](#bottom9btcnemo)], might be worth much less than freshly mined ones. In an extreme case, the market could cease to function until the provenance of enough Bitcoins is publicly known. And perhaps future transactions would have to be fingerprinted and authenticated though an ancillary blockchain.

# National Stolen Property Act

Is it possible that it’s a crime to knowingly sell (or transmit) stolen Bitcoins? I have no understanding of this, but **if you’re worried you possess stolen coins and want to sell them, you may want to consult a lawyer first**. The National Stolen Property Act could [apply](https://www.justice.gov/usam/criminal-resource-manual-1312-national-stolen-property-act-goods-wares-merchandise) to intangible goods, and I don’t want to hear about any readers of this blog going to jail.

# Bringing Transparency to Bitcoin

Established [institutions](https://www.bloomberg.com/news/articles/2017-10-31/cme-group-world-s-biggest-exchange-plans-bitcoin-futures) are trying to make Bitcoin a more trustworthy asset. That requires knowing that marketable coins have similar values and are legitimately owned, as well as reducing the incentives of crime. There’d be some pain involved in reversing past thefts, but it may be better for the Bitcoin community to deal with these issues sooner rather than later.

[[1](#1btcnemo)] Some Bitcoin exchanges may not keep good records of counterparties to trades they facilitated. Perhaps the allocation method should be pro-rata in these cases, i.e. anyone with Bitcoin in the custody of such an exchange has their coins partly tainted when stolen coins are deposited at the same exchange address. This may feel unfair to the innocent depositors at the exchange, but it does seem a lot like a shady gold broker combining legitimate with stolen gold, and returning the blended product to innocent customers. Customers may feel bilked when a victim of theft reclaims gold that the customers believed was theirs, but that’s the fault of the broker, who should compensate them.

This method makes particular sense in the extreme case of a Bitcoin exchange that intentionally loses records, which is arguably similar to a “[mixer](https://en.wikipedia.org/wiki/Bitcoin_mixer).” In the gold analogy, a “mixer” would melt together gold from many sources, and return the same quantities to the sources. You can certainly question the motivations of mixer-users, but even those acting in good faith probably have an idea that they might be acquiring tainted coins.

[[2](#2btcnemo)] “Market overt” generally grants the title to stolen goods to an innocent buyer. See, e.g., [Schwartz’s](http://digitalcommons.law.yale.edu/fss_papers/4166/) footnote 15 and Appendix for a brief overview of jurisdictions that follow “market overt.”

[[3](#3btcnemo)] Bitcoins are generally considered electronic and intangible, but some people [print](https://en.bitcoin.it/wiki/Ways_to_store_Bitcoins#On_a_paper_wallet_or_bank_card) them out on sheets of paper.

[[4](#4btcnemo)] In the US, if a merchant sells goods [entrusted](https://www.law.cornell.edu/ucc/2/2-403) to it in the “ordinary course of business” — whether authorized or [not](http://www.artnet.com/magazineus/news/spencer/spencers-art-law-journal12-30-10.asp) — the purchaser acquires the title. So perhaps if a Bitcoin exchange sold client coins to an innocent buyer on the exchange, without transferring the proceeds to the client, the buyer would acquire the title to the coins (in the US). But, if an exchange absconded with client coins and sold them later, outside the normal course of business, the victim would still own the title. Likewise for coins stolen from an exchange by a third party.

This treatment could have important consequences for the missing Mt. Gox coins, worth several billion USD at current prices. We still [don’t know](https://www.japantimes.co.jp/news/2017/08/05/national/media-national/bitcoin-exchange-operator-arrested-amid-new-questions-mt-gox-theft/) the full story behind those coins, but it seems likely that the victims own the title in the eyes of many jurisdictions.

[[5](#5btcnemo)] Similar arguments have allowed [lawsuits](https://www.lexology.com/library/detail.aspx?g=77fd26d2-6791-4bab-abd1-3c85bfd35eaf) concerning allegedly misappropriated art to proceed in NY.

[[6](#6btcnemo)] Bobby Cho of Cumberland, a DRW subsidiary and large OTC market maker, [says](https://marketvoice.fia.org/node/2843) that:

> On any given day, exchanges are reporting anywhere from $200 million to $250 million traded in a 24-hour period. OTC trading is not reported anywhere, but I’d imagine that the OTC market is larger than that number.

[[7](#7btcnemo)] JP Koning [discusses](http://jpkoning.blogspot.com/2016/01/what-makes-money-special-lawyers.html) the notion of fungibility as it relates to “nemo dat.” That is, if “nemo dat” applied to legal tender, identical units of currency would have different (and hard to ascertain) values depending on their history. If only one jurisdiction applies “nemo dat” to Bitcoin, then its value could become unstandardized everywhere.

[[8](#8btcnemo)] Especially high-risk coins might include the Silk Road coins auctioned by the US Marshals. The US Government [said](https://www.usmarshals.gov/assets/2015/dpr-february-auction/sale-order.pdf) that Ross Ulbricht “is the only person or entity reasonably believed to be a potential claimant to the Computer Hardware Bitcoins.” I don’t know how civil forfeiture works, so maybe this doesn’t matter at all, but isn’t there at least a chance some of those coins didn’t belong to him? Ulbricht was convicted of [charges](https://www.justice.gov/usao-sdny/pr/ross-ulbricht-aka-dread-pirate-roberts-sentenced-manhattan-federal-court-life-prison) related to drug-dealing, hacking, and money-laundering. I’m not sure it’d be a surprise if something in his possession had been stolen.

[GBTC](http://www.otcmarkets.com/stock/GBTC/profile), a Bitcoin-holding trust listed on OTC Markets, [bought](https://www.coindesk.com/bitcoin-investment-trust-wins-48000-btc-us-marshals-bitcoin-auction/) 48,000 BTC from this source. Cumberland reportedly [bought](https://www.coindesk.com/secretive-mining-firm-revealed-as-possible-us-marshals-auction-winner/) 27,000 BTC. Tim Draper [bought](http://www.reuters.com/article/us-usa-bitcoin/venture-capitalist-draper-wins-u-s-bitcoin-auction-idUSKBN0F719920140702) around 30,000 of “[these bitcoins with a tainted past](https://medium.com/@TimDraper/i-will-do-everything-in-my-power-to-drive-build-and-pursue-progress-and-change-73c6b0412114),” and deployed them at market maker and exchange [Mirror](https://www.coindesk.com/vaurum-rebrands-mirror/). Exchange itBit, which will form part of the [settlement price](http://www.cmegroup.com/trading/cf-bitcoin-reference-rate.html) for CME Bitcoin futures, [bought](https://www.coindesk.com/us-marshals-auction-winner-announcement-delay/) 13,000 BTC.

[[9](#9btcnemo)] I don’t know if OTC market makers keep large cash reserves, but perhaps some clients patronize them because they offer more reliable protections in case they accidentally sell illegitimate Bitcoins. I can imagine a situation where clients purchasing Bitcoin require market makers to post margin as an additional protection; and conversely market makers could require margin when buying coins from clients.