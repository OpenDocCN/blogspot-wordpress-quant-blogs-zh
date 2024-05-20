<!--yml
category: 未分类
date: 2024-05-13 00:04:02
-->

# hacking NASDAQ @ 500 FPS: h4cking HASDAQ 1U High Performance Server Model 1337

> 来源：[http://hackingnasdaq.blogspot.com/2012/02/h4cking-hasdaq-1u-high-performance.html#0001-01-01](http://hackingnasdaq.blogspot.com/2012/02/h4cking-hasdaq-1u-high-performance.html#0001-01-01)

Busy as hell.. seems to be a the never ending story. Original plan for colo was teaming up with a small HFT group that would have been really cool but.. alas fell thru at the last minute, thus had to re-group both infra and strategies. So as of now im finally plugged in hooked up and almost ready to let that first strategy run loose to generate those millions of dollars ... ho ho ho ha :P

When you get ready to put servers into colo theres a sudden realization of how expensive enterprise grade name brand servers are. Typically HP G6 or G7, various flavors of IBM and occasionally a DELL shows up. Unfortunately these kinds of machines are out of my budget or more precisely I`d rather spend the money elsewhere so.... lets build are own 1U server on the cheap.

Reference point is

HP ProLiant DL370 G7 High Performance 2U Server

x2 6 core 3.4Ghz X5690

16GB ECC memory

5TB of disk space

Dual 10Gb Port NIC

[http://h71016.www7.hp.com/dstore/MiddleFrame.asp?view=all&oi=E9CED&BEID=19701&SBLID=&AirTime=False&BaseId=35620&FamilyID=3180&ProductLineID=431](http://h71016.www7.hp.com/dstore/MiddleFrame.asp?view=all&oi=E9CED&BEID=19701&SBLID=&AirTime=False&BaseId=35620&FamilyID=3180&ProductLineID=431)

For a total of $14,421.00 ..... OUCH!

Brand new h4cking NASDAQ 1U High Performance Server Model Number 1337

... lol

So whats in the box?

x1 4 Core 8 thread 3.4Ghz E3-1270 (Sandy Bridge)

16GB ECC memory

4.5TB HDD space

120GB Intel SSD

x1 SolarFlare Dual 10Gb NIC

... and yes its a tiny 1U as you can see from the $20 bill. Typically this kind of chassis is used for low end systems as the aiflow is pretty messed up ... but it fits my style, lean, mean and a hell of alot cheaper! Only major concern is airfow as cold air intake from the side and the blower pushing the air  out the back (pic is a little old) yet so far no problems.

To break the costs

Motherboard is SuperMicro X9SCM-F (IPMI very important) - $200

Processor E3-1270 - $340

16 GB ECC Memory - $200

WD Green 2TB - $120

WD Green 2.5TB $120 (disk in the picture is a 1TB that was replaced)

120GB Intel SSD (thing between PSW & HDD) - $200

Chassis, imported directly from Taiwan - $100 (including shipping + PSW + Blower + Riser)

SolarFlare Dual Port 10Gb NIC - $1000

Total all up $2,280

That`s a saving of $12,000 not bad. Of course the reliability of the server, comparability, SLA is non existent, HDD are slow.. uses some "Desktop Grade" parts as well as a power supply of unknown origin. Not exactly the fairest of fair compairson to your decked out HP G7 box but spending money where it counts, CPU frez, Memory, and NIC. To sum it up nicely would be to say, if it fuck ups its your own fault and theres no support line to call/sob/pass the buck to. 

All up haven`t had any problems and more than happy with the performance and yes DO NOT mess with the punk ass pink bunny!