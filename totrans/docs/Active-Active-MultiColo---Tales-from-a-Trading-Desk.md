<!--yml
category: 未分类
date: 2024-05-18 05:37:02
-->

# Active/Active MultiColo | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2015/12/15/activeactive-multicolo/#0001-01-01](https://mdavey.wordpress.com/2015/12/15/activeactive-multicolo/#0001-01-01)

## Active/Active MultiColo

Great [presentation](http://www.infoq.com/presentations/linkedin-scalability-arch) from Erran Berger, Head of Content Engineering at LinkedIn.  Discussion centres around stream processing, personal data and cache invalidation & replication conflicts.  Take aways:

*   Kafka – data is replicated (best and worst feature because it causes re-processing of messages)
    *   Kafka and DB replication turned out not to be the LinkedIn solution – due to duplication.
    *   The solution was to process user notifications in the data centre in which the user is attached too via a sticky routing service.  Each data centre has a queue to route messages to other data centres.
    *   Process Kafka messages only once, else you’ll go down a painful road 🙂
*   Data
    *   Replicate data only as required.  Personal data doesn’t need to live everywhere in LinkedIn.  Profile data does live everywhere.
    *   Router service decide which DB is accessed in which data centre using URN’s as the routing payload, and a catalog held in a DB for route the personal data request to the correct DB to retrieve the mailbox.
    *   Data centre connectivity needs to be low latency to aid this solution
    *   DB is shard (1000’s) for the 95 TeraBytes 🙂
*   Cache invalidators
    *   In the case of LinkedIn, the cache invalidator listens to DB writes to invalidate the cache, leveraging the DB [replication](https://engineering.linkedin.com/data-replication/open-sourcing-databus-linkedins-low-latency-change-data-capture-system) across data centres
*   Conflicts
    *   Soft deletes
    *   Custom conflict resolution if you can’t resolve in the data model/actors

~ by mdavey on December 15, 2015.

Posted in [Data](https://mdavey.wordpress.com/category/data/)