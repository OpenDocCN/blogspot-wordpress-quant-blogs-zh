<!--yml
category: 未分类
date: 2024-05-12 19:52:32
-->

# The write stuff | Coding the markets

> 来源：[https://etrading.wordpress.com/2006/06/22/the-write-stuff/#0001-01-01](https://etrading.wordpress.com/2006/06/22/the-write-stuff/#0001-01-01)

## The write stuff

### June 22, 2006

Our electronic trading system consists of more than 500K lines of C++. There's some Java and C# in there too. We have 50 traders using that system to autoquote, place and pull orders, autonegotiate RFQs and STP their trades for a dozen ECNs. Last year we did 23 releases to the trading floor.

Developers who come from an ISV or shrink wrap background are often completely confounded by the way development and deployment works in wholesale banking. They're used to long development and release cycles, measured in months and years. They think that since our systems are used to trade billions of Euros of bonds, swaps, futures and options every day, they must have massively heavyweight QA processes, like the [shuttle software](http://www.fastcompany.com/online/06/writestuff.html).

What those ISV developers don't realise are the factors that make trading software different from vendorware…

*   Time to market is critical. When a trader wants to quote new instruments, they'll often tolerate flakiness to get to the business opportunity quicker.
*   We only deploy to one site, our trading floor. We don't have to worry about being cross platform, or which service pack the users are running. We have a single, well managed, target infrastructure.
*   We have the luxury of a dedicated test and release team. There's no way our users will test software, they're too busy trading !  Our testers often save us developers from getting the hairdryer treatment from a trader by picking up bugs before deployment. God bless 'em.

So in many ways developing trading systems is like the new world of web application deployment. Paul Graham was [ahead of the game as usual](http://www.paulgraham.com/road.html) on this. And like Paul Graham says, we're in very close touch with our users on the trading floor. They're quick to let us know when we get it wrong!