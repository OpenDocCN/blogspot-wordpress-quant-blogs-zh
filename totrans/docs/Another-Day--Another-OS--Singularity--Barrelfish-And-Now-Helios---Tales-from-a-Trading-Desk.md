<!--yml
category: 未分类
date: 2024-05-18 06:10:38
-->

# Another Day, Another OS: Singularity, Barrelfish And Now Helios | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2009/09/29/another-day-another-os-singularity-barrelfish-and-now-helios/#0001-01-01](https://mdavey.wordpress.com/2009/09/29/another-day-another-os-singularity-barrelfish-and-now-helios/#0001-01-01)

## Another Day, Another OS: Singularity, Barrelfish And Now Helios

Helios is an [operating system](http://www.osnews.com/story/22251/Another_Microsoft_Research_Operating_System_Helios) designed to simplify the task of writing, deploying, and tuning applications for heterogeneous platforms. Helios introduces satellite kernels, which export a single, uniform set of OS abstractions across CPUs of disparate architectures and performance characteristics. Access to I/O services such as file systems are made transparent via remote message passing, which extends a standard microkernel message-passing abstraction to a satellite kernel infrastructure. Helios retargets applications to available ISAs by compiling from an intermediate language.

~ by mdavey on September 29, 2009.

Posted in [Uncategorized](https://mdavey.wordpress.com/category/uncategorized/)
Tags: [Microsoft](https://mdavey.wordpress.com/tag/microsoft/)