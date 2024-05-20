<!--yml
category: 未分类
date: 2024-05-18 05:32:20
-->

# Stung by Python 3 – HBase and Phoenix | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2016/05/11/stung-by-python-3-hbase-and-phoenix/#0001-01-01](https://mdavey.wordpress.com/2016/05/11/stung-by-python-3-hbase-and-phoenix/#0001-01-01)

## Stung by Python 3 – HBase and Phoenix

Playing around late one night with Apache [HBase](https://hbase.apache.org/) and Apache [Phoenix](https://phoenix.apache.org/).  Couldn’t figure out what the issue was around connectivity with Phoenix.  Followed the simple [install](https://phoenix.apache.org/installation.html) instructions.  I knew HBase was running, as [simple](http://www.tutorialspoint.com/hbase/pdf/hbase_create_table.pdf) table creations worked.  However, Phoenix just didn’t want to return data 😦

Resolution.  Downgrade from Python3 to Python2.7\.  Problem solved

~ by mdavey on May 11, 2016.

Posted in [HPC](https://mdavey.wordpress.com/category/hpc/), [Languages](https://mdavey.wordpress.com/category/languages/)