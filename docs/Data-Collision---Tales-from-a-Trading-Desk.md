<!--yml

category: 未分类

date: 2024-05-18 05:46:24

-->

# Data Collision | Tales from a Trading Desk

> 来源：[`mdavey.wordpress.com/2014/09/17/data-collision/#0001-01-01`](https://mdavey.wordpress.com/2014/09/17/data-collision/#0001-01-01)

## Data Collision

[Oracle](http://www.oracle.com/uk/products/middleware/cloud-app-foundation/coherence/overview/index.html) [GoldenGate](http://www.oracle.com/us/products/middleware/data-integration/goldengate/overview/index.html) 和 [HotCache](http://www.slideshare.net/OracleCoherence/coherence-goldengate-hotcache) 提供了一个有趣（但昂贵）的解决特定类别问题的方案。假设一个使用 Java 的应用程序堆栈，利用了 Oracle Coherence，在 Oracles 数据库支持下，应用程序堆栈安装在两个地点，需要数据双向复制，因此每个应用程序都能看到另一个的数据，并可对数据执行操作。GoldenGate 利用 [HotCache](http://www.oracle.com/technetwork/middleware/coherence/learnmore/hotcache-tutorial-2193398.pdf) 提供了一种实现复制的机制，除了数据在数据库之间被复制外 ([GoldenGate](http://www.oracle.com/us/products/middleware/data-integration/oracle-goldengate-realtime-access-2031152.pdf))，还更新了 [Coherence](http://coherence.oracle.com/download/attachments/16908294/Coherence+GoldenGate+Adapter.pdf) 的状态 ([HotCache](http://www.slideshare.net/OracleMKTPR20/01-coherence-golden-gate-technical-overview))。

Data [collision](http://docs.oracle.com/goldengate/1212/gg-winux/GWUAD/conflict_resolution.htm) 然而是需要解决的关键问题。Oracle 提供了一些最佳 [practices](http://www.oracle.com/technetwork/middleware/gg-activeactive-11-2009-159996.pdf)。 [Blogs](http://gavinsoorma.com/2013/04/goldengate-active-active-replication-with-conflict-detection-and-resolution-cdr-part-2/) 提供了一些想法，还有一些 [well](http://www.dba-oracle.com/t_goldengate_built_in_conflict_detection.htm) 的想法。

~ by mdavey on September 17, 2014.

Posted in [Data](https://mdavey.wordpress.com/category/data/)
