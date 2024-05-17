<!--yml
category: 未分类
date: 2024-05-13 00:01:16
-->

# hacking NASDAQ @ 500 FPS: Tale of two sockets

> 来源：[http://hackingnasdaq.blogspot.com/2013/03/tale-of-two-sockets.html#0001-01-01](http://hackingnasdaq.blogspot.com/2013/03/tale-of-two-sockets.html#0001-01-01)

Once upon a time in a far away place there was a socket... 

The term socket has different interpretations, to those on the left in the network world it usually refers to a

[Berkely sockets](http://en.wikipedia.org/wiki/Berkely_sockets)

 aka socket(AF_INET, _ ... ) send/recv. 

To those on the right in

[LSI](http://en.wikipedia.org/wiki/Large_Scale_Integration#LSI)

 land it means a place where you plug in an

[ASIC](http://en.wikipedia.org/wiki/Application-specific_integrated_circuit)

. Today we`re talking about the latter, the space where you plug in (usually) a CPU.

Recently faced an unusual timing problem - a bit of code was taking negative 1 to 10 usecs. Under other circumstances would have been delighted the code was running so fast yet nature being the stubborn

[SOB](http://en.wikipedia.org/wiki/Son_of_a_bitch#Son_of_a_bitch)

 that it is, prohibits such things... atleast outside the Physics department.

It got me thinking, questioning every aspect of the code and hardware with one nagging question popping up.

### Is the cycle counter between two sockets synchronized?

[![](img/3d18bcd70389ac74998326da4f45344c.png)](http://www.pcper.com/files/imagecache/article_max_width/review/2011-12-14/die.jpg)

Its well known and documented that in a post Nehalam age the intel cycle counter is rock solid, invariant to power states, between cores and also immune to turbo boost, the latter being a pain the ass if you really want to count cycles. Why does it always tick over at the frequency rate listed on the box ? seems the Nehalam intel designers decided rdtsc & friends should be based on a clock in the creatively named "UnCore" which sits way out near the IO logic, thus centralized and the same for all cores.

rdtsc on a single cpu socket machine has been a trusted friend since the good ol Pentium 90 days but never tested its behaviour between cpu sockets. Yet is it syncrhonized between two cpu sockets? the short answer is, yes it is very well synchronized between cpu sockets as mentioned in various placed. However ... being the skeptical person I am - don`t believe writings on teh itnerwebz (such as this blog!) and so.....  a test.

The test is simple, run 2 hardware threads(HWT) on 2 different sockets. Each HWT will update a shared cycle counter in memory. The expected result is, the local HWT cycle counter should *always* be greater than the memory value.

Why ? example case 1

Cycle |         HWT 0     |  HWT 1

   0  |  sample           |

   1  |  write to memory  |

   2  |                   |    sample

   3  |                   | write to memory

Or the perverse edge case

Cycle |         HWT 0     |  HWT 1

   0  |  sample           |      sample

   1  |  write to memory  |   write to memory

2  | |

**1 - in the smallest font possible hoping no one will read this... the test fails when the 64b cycle counter overflows

**2 - yes im completely delusion to think the above is anything close to the voodoo magic that goes on inside a real intel cpu

Presuming the cycle counter is synchronized  then every time we sample the cycle counter, the counter will be higher than whats written in memory - because whats in memory is a past cycle count, which by definition is less than the current count.

in code  (g_tsc is the shared memory value)

        u64 memory_tsc = g_tsc;

        u64 tsc = rdtsc();

        s64 dtsc = tsc -  memory_tsc;

        assert(dtsc >= 0);

This works if the two cycle counters (one for HWT 0, one for HWT 1) are synchronized and fails otherwise. There is a problem tho... if we run this as is, it fails.

Theres 3 (possibly more?) reasons why

1) cycle counters are not perfectly synchronized

2) x86 micro architecture is re-ordering the memory operations

3) compiler re-ordered the load.

Checked the asm and 3) is not true thus suspect 2) as x86 is notorious for its (very) relaxed memory ordering so we modify the above slightly by adding an lfence instruction. What this does is serializes all memory loads (but not stores) with respect to the current instruction fetch stream - creating a barrier of some sort.

After this is added the program runs perfectly, thus conclude the cycle counter between sockets is perfectly synchronized, or closely synchronized.

[![](img/4e0854b71ffa19b18771113543e157ed.png)](http://msptelemarketing.com/wp-content/uploads/2011/05/istock_000010672195xsmall-300x199.jpg)

Now we know their closely synchronized, the question is how close and does it explain my negative 10usec. To do this we run a histogram on what that delta between the cycle counter and the memory value which shows a range of 100-200 cycles, which at 3ghz is at most 66.66nses, likely the QPI cost between sockets. All in all thats pretty tight.

The down side, this was classic tunnel vision and not the cause of my negative latency number. The real cause was something way up the stack and far to embarrassing to write about here.!