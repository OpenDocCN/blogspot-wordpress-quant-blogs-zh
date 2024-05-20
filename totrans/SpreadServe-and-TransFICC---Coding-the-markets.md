<!--yml
category: 未分类
date: 2024-05-12 19:29:32
-->

# SpreadServe and TransFICC | Coding the markets

> 来源：[https://etrading.wordpress.com/2017/08/11/spreadserve-and-transficc/#0001-01-01](https://etrading.wordpress.com/2017/08/11/spreadserve-and-transficc/#0001-01-01)

## SpreadServe and TransFICC

### August 11, 2017

Earlier in the summer I did a POC integration of [SpreadServe](http://spreadserve.com) with [TransFICC](http://transficc.com). For those unfamiliar, TransFICC has an ex-[LMAX](https://etrading.wordpress.com/disruptor/) founding team, and is a new entrant in the ECN gateway space. Technically their key differentiators are cloud hosting and high performance engineering techniques. For Transficc clients the only thing running on premises is the Java API, which puts the same orthogonalised interface on all the usual fixed income ECNs, and connects to the cloud hosted gateway processes.

It’s been a while since I built anything non trivial in Java, so I was pleasantly surprised by how improved the Java ecosystem has become. [Gradle](http://gradle.org) has transformed dependency and package management. And the single threaded async approach popular in the Python and C++ worlds has finally made it to Java with [Netty](https://netty.io). You can find the code [on GitHub here](https://github.com/SpreadServe/TFWebSock).