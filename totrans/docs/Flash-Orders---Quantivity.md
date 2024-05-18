<!--yml
category: 未分类
date: 2024-05-18 13:56:17
-->

# Flash Orders | Quantivity

> 来源：[https://quantivity.wordpress.com/2009/07/25/flash-orders/#0001-01-01](https://quantivity.wordpress.com/2009/07/25/flash-orders/#0001-01-01)

High-frequency trading (HFT) has been the subject of much hubbub across the blogosphere (and just recently [mainstream media](http://www.nytimes.com/2009/07/24/business/24trading.html?_r=1&scp=1&sq=high%20frequency&st=cse)) lately, stoked by the combo of Tyler Durden from [Zero Hedge](http://zerohedge.blogspot.com/) on the investigative side and Joseph Saluzzi from [Themis Trading](http://www.themistrading.com) on the institutional agency broker side. No doubt buy-side agency brokers and their their [NBBO](http://en.wikipedia.org/wiki/National_best_bid_and_offer)– and [VWAP](http://en.wikipedia.org/wiki/VWAP)-pegged execution algos are getting killed by the HFT guys.

A fascinating development along this thread are *flash orders*, originated by [Direct Edge](http://www.directedge.com)‘s ELP.

Traders Magazine ran a nice [intro article](http://www.tradersmagazine.com/issues/20_296/-103978-1.html?pg=1) this month. Much more interesting is reading actual [FIX](http://www.fixprotocol.org/) support for flash orders by the exchanges, as they become available. For example, [BATS](http://www.batstrading.com) [announced](http://www.batstrading.com/alerts/release_notes/) on May 26 support for BOLT orders (see the [BATS FIX spec](http://www.batstrading.com/resources/membership/BATS_FIX_Specification.pdf) for more details, such as Page 13 in bold). Relevant for this discussion is the following snippet from the BOLT announcement (other exchanges have equivalent):

> After removing the marketable liquidity on the BATS order book, BOLT Routing will first expose an order to BATS Members for up to 25 milliseconds before routing to away markets. BOLT Routing offers users the opportunity to fill during the exposure period and collect a $.0015 per share rebate on a routable order rather than pay the standard routing fee.

Two aspects of this are revolutionary, with the latter being the “reward” for accepting the former indirect “cost” (from the perspective of the order taker):

*   Advance knowledge:  members subscribing to the proprietary BATS order feed can observe BOLT orders 25 ms in advance of routing to an away market, which is otherwise invisible to everyone else (either until it is posted at the destination, or forever if the order is processed by the available book at the destination)
*   Rebate: marketable orders get a **rebate** (as opposed to a cost), if you agree to have your order flashed

Although not legally [front running](http://en.wikipedia.org/wiki/Front_running), due to the sub-500 ms exemption in the Reg NMS Quote and Limit Display Rules (Rules [602](http://content.lawyerlinks.com/library/sec/sec_rules/reg_nms/17cfr242_602.htm) / [604](http://content.lawyerlinks.com/library/sec/sec_rules/reg_nms/17cfr242_604.htm)), this does offer wonderful advance knowledge to BATS members.

Needless to say, devising an algo to exploit this type of pre-routing visibility is an interesting quantivity-style problem.