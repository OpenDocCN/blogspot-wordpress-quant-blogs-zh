<!--yml
category: 未分类
date: 2024-05-18 06:01:21
-->

# Airplane Madness Coding – Financial Market Simulation | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2013/09/22/airplane-madness-coding-financial-market-simulation/#0001-01-01](https://mdavey.wordpress.com/2013/09/22/airplane-madness-coding-financial-market-simulation/#0001-01-01)

## Airplane Madness Coding – Financial Market Simulation

A few people may have realised that I’m flying more this year.  As anyone who flies a lot will know, there are only so many movies you can watch, and work document one can read/write/review.  At a certain point, I find the need to code 🙂  Recently (whatever timeframe that means 🙂 ) I’ve decide to attempt to merge all the mad spike/proof of concept idea’s I’ve had over the last n years into a financial market simulation.  Essentially, the concept is to take the various ideals I’ve kicked around in the many silo’s of finance, and weld them together to construct a simulation offering the normal high level actors such as banks, ECN’s, hedge funds etc.  Obviously, given the Rx revival on this blog, Rx is a key pattern in the construction of the simulation world.

Initially, I’ve decided to avoid any IPC, and simply constructed an in-memory message bus’s to connect the actors within a single process (and sub actors within an actor leveraging separate message bus’s), offering a faster speed of development in-flight 🙂  In the future, I expect this to change to allow the solution to scale.

Pricing and execution are supported (basic) within the simulator today, risk and hedge will follow soon.  Banks can be configured to run plain pricing engines with a model at one end of the bank spectrum, with the other offer algo type strategies to generate instrument pricing.

~ by mdavey on September 22, 2013.

Posted in [Java](https://mdavey.wordpress.com/category/languages/java/)