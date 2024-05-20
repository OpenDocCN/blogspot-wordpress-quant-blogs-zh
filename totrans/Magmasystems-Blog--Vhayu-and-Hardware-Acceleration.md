<!--yml
category: 未分类
date: 2024-05-18 05:00:58
-->

# Magmasystems Blog: Vhayu and Hardware Acceleration

> 来源：[http://magmasystems.blogspot.com/2008/06/vhayu-and-hardware-acceleration.html#0001-01-01](http://magmasystems.blogspot.com/2008/06/vhayu-and-hardware-acceleration.html#0001-01-01)

Vhayu's

Velocity (too many Velocity's out there!) now has data compression performed by

FPGAs

. This looks like pretty impressive stuff, and sets the bar a bit higher for

KDB

.

With on-the-fly data compression, you can have more tick and trade data available for

backtesting

, and since the compression is done in hardware, this should reduce the latency compared with software-based on-the-fly compression.

Even though this is pretty good news, I wonder if Compliance Departments might have an issue with storing zipped data, as it is not readily available for inspection and analysis by non-

Vhayu

applications. But that is a trade-off that you will need to make. I am sure Ross

Dubin

can further enlighten us on this...

I would rename the product from Velocity to ZIP-ON-A-CHIP.

:-)

©2008 Marc Adler - All Rights Reserved.

All opinions here are personal, and have no relation to my employer.