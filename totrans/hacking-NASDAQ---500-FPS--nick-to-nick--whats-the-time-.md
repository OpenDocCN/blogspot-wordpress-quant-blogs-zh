<!--yml
category: 未分类
date: 2024-05-13 00:07:34
-->

# hacking NASDAQ @ 500 FPS: nick to nick, whats the time?

> 来源：[http://hackingnasdaq.blogspot.com/2010/01/nick-to-nick-nicknacks.html#0001-01-01](http://hackingnasdaq.blogspot.com/2010/01/nick-to-nick-nicknacks.html#0001-01-01)

The topology of the previous test was NIC -> switch -> NIC and we assumed the switch was causing un-due latency. Turns out this is true, but not to the extent anicipated.

NIC <-> switch <-> NIC fabric time

NIC <-> NIC fabric time

As you can see, ditching the switch gained about 7,000ns, not bad but there`s still 23,000ns going somewhere. First thing to always do is back-of-the-envelope calculation and multiply by two.

GigE throughput is 1e9 bits / second, so on average the frame is say 160B (minus PHY framing) so that's 160 * 8 / 1e9  - roughly 1,280ns to encode one way. We`re doing this x4 (encode->decode->encode->decode) so we`re up to 5,120ns or so to encode the thing, and lets be generous and double it, resulting in around 10,000ns to account for GigE PHY framing. and  other junk, but we`re still missing 13,000ns!

Taking a detour, the 82573L NIC we`ve used so far is... slightly incorrect. Seems I assumed NICx2 on a blade would use the same controller, however this is incorrect. The 82573L NIC we`ve been assuming, is in fact a Intel 82566DC-2 NIC. If we change it to *really* use the 82573L the picture ain`t pretty.

NIC <-> NIC real intel 82573

And when its compared with using the Intel 82566DC its quite interesting.

NIC <-> NIC Intel 82566DC

Its true the 82573L is about a year older than the 82566DC, 2005 vs 2006 but that alone cant explain the huge 15,000ns or so difference. Digging a bit deeper, there`s significant difference in host interface between the two cards, the 82573L uses PCIe while the 82566DC use`s intels proprietary LCI*/*GLC bus - its wired directly to the southbridge. Lets use some creative licensing, and assume say 5,000ns is improved hardware design, leaving around 5,000ns each way, spent in the PCIe encode/decode/hub/and largish staging buffers, which conveniently is near our missing 13,000ns number (remember only 1 NIC is on PCIe).

And we have some ideas on where the time has gone:

- 10,000ns for GbE encode/decode/transport

- 10,000ns for PCIe encode/decode/forward/transport.

- 3,000ns

LCI/GLC encode/decode/transport (whats left)

How realistic these guesstimates are I`ve no idea and further digging requires hardware tools which are expensive, thus aren`t available. So we`ll leave it at 23,000ns in the interconnect fabric, and average HW time as 23,000ns / 4 = 5,740ns or so in one direction.