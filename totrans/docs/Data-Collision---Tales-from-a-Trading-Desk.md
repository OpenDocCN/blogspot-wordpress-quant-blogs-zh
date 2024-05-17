<!--yml
category: 未分类
date: 2024-05-18 05:46:24
-->

# Data Collision | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2014/09/17/data-collision/#0001-01-01](https://mdavey.wordpress.com/2014/09/17/data-collision/#0001-01-01)

## Data Collision

[Oracle](http://www.oracle.com/uk/products/middleware/cloud-app-foundation/coherence/overview/index.html) [GoldenGate](http://www.oracle.com/us/products/middleware/data-integration/goldengate/overview/index.html) and [HotCache](http://www.slideshare.net/OracleCoherence/coherence-goldengate-hotcache) offer an interesting (but expensive) solution to solving certain classes of problem.  Assuming an application stack that is Java, leveraging Oracle Coherence, backed by an Oracles database, where the application stack is installed in two locations, with the requirements for bi-directional replication of data, so each application sees the others data, and can perform actions on the data.  GoldenGate leveraging [HotCache](http://www.oracle.com/technetwork/middleware/coherence/learnmore/hotcache-tutorial-2193398.pdf) provides a mechanism to achieve replication, with the added benefit that not only does the data get replicated between databases ([GoldenGate](http://www.oracle.com/us/products/middleware/data-integration/oracle-goldengate-realtime-access-2031152.pdf)), but that [Coherence](http://coherence.oracle.com/download/attachments/16908294/Coherence+GoldenGate+Adapter.pdf) state is updated as well ([HotCache](http://www.slideshare.net/OracleMKTPR20/01-coherence-golden-gate-technical-overview)).

Data [collision](http://docs.oracle.com/goldengate/1212/gg-winux/GWUAD/conflict_resolution.htm) is however the key issues to resolve.  Oracle offers some best [practices](http://www.oracle.com/technetwork/middleware/gg-activeactive-11-2009-159996.pdf).  [Blogs](http://gavinsoorma.com/2013/04/goldengate-active-active-replication-with-conflict-detection-and-resolution-cdr-part-2/) offer some ideas as [well](http://www.dba-oracle.com/t_goldengate_built_in_conflict_detection.htm).

~ by mdavey on September 17, 2014.

Posted in [Data](https://mdavey.wordpress.com/category/data/)