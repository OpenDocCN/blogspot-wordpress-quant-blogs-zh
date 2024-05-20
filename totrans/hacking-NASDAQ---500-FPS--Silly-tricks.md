<!--yml
category: 未分类
date: 2024-05-13 00:04:17
-->

# hacking NASDAQ @ 500 FPS: Silly tricks

> 来源：[http://hackingnasdaq.blogspot.com/2011/10/silly-tricks.html#0001-01-01](http://hackingnasdaq.blogspot.com/2011/10/silly-tricks.html#0001-01-01)

... and the long grind forward continues abeit slowly. This week found some weirdness with the exchange and problems with my strategies using end of day tick data aka non realtime paper trading. Was using slightly stale 3-4Month old data and figured it should be close enough but dam.... how much things have changed in a few months. Will post about this when ive got some spare cycles.

Im a huge fan of autonomic computing, which means hardware&software systems that do integrity checking and automatic recovery, with the obvious examples being RAID for disk and ECC for ram. Once upon a time I worked for and with (insert huge megacorps you all know) <insert all="" know="" megacorp="" you="">and had a fascinating discussion with one of their hardware engineers.</insert>

HW Dude: hmm thats a weird problem, whats the value of register at offset 0xbeefbabe?

Hacking Nasdaq: register 0xbeefbabe reads out to be ... 0x01234567.

(silence)

HW Dude: are you sure thats correct?

Hacking Nasdaq: ... yes

HW Dude: thats impossible, are you on crack?

.

.

.

What he was referring to is the MSB of that register was the logical OR of the other 30bits. Making a value of 0x01234567 impossible with the only correct value being  0x**8**1234567\. Moral of the story is encoding self integrity checks into everything makes it easy to catch and not waste time on dumb ass errors - the "oh woops the cable isnt plugged in, sorry" kind

... which leads us to OUCH and the 14byte identifier token. What Ive done is reserve the last byte as an integrity check such that the 32bit sum of the previous 13bytes modulo 26 is its value.

e.g.

u32 Sum = 0;

for (int i=0; i < 13; i++) Sum += P->Msg.OrderAdd.Token[i]

P->Msg.OrderAdd.Token[13] = 'A' + Sum % 26;

This way its trivial to check if the OrderToken you looking at is actually real or corrupt without any effort. So far ive caught this a few times, usually when some bit of code has gone rouge and pissing all over memory.

...and yes thats only in development, no errors in prod... yet :)