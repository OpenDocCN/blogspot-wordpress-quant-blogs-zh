<!--yml
category: 未分类
date: 2024-05-18 06:37:44
-->

# Balloons, Retail Order Auctions, Citadel and Antitrust, IEX and FTX | Mechanical Markets

> 来源：[https://mechanicalmarkets.wordpress.com/2023/06/07/balloons-retail-order-auctions-citadel-and-antitrust-iex-and-ftx/#0001-01-01](https://mechanicalmarkets.wordpress.com/2023/06/07/balloons-retail-order-auctions-citadel-and-antitrust-iex-and-ftx/#0001-01-01)

I am going to try to write a bit more casually here, seeing as this is a blog. Please feel free to discuss anything that looks wrong in the comments section or over email with me.

## **Balloon Shootdowns**

It seems unlikely that an HFT would use an unmaneuverable balloon. They’d get blown off their useful path pretty quickly, and even if it were economically viable on some routes to float expendable communications relays into the air every hour or so, it’d create an irresponsible amount of litter. Nevertheless, how long until an F-22 shoots down a high-frequency trader? I wouldn’t be surprised if HFTs were operating maneuverable balloons, balloons tethered to buoys, or drones that might be near some of the reported balloon incidents.

## **Retail Order Auctions**

There’s quite a hubbub over the SEC’s [proposal](https://www.sec.gov/news/press-release/2022-225) for retail orders to be sent to auctions at market centers, where some order information would be shown to the public via auction messages, allowing low and mid-latency traders to compete over their execution price. I will admit that running auctions so often makes me nervous — they generally have an elevated potential for mishaps compared to order books. So some of the criticism is justified. But the near-unanimity about the proposal seems like too much. If this proposal isn’t workable, then retail flow should probably be restructured another way. The industry catchphrase that “retail has never had it better” is true, but that doesn’t mean that it can’t get better still.

Additionally I think the current system is unsustainable, and may eventually result in degraded execution quality for retail traders. Citadel is in danger of gaining a monopoly on retail order flow. Virtu (which, in keeping with a certain tradition, [questions](https://www.marketwatch.com/story/virtu-ceo-slams-gensler-reforms-as-democratic-plan-to-curb-retail-trading-2ea1daf0) the SEC’s good faith) appears to be losing the ability to compete at the top level. Some new entrants could potentially give Citadel more competition, like [Jane Street](https://content.schwab.com/drupal_dependencies/psr/606/2023-Q1-Schwab-Quarterly-Report.pdf). But I have my doubts that new entrants can survive unless they’re willing to lose a lot of money for multiple quarters as they accumulate volume, not only because of the regulatory and legal overhead, but also because Citadel has enormous market color on retail orders and the market overall. Which brings me to the next topic.

## **When Does a Market Participant’s Dominance Become Anticompetetive?**

This question is a thorny one. Even in a completely open market, a participant with high market share could have enough additional color from its own trading activity that it’s very hard for newcomers to compete. A new entrant might have access to all public data, but they cannot match what the dominant trader sees, which learns a lot about market conditions from its own fill information. Now, there’s nothing wrong with traders compliantly using information from their own orders — every trader’s order flow is path-dependent — but I think everyone would agree that it’d be a problem for one entity to have 99% market share (double-counted). In such a case, the entity would not only get color from their filled and unfilled orders’ particular details, but would know the direction of order flow of the overall market. There’d also be serious financial stability problems resulting from such high concentration.

In any case, US equities and other electronic markets are not completely open and transparent, although they’re far more than they used to be. One of the biggest examples of that is access to retail flow. When a market has sufficient barriers to entry, the dominant participant can offer an inferior product and still maintain its position. I’m not saying Citadel is doing so right now, but the danger is clearly there.

## **Flash Boys, 9 Years Later**

Hard to believe it’s been nearly a decade. The eponymous “boys” of IEX preached several tenets of exchange design. How would the characters in the book judge today’s IEX?

**Tenet 1:** “Fading liquidity” is a huge problem created by electronic trading, creates a “rigged” market, and an exchange should do as much as possible to prevent it.
**IEX today:** Has special order types that use advance information — skipping the speedbump — so resting orders can fade when incoming, contra-side order flow is judged to be unprofitable. IEX offers this functionality on displayed orders too, which the CEO committed not to do in 2016 because “that’s what started this whole journey for us” ([footnote 10](https://www.bloomberg.com/news/articles/2016-10-12/beyond-flash-boys-matt-levine-interviews-iex-s-brad-katsuyama)).

**Tenet 2:** “Fading liquidity” is in large part caused by high-frequency traders sniffing out large, routable orders before they can reach their destination markets. An outbound speedbump is necessary for an exchange to prevent this form of fading.
**IEX today:** Has eliminated its outbound speedbump.

**Tenet 3:** Exchanges should have simple, easily understood order types and mechanics.
**IEX today:** An [alphabet soup](https://www.iexexchange.io/products/order-types) of complex order types.

**Tenet 4:** Market data fees contribute to a “rigged” market.
**IEX today:** [Charges](https://www.iexexchange.io/resources/trading/fee-schedule) for market data.

A pretty lackluster performance. So it’s no surprise that people paranoid about markets aren’t interested in “Flash Boys” anymore, preferring darker conspiracy theories. But somehow, IEX seems be involved there too! IEX appears to have cross-invested with FTX, planning some kind of joint venture to help unrig the financial system. [[1](#Jup1)] The details are murky (naturally, IEX used to preach increased disclosure), but it seems like IEX may have engaged in some kind of [share swap](https://www.axios.com/pro/fintech-deals/2022/11/14/ftx-f-bankruptcy-fallout-iex) with FTX. [[2](#Jup2)] In any case, while this venture says a lot about IEX’s judgment and governance, it doesn’t *necessarily* say much about the executives’ honesty. People who assume fraud is behind every regretted transaction can make easy targets for actual fraudsters.

And who better to call when trying to differentiate a seller of genuine snake-oil from an outright swindler? Evidently, Michael Lewis. [Appearing](https://www.youtube.com/watch?v=7KWuS_wOUnY) with [Arthur Hayes](https://www.justice.gov/usao-sdny/pr/founders-cryptocurrency-exchange-plead-guilty-bank-secrecy-act-violations) at a crypto conference, Michael Lewis said Brad Katsuyama introduced him to Sam Bankman-Fried and asked for Lewis’s opinion on whether IEX should proceed with its FTX deal. Lewis jokingly recalls how he told Katsuyama yes, then got interested in profiling SBF. Now, maybe this story isn’t told completely accurately, for instance it could be that Katsuyama had already decided to do the deal and was hoping to get Lewis interested in promoting FTX. That theory is compatible with a [report](https://www.foxbusiness.com/markets/iex-taps-potential-partner-regulated-crypto-exchange) that IEX had such a good time with FTX that it wants to try collaborating with another crypto exchange.

But what a twist! After the smoke has cleared from “Flash Boys,” its legacy is finally emerging: a sequel and an influential Apple TV show about the largest financial fraud since Madoff. And Michael Lewis not only had a “[front row seat](https://www.nytimes.com/2023/05/16/books/michael-lewis-ftx-bankman-fried-going-infinite.html)” to the scam, he was a tool in SBF’s [reputation-laundering campaign](https://www.reuters.com/technology/exclusive-how-ftx-bought-its-way-become-most-regulated-crypto-exchange-2022-11-18/) that intended to [restructure](https://www.ft.com/content/dd4db197-cb9b-4f29-b923-9bd94e1e3aed) our financial system. Anyway, maybe Lewis will appreciate the delicateness of how he tells a story about a con-man who used stolen money to [nearly buy off](https://www.axios.com/2022/12/14/sbf-campaign-finance-political-donations-charges) the world’s power centers. Or maybe he’ll broadcast unfounded conspiracy theories to a hundred million people. Given his record, I won’t deny feeling nervous.

[[1](#Jdown1)] I’m obviously being slightly tongue-in-cheek — but only slightly. A big argument of “Flash Boys” is that regulators help rig markets, sometimes unwittingly. IEX’s CEO [said](https://www.youtube.com/watch?v=-RWWTFDuwv0&t=285s) that their joint venture with FTX was focused on helping “shape” regulation, drawing from their experience doing so with equity markets. It’s not a big stretch to think this “shaping” aimed to help FTX with its desire to replace the whole financial system with something they could claim is “unrigged.”

[[2](#Jdown1)] My (admittedly crude) understanding is that exchanges are required to disclose all 5%+ owners on their Form 1 Exhibit K ([p7](https://www.sec.gov/files/form1.pdf)). It appears that IEX has [not done so](https://www.sec.gov/cgi-bin/browse-edgar?action=getcompany&CIK=0001653090&type=&dateb=&owner=include&count=40&search_text=) yet. I don’t know why.