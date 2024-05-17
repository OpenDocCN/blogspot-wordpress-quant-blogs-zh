<!--yml
category: 未分类
date: 2024-05-13 00:03:57
-->

# hacking NASDAQ @ 500 FPS: Week Number 2

> 来源：[http://hackingnasdaq.blogspot.com/2012/03/week-number-2.html#0001-01-01](http://hackingnasdaq.blogspot.com/2012/03/week-number-2.html#0001-01-01)

Wow my 2nd week live has finished, pretty much just testing the break, accelerator, warming up the tiers, a few test laps, getting a feel for at what speed/rpm to shift gears. how it corners and most importantly how fast does it go and how fast can it stop.

so far no trip to the emergency room.... yet lol

This pretty much sums up the experience

... and yes getting wacked happens a bit, tho only down $20 so far. Whats weird is there`s this completely irrational fear, similar to the fear of talking to that girl... or hitting that asshole on the nose...  and now a new addition...  putting 100shrs at the BBO. Theres no logical explanation for it. Sure, she might ignore you, or you might get some nasty bruise or you might get executed with a 100shrs of an incredibly liquid stock, all 3 of which are of little consequence.

So just like the above examples, after you`ve done it a few times and realize its not so bad, the irrational fear dissipates and the analytical part of your brain takes over from more primal/emotional.

Basic breakdown has been

Week 1

- code order entry gateway

- code market data feed handler

- code risk managmenet

- cron jobs

- scripts of all sorts

- various system infra stuff.. pissed you cant monitor ECC failures

- various silly bug fixes

Week2

- recon/SOD/EOD automation

- performance/latency tests

- debugging latency problems with market data

- re-wrote feed handler (latency probs)

(most of the week spent on market data latency)

Whats gone wrong so far?

- incorrectly sent massive burst of cancels (5000+) ... opps

- VPN connection into colo dropped out while trading! holy fark!

- a few run-away terminal sessions, flood of printf`s makes ssh un-responsive

- desktop PC`s deciding to update and reboot by themself

- pretty much most of my worst fears have happened

Murphy I really do hate you.

Next up? bit more latency/performance tuning and now finally digging deeper into strategy development, and as they say.

Gentlemen, please start your engines!