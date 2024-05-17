<!--yml
category: 未分类
date: 2024-05-17 23:41:16
-->

# Running QuantLib on a Raspberry Pi – HPC-QuantLib

> 来源：[https://hpcquantlib.wordpress.com/2012/08/11/running-quantlib-on-a-raspberry-pi/#0001-01-01](https://hpcquantlib.wordpress.com/2012/08/11/running-quantlib-on-a-raspberry-pi/#0001-01-01)

QuantLib 1.2 runs on a [Raspberry Pi](http://www.raspberrypi.org/), a credit card computer build around an 700MHz ARM processor and priced at US$ 35\. Compiling QL on the Pi is straight forward:

1.  install boost unit tests: sudo apt-get install libboost-test-dev
2.  ./configure –disable-static
3.  make

If your distribution is based on boost 1.49 then you will get many warnings like “Warning: *swp*{b} use is *deprecated* for this architecture”. These warnings can be ignored or follow the short note [here](https://svn.boost.org/trac/boost/ticket/7141) to get rid of them. The QuantLib benchmark runs at 28.3MFlops, which is comparable to the performance of an Pentium II@300MHz.