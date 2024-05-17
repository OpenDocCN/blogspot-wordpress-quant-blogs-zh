<!--yml
category: 未分类
date: 2024-05-18 06:43:10
-->

# Are Data Centers that Host Exchanges Utilities? | Mechanical Markets

> 来源：[https://mechanicalmarkets.wordpress.com/2015/05/28/are-data-centers-that-host-exchanges-utilities/#0001-01-01](https://mechanicalmarkets.wordpress.com/2015/05/28/are-data-centers-that-host-exchanges-utilities/#0001-01-01)

Swedish regulators are [seeking to fine](http://www.kkv.se/en/news/the-swedish-competition-authority-is-taking-legal-action-against-nasdaq-omx/) Nasdaq OMX for alleged anti-competitive practices in the Nordic colocation business. This case is fairly limited in scope, but it raises some more general questions about colocation.

HFTs, execution algorithms, and smart order routers rely on exchange colocation to provide cost-effective and fair access to market centers. Locking competitors out of an established data center could easily destroy their businesses. The Swedish Competition Authority [alleges](http://www.kkv.se/globalassets/english/news/15-0406_facts_nasdaq.pdf) that Nasdaq OMX did just that:

> In 2009, a Stockholm – based multilateral trading platform called Burgundy was launched. Burgundy was formed by a number of Nordic banks. The Burgundy ownership structure gave the platform a large potential client base, especially with respect to brokers. However, the owners had limited possibilities of moving trade from Nasdaq to Burgundy as long as the trade on Burgundy was not sufficiently liquid to guarantee satisfactory order execution. In order to increase the liquidity on Burgundy, it was vital for Burgundy to get more trading participants…
> 
> In order to come into close physical proximity with the customers’ trading equipment in Lunda, Burgundy decided to move its matching engine to the data centre in Lunda…
> 
> Burgundy had finalised negotiations with Verizon, via their technology supplier Cinnober, and the parties had agreed that space would be leased in Lunda for Burgundy’s matching engine. When Nasdaq heard of this agreement, they contacted Verizon demanding to be the sole marketplace offering trading services in Nordic equities in Lunda. Nasdaq told Verizon that if Verizon allocated space to the Burgundy matching engine at their data centre in Lunda, Nasdaq would remove their own primary matching engine and their co-location service from that centre. Such an agreement with Burgundy/Cinnober could also have an impact on Verizon’s global collaboration with Nasdaq. Verizon accepted Nasdaq’s demands, and terminated the deal with Burgundy/Cinnober.

# Latency Arbitrage And Traders’ Expenses

In the US, a lot of people are upset that equity exchanges are located all over New Jersey, instead of being in one building. Michael Lewis’s primary complaint about HFT is that it engages in “latency arbitrage” by sending orders between market centers ahead of anticipated institutional trades. I suspect that, in addition to those concerned about latency arbitrage, most HFTs would also be happy if important exchanges moved to one place. That would cut participants’ expenses significantly; there would be no need to host computers (and backups) at multiple locations and no need to procure expensive fiber and wireless links between locations. It would also allow HFTs to trade a given security on multiple exchanges from a single computer, dramatically simplifying risk checks and eliminating accidental self-trading.

If so many market participants want it, why hasn’t it happened? There could be several reasons:

1.  It’d be anti-competitive for exchanges to cooperate too much in bargaining with data center providers.
2.  Established exchanges want the best deal possible for their hosting, which means they need to consider bids from many competing providers.
3.  Under the Reg. NMS Order Protection Rule, there [could be some benefit](https://mechanicalmarkets.wordpress.com/2015/03/03/should-iex-become-a-full-exchange-incentives-for-exchanges-to-compete-by-increasing-delays/) to exchanges if they have a structural delay with their competitors.
4.  Some exchanges see hosting, connectivity, and related services as important sources of revenue and want customers to procure those services from them. This especially includes exchanges which require colocated customers to lease rackspace only from the exchanges themselves – and also exchanges that operate their own data centers.
5.  Exchanges don’t want competitors in the same data center as them, so they use their considerable leverage with providers to keep them out.

The allegations against Nasdaq OMX are about #5 and seem to be about just one case. But here’s a potentially concerning statement by [Andrew Ward in the FT](http://www.ft.com/intl/cms/s/0/fdef8d24-06f5-11e0-8c29-00144feabdc0.html) (2010):

> People familiar with Verizon said it would be unusual in the exchange industry for more than one operator to share the same data centre.

# A New Model for Colocation

Reg. NMS requires exchanges to communicate with each other, and would work better if delays in that communication were kept to a minimum. Would it be reasonable for updated regulation to require market centers to provide one another with a rapidly updated view of their order books? That would necessitate exchange matching engines being physically close to one another, ideally in the same building. Requiring this would end most types of “latency-arbitrage,” whether real or perceived.

One solution could be for FINRA to solicit bids from providers under the assumption of a long-term contract, with extra space available for new exchanges and traders – keeping costs down for everybody. This proposal is in tension with the concern in #1, but I wonder if, because we have a single national market system, it’s reasonable for that system to negotiate as a single entity, and for the other concerns to override #1\. Exchanges would no longer make much money from colocation services, but they could compensate for that by raising trading fees, which would arguably be healthier for markets anyway.

In my mind, what separates data centers from utilities is that, for most of their non-financial customers, there’s very little benefit to being in a certain building versus a nearby one. So long as nearby buildings have good connectivity to the local internet, customers have many options when procuring hosting services. Financial customers are much different. Once a major exchange is located in a certain building, traders, and sometimes competing exchanges, have no choice but to lease space there. That feels to me like a completely different dynamic, and possibly one that justifies data centers, in this specific industry, being classified as utilities.