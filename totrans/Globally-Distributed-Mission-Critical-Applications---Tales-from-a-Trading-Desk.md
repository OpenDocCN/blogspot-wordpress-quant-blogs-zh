<!--yml
category: 未分类
date: 2024-05-18 05:39:46
-->

# Globally Distributed Mission Critical Applications | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2015/09/23/globally-distributed-mission-critical-applications/#0001-01-01](https://mdavey.wordpress.com/2015/09/23/globally-distributed-mission-critical-applications/#0001-01-01)

## Globally Distributed Mission Critical Applications

Kris Beevers offers some great [insight](http://highscalability.com/blog/2015/9/2/building-globally-distributed-mission-critical-applications.html) through a two part series on  [NSONE](https://nsone.net/).  A few noteworthy callouts:

*   “Unit testing is not enough.   Test the interactions between your subsystems.”  Could not agree with this more.  Numerous projects obsess with unit test coverage, and forget boundary testing between subsystems.  Likewise, how many systems fail to test the expected number of payloads sent over the wire?
*   “Automate Deployments And Config Management – With Extreme Care” There is no free lunch!
*   “We roll out deployments facility by facility, from lowest traffic to highest. Within a facility, we roll out server by server, and even core by core, running a comprehensive functional testing suite at every step of the way. ”  Big bang deployments have implications.  NSONE deployment sounds very similar to the
*   “Simulate the bad things before they happen. Netflix’s Chaos Monkey is one well-known example” – how many times have you heard IT propose no concept of failover/DR because they believe their isn’t budget, only to be burnt a time period later?
*   “Lock your systems down and minimize the attack surface exposed to the internet.” – security 101 in my view.  Likewise, “Each role in your architecture should expose the services it provides only to the set of systems that need to access those services”

~ by mdavey on September 23, 2015.

Posted in [Agile](https://mdavey.wordpress.com/category/agile/)