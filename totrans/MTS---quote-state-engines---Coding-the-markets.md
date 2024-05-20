<!--yml
category: 未分类
date: 2024-05-12 19:52:09
-->

# MTS & quote state engines | Coding the markets

> 来源：[https://etrading.wordpress.com/2006/06/28/mts-quote-state-engines/#0001-01-01](https://etrading.wordpress.com/2006/06/28/mts-quote-state-engines/#0001-01-01)

## MTS & quote state engines

### June 28, 2006

[Finite state machines](http://en.wikipedia.org/wiki/Finite_state_machine) are a standard programming technique we use in our trading system for managing the state of quotes and RFQs. Let’s consider quote state management on MTS. MTS is particularly interesting since MTS treats market maker quotes as ‘proposals’, which are firm, tradeable quotes. This is quite different from purely quote driven markets like Bloomberg and TradeWeb, where the quotes we send are indicative, not tradeable. On those ECNs we only send a tradeable price to an individual client when they click on an indicative quote and initiate an RFQ.

Since for MTS, our quotes are firm, or tradeable, we developers must take great care over the quotes our system sends on the trader’s behalf. If we leave a stale quote out on the market, our traders will lose money. They get very unhappy when that happens. Exactly how and why quotes become stale would lead us into a discussion of the architecture and design of fixed income pricing engines, and the relationship between the prices of futures, benchmark bonds, bonds and swaps. We could also discuss MTS’s transactional quote model, and the associated queueing mechanisms. They’re both issues for another day, so let’s just take it as read that in a fast moving market, we have to recalc bond prices several times a second, and publish the resulting quotes to MTS.

Our system is an autoquoting system: it automates the quoting of bonds on a dozen ECNs. Naturally, our traders control our autoquoting system, just as a pilot controls an autopilot in an aircraft. The quote state engine ensures that the autoquoting system responds to trader operation of its controls in a safe and predictable manner. The controls at the trader’s disposal are the spread, the bid and offer sizes, and whether the quote should be on or off. Now let’s work though some example states and transitions for a quote for a bond…

*   States 
    *   Dead: we’re not quoting the bond
    *   PendingPrice: trader has switched the quote on, but we haven’t had a fresh tick from our pricing engine yet
    *   PendingMarketOn: the quote is on, we have a fresh mid price and have applied a spread and sent the resulting bid and offer prices and sizes to MTS, thereby opening a quote transaction, but MTS has yet to close the quote transation
    *   Live: MTS has closed the quote transaction, signalling to us that the proposal is live on the market, and therefore tradable
    *   PendingMarketOff: trader has switched the quote off, we’ve initiated the quote off transaction, but MTS has not yet confirmed the quote off transaction as closed
*   Transitions
    *   BankOn: we’re logged on to MTS
    *   TraderOn: quotes are grouped by trader. The trader for the group owning this quote is logged on
    *   Price: a fresh mid price for this quote has arrived from the pricing engine
    *   Trade: a market taker has hit our proposal. We may want to go quote off for a few seconds to let the trader think about the trade before going back on
    *   TraderOff: trader has turned off his quote group
    *   BankOff: we’ve logged off MTS

Getting the states and transitions right means we avoid trading at stale prices. For example…

*   Going quote on with a stale mid price, then subsequently trading at the wrong price
*   Trying to send a new quote before the transaction for the previous quote has closed. If the mid price for this quote ticks again, we’ll have a stale quote at the head of the outgoing queue, with a fresher quote behind it

Of course, all the above is an over simplification, and I’ve omitted all sorts of issues like MTS’s channel mechanism and the OpenServer, but you get the idea…