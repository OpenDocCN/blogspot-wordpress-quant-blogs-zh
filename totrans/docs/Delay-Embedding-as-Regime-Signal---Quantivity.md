<!--yml
category: 未分类
date: 2024-05-18 13:44:50
-->

# Delay Embedding as Regime Signal | Quantivity

> 来源：[https://quantivity.wordpress.com/2011/02/24/delay-embedding-as-regime-signal/#0001-01-01](https://quantivity.wordpress.com/2011/02/24/delay-embedding-as-regime-signal/#0001-01-01)

Infantino and Itzhaki, in their 2010 thesis [Developing High-Frequency Equities Trading Models](http://hdl.handle.net/1721.1/59122), utilize a regime switching signal based upon *time delay embedding*. The intuition underlying this signal and use for [regime discovery](https://quantivity.wordpress.com/2010/02/15/regime-discovery/) are unexpectedly interesting.

![](img/66e02853c93ae3c34473e9caa1f85ce3.png) Conceptually, their signal is framed within the context of a *two-state switching regime* (interpreted in the classic technical sense): “momentum” or “mean reversion”. With high frequency equities portfolio data, they informally observe the familiar *volatility-regime correlation*: high volatility implies momentum (*e.g.* herd effects), low volatility implies mean reversion (*e.g.* market making).

In their words: “﻿﻿As the short-term changes in ![\sigma_D](img/6ef5edabc294ebb43f646fdc40b87602.png) appeared to be more pronounced — identified by very narrow peaks in the ![\sigma_D](img/6ef5edabc294ebb43f646fdc40b87602.png) time series — cumulative returns from the basic mean-reverting strategy seemed to decrease” (p. 44). Note ![\sigma_D](img/6ef5edabc294ebb43f646fdc40b87602.png) is a measure of cross-sectional volatility on dimensionally reduced returns (*i.e.* standard deviation of returns projected on dominant PCA eigenvectors). This relationship is illustrated in the right graphic.

How they translate this intuitive volatility-regime correlation into a switching signal is the fun part. They define the difference of ![\sigma_D ](img/caace9246a12cff17c95ed38373b7ec8.png) as ![\psi ](img/a76477d843f3ce875b5fc793ca03e55f.png), then define the following distance metric (illustrated in left image):

     ![E_H (t) = \sqrt{\sum\limits_{i=1}^H{[\psi(t - i)]^2}} = \sqrt{\sum\limits_{i=1}^H{[\sigma_D(t - i) - \sigma_D (t - i - 1)]^2}} ](img/a791147f939bc1094f96932289a5adeb.png)

This is an interesting starting point, as [dynamical systems](http://en.wikipedia.org/wiki/Dynamical_system) reminds us that ![\psi(t - i) ](img/21b24d179988310127c77ec810471531.png) is a *phase space reconstruction for ![\sigma_D ](img/caace9246a12cff17c95ed38373b7ec8.png)*, given ![\psi ](img/a76477d843f3ce875b5fc793ca03e55f.png) is the delayed chain of discrete i.i.d. steps walking backwards in time for ![\sigma_D ](img/caace9246a12cff17c95ed38373b7ec8.png). In other words, the following are vectors reconstructing the volatility from which mutual distance is being measured for each observed time ![t ](img/e44a5d7c103f4698c89ecb47d7333f49.png):

![[ \psi(t - 1), \psi(t - 2), \cdots , \psi(t - H) ] ](img/25fdcccc0ca0f19bd694ec7f3534bcf7.png)

![](img/759c9267035a7f1a872791593b6375a5.png) From which they define a *binary regime signal* ![\omega ](img/5d0885d2568a295726f5f91b4f8af64a.png) as the positive first difference of ![E_H(t) ](img/0fcc121de72a9d71ecd8a7952b3a3b25.png):

    ![\omega = [ E_H(t) - E_H(t - 1) ] > 0 ](img/358a491cf76e06eb79ddc1005231f658.png)

From which the regime switch is defined: ![\omega > 0 ](img/b21206309c05d0697128103f6ea7c7c8.png) indicates volatility is increasing and thus a “momentum” regime is appropriate. On the contrary, ![\omega \le 0 ](img/2db64cd6ec77e13ba337830f94a4b1e2.png) indicates volatility is decreasing and thus a “mean-reverting” regime is appropriate.

This signal is quite interesting when considered within the larger context of several familiar time series analysis traditions:

Undoubtedly not by accident, the authors conveniently omit their choice of embedding dimension ![H ](img/476b7639b127a2941791628e4786c510.png). Such is presumably left as an exercise for the reader, as selecting optimal embedding dimension is indeed well-known to be one of the most significant challenges in reconstruction.