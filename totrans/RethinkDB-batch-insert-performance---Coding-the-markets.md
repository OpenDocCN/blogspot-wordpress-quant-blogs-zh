<!--yml
category: 未分类
date: 2024-05-12 19:30:29
-->

# RethinkDB batch insert performance | Coding the markets

> 来源：[https://etrading.wordpress.com/2016/11/21/rethinkdb-batch-insert-performance/#0001-01-01](https://etrading.wordpress.com/2016/11/21/rethinkdb-batch-insert-performance/#0001-01-01)

## RethinkDB batch insert performance

### November 21, 2016

The forthcoming cloud version of SpreadServe uses a Tornado based server to persist a breakdown of all formulae used in a spreadsheet loaded by SpreadServe. For complex sheets I found that the insertion of many formulae in the formula table could be timeconsuming. In one test scenarion a multi-formula insert took 5 minutes. So I checked out the RethinkDB’s [troubleshooting page](https://www.rethinkdb.com/docs/troubleshooting/) where there are some useful performance tips. Batch insertions with the recommended batch size of 200 brought the insert time down from 5 mins to 21 secs. Further improvements came from using soft durability and noreply, bringing the insert time down to ~3.5 secs. However, I found that my Tornado server couldn’t respond to incoming HTTP GETs while the insert coroutine was looping on the insert batches. I figured that noreply meant that the yield in the loop resumed immediately, without waiting for the reply IO from the DB. Taking out noreply allowed the single threaded server to handle HTTP GETs in the middle of an insert. If improved performance is necessary in future, splitting the Tornado server into two processes may be the way to go, but for current test scenarios performance is acceptable.