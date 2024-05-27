<!--yml

category: 未分类

date: 2024-05-12 19:36:24

-->

# LMAX Disrupter | Coding the markets

> 来源：[`etrading.wordpress.com/2011/01/21/lmax-disrupter/#0001-01-01`](https://etrading.wordpress.com/2011/01/21/lmax-disrupter/#0001-01-01)

## LMAX Disrupter

### January 21, 2011

两位 LMAX 人的这个[演讲](http://www.infoq.com/presentations/LMAX)是我一些朋友向我推荐的。我昨晚看了，印象深刻。主题是高吞吐量，低延迟的服务器工程。有很多关于如何让 Java 变得非常快的内容，以及如何以一种同情硬件的方式与硬件工作。他们推荐为一个业务逻辑使用一个线程，为消息传递和持久化使用专用线程。这与传统的 Java 智慧相悖，传统 Java 智慧通常涉及执行相同逻辑的工作线程池和锁。这是一种我在混合 C++ Python 服务器进程中所取得成功的做法：将所有的业务逻辑放在一个 Python 线程上，然后在 C++线程上处理发布/订阅消息和持久化。

他们所倡导的 LMAX Disrupter 模式，真正让我感到新颖和激动人心的是，它使用了环形缓冲区来实现线程间的无锁通信。我在我的 C++和 Python 进程之间使用队列来进行线程间的通信。正如 LMAX 的人所指出的，这些队列使用了锁。LMAX Disrupter 使用原子 CAS 指令来实现线程间的通信，因此使用环形缓冲区的通信是锁免费的。

总的来说，这是一个精彩而富有洞察力的演讲……
