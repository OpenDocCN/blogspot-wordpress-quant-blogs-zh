<!--yml
category: 未分类
date: 2024-05-18 06:02:37
-->

# RXJava Airplane Coding | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2013/08/19/rxjava-airplane-coding/#0001-01-01](https://mdavey.wordpress.com/2013/08/19/rxjava-airplane-coding/#0001-01-01)

## RXJava Airplane Coding

Managed to get a few hours in during the long return flight from Sydney to London.  Most of the coding was around enhanced [scenario](http://cukes.info/) testing and refactoring the underlying codebase to further leverage [RxJava](https://github.com/Netflix/RxJava).  Ran into a curious “box type” cucumber error, which due to not having download the full documentation pre-flight, was luckily resolved via a spelling correct in the .feature file.

Observable.[Zip](https://github.com/Netflix/RxJava/wiki/Combining-Observables#zip) allowed me to combine two observables, but I’ve now realised that that isn’t exactly what I want to do.  I really want a “select” across two Observables – still pondering on that one.

~ by mdavey on August 19, 2013.

Posted in [Java](https://mdavey.wordpress.com/category/languages/java/)