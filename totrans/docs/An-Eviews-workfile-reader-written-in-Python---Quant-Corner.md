<!--yml
category: 未分类
date: 2024-05-18 08:07:06
-->

# An Eviews workfile reader written in Python | Quant Corner

> 来源：[https://quantcorner.wordpress.com/2015/10/05/reading-eviews-workfiles-with-python/#0001-01-01](https://quantcorner.wordpress.com/2015/10/05/reading-eviews-workfiles-with-python/#0001-01-01)

**»’** **March 20h, 2016 update: the Eviews workfiles reader described below also works with Eviews9 workfiles.
»’**

*On a side note …*

In the video below, I show in action the **Eviews** workfile (***.wf1**) reader I wrote in **Python**.

There is almost no information on the **Eviews** workfiles format (it is proprietary after all…). The only resource I found out on the internet is located here: [EViews workfile format](http://ricardo.ecn.wfu.edu/~cottrell/eviews_format/) . But, I cannot say it was actually helpful. My understanding of how **Eviews** files are structured and the way data can (must?) then be extracted (the ‘algorithm’) are very different, to be honest. This probably relates to **Eviews** versions. The workfiles I worked on were created with **Eviews 8**.

For the time being, the **Python** class I wrote returns *all* the time series as a single **pandas.DataFrame** object. Alternatively, it could return a specific series (or set of series) depending on user’s needs. It is straightforward to implement.

There are pieces of information contained in **Eviews** workfiles that are left to be ‘decoded’, eg dates when objects were last updated. It is something I have even not tried to do. All I was willing here was exporting the time series/observations from  **Eviews** to **Python**.

Et voilà!

 [https://www.youtube.com/embed/0Z841f8EHlU?version=3&rel=1&showsearch=0&showinfo=1&iv_load_policy=1&fs=1&hl=es&autohide=2&wmode=transparent](https://www.youtube.com/embed/0Z841f8EHlU?version=3&rel=1&showsearch=0&showinfo=1&iv_load_policy=1&fs=1&hl=es&autohide=2&wmode=transparent)

VIDEO