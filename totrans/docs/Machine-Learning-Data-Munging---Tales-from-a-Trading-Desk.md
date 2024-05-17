<!--yml
category: 未分类
date: 2024-05-18 05:34:58
-->

# Machine Learning Data Munging | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2016/03/23/machine-learning-data-munging/#0001-01-01](https://mdavey.wordpress.com/2016/03/23/machine-learning-data-munging/#0001-01-01)

## Machine Learning Data Munging

There are at a minimum two types of data sources that you can load/[munge](http://www.slideshare.net/SparkSummit/an-introduction-to-sparkling-water-by-michal-malohlava)/explore:

1.  Data sources that already exist, and can possible be enhanced by refactoring/enhancing the application(s) that generates the data
2.  Defining the data required when the data generation will occur via a new application/platform that is being built in parallel to the Machine Learning engine

Clearly both option have their pro’s and cons’.  Option 1 at least offers a set of data which you can explore and understand missing linkages, and data holes.  Option 2 in my view is possibly a little more difficult, as you are essentially defining the data set prior to actually getting any real data from the source system(s).

Going down Option 2 road, I’ve found it helpful to leverage a few tools in an attempt to visualise the data attributes that may aid the machine learning engine.  I’ve gone though a number of mind mapping tools, which mostly free (and possibly part of the issue), have in some shape of form felt restricted, or lack an appropriate user interface 🙂

The latest tool set I’ve settled on, for at least the short term, is:

Cmap’s user experience isn’t great at all.  It’s clearly come from academia, but it does offer the ability to link concepts and label the links. XMind is graphically a lot easier on the eye, but once you start down the road of adding relationships to your mindmap, things get a bit messy.  At the end of the day, they are very different tools, aiming to tackle different problems, but they are helpful in exploring the data set that needs to be ingested into the AI engine

~ by mdavey on March 23, 2016.

Posted in [Data](https://mdavey.wordpress.com/category/data/), [Uncategorized](https://mdavey.wordpress.com/category/uncategorized/)