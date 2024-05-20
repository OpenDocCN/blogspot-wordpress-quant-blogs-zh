<!--yml
category: 未分类
date: 2024-05-18 05:28:18
-->

# Know Your Stack – Neo4j | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2017/02/22/know-your-stack-neo4j/#0001-01-01](https://mdavey.wordpress.com/2017/02/22/know-your-stack-neo4j/#0001-01-01)

## Know Your Stack – Neo4j

Sometimes things go south in production.  Often its a combination of events that have generated a perfect storm.  The storm being production outages that are difficult to diagnose due to lack of understanding of the application stack, tools, and knowledge.

When attempting to diagnose an issue, its important to piece together the situation though evidence – log files, monitoring tools, etc.  Your own codebase can often be improved with appropriate logging and inclusion of monitoring tools/UI’s.  Issues often come about with off-the-shelf products, and lack of knowledge around how to understand the inner workings.  One example in Neo4j.  What follows is a few hopefully helpful suggestion to understand what is going on in your application stack:

*   Neo4j has a query.log which is extremely useful in tailing to view the queries being run, and the time to execute each query.
*   Neo4j browser (port 7474 by default) has a “:play sysinfo” which has some basic information that can prove useful e.g the Transaction tile, and in particular “Current”.  If Current remains move than 0 for a duration, when you expect it to be 0, you could have long running transactions 😦
*   Neo4j 3.1+ has improved query management.  In particular its now possible to see what queries are [running](https://neo4j.com/docs/operations-manual/current/monitoring/query-management/procedures/?_ga=1.17453689.1953165753.1485254392#query-management-list-queries), and kill queries if required
*   Reading documentation before using a product is key.  Remember the Open [Files](https://support.neo4j.com/hc/en-us/articles/222587167-How-do-I-set-max-open-files-for-Debian-installs) for Neo4j.

~ by mdavey on February 22, 2017.

Posted in [Languages](https://mdavey.wordpress.com/category/languages/), [Uncategorized](https://mdavey.wordpress.com/category/uncategorized/)