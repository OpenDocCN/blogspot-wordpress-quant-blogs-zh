<!--yml
category: 未分类
date: 2024-05-13 00:08:22
-->

# hacking NASDAQ @ 500 FPS: trivial reject

> 来源：[http://hackingnasdaq.blogspot.com/2009/12/trivial-reject.html#0001-01-01](http://hackingnasdaq.blogspot.com/2009/12/trivial-reject.html#0001-01-01)

Ok down to business, problem is there's a 64b unique index(OrderID) we need test against so a straight up array aint going to cut it. Next choice is std::map<> with a key of orderID storing a pointer to the order structure. Please note we are testing against 700M / messages on the MSFT symbol, so reject rate is 99.7% of all messages. Also note this is ITCH3.1 so we need to do ascii->u64 converion on the orderid which is reflected in the perf numbers.

First up std::map<> which ... fails to run. Allocats a metric ton of memory and barely gets beyond an hour or two of trading. assuming theres enough memory.. clocks in at 553cycles / message or 135ns@4.1ghz.

Next up is an unordered map, as we dont need it sorted and.. same thing. metric ton of memory and fails to complete. assuming you have the memory, it clocks in at  285cycles/message or 69ns@4.1ghz.

Which is hmm not bad if you have 64GB of RAM and your run of the mill programmer, but we can do better. The trick is we have information that can`t be expressed to STL, and that`s that orderID only uses 34bits of data, and the working set is roughly 18k orders so lets exploit it using a bitmap array + 16 way set, similar to a hardware set associtave cache.

How it works is use the 20 LSB as an index into a 1bit array, resulting in a 128KB array (2^20 / 8 /1024). If the bit is set, then theres valid entries in the set, otherwise theres nothing there - trivial reject. If there is entries then its a simple 16 entry search space which is easily parallelizable.

Thus going from OrderID -> Order_t* is nice fast O(1) or O(16) depending on how you look at it with a nice fixed memory footprint. Problems arise if the set overflows and theres data loss, but the highest occupancy is a wopping 3 entries for MSFT so in practice we drop down to 8 entries in the set.

Total footprint = (2^20 / 8) + (2^20 * 16 * 8)  ~= 128MB. However as stated in optimization 101, keeping the footprint down is critical and we can reduce this further. Given each set entry, we know its lower 20bits are unique, and the same for all set entries. OrderID has 34 significant bits, so that drops down to significant 14bits thus we can use a 16bit value in the set search space instead of the full 64bit, woot.

Footprint = (2^20 / 8) + (2^20 * 16 * 2) ~= 32MB

As the data indicates a max 3 entry occupancy, its safe to reduce to 8 entries per set leaving

Footprint = (2^20 / 8) + (2^20 * 8 * 2) ~= 16.125MB

Which gets close to fitting entirely in the L3 cacahe! The numbers clock in , averaging 108 cycles / message, meaning 26ns / msg @ 4.1GHz for a full book update on a single symbol. Keep in mind this is  mostly just the reject code at play, its straight C(no assembler/intrinsics), were dealing with ITCH3.1 and the book update code is pretty shitty and eats into the average. So .... theres still plenty of milage to get that number down!