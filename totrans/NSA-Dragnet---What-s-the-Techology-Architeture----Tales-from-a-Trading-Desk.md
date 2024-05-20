<!--yml
category: 未分类
date: 2024-05-18 06:02:58
-->

# NSA Dragnet – What’s the Techology Architeture? | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2013/08/11/nsa-dragnet-whats-the-techology-architeture/#0001-01-01](https://mdavey.wordpress.com/2013/08/11/nsa-dragnet-whats-the-techology-architeture/#0001-01-01)

## NSA Dragnet – What’s the Techology Architeture?

Most of us have probably read something about Snowden and the NSA data collection.  ACLU’s recent [article](http://www.aclu.org/blog/national-security/guide-what-we-now-know-about-nsas-dragnet-searches-your-communications), “A Guide to What We Now Know About the NSA’s Dragnet Searches of Your Communications”, provides the usual high level view of the data collection, analysis and searching features that the NSA have at their disposal.  Like possible numerous other software engineers, I’m curious as to the architecture, and technology in use.  Specifically, the data storage, the amount of real-time compared to off-line processing, etc

Based on the ACLU article alone, one could make the following (in-correct) assumptions:

*   Assuming network taps are one of the sources of data collection, based on the X-KEYSCORE “Where” slide, it sounds like the data is stored locally where its collected.
*   Data collection via UpStream cable taps would I assume break the data into both content and meta data (IP address’s, email address, keywords etc.) and store the data for further processing, or just search retrieval
*   PRISM data collection sounds more like an application tap, routed into the infrastructure as per the above two points.  Again its unclear if data storage for PRISM is local to each PRISM tap, or back to a single data repository
*   You could see how [hadoop](http://hadoop.apache.org/) and other similar technologies from the open source community could aid the NSA in processing the data collected.  However, hadoop across multiple data centres located globally would incur some latency.
*   “wiretap anyone, from you or your accountant” should be of no shock given the NSA has the stated application and network taps, its effectively a [continuous](http://coherence.oracle.com/display/COH31UG/Continuous+Query) query against the NSA’s data source to get a real-time view for the data requested

The above is basic at best based on the flight I’ve just got off, but I’d be curious if anyone reading this blog has found further writing on the hypothetical technology being used by the NSA to process the “big-data” problem they would clearly have

~ by mdavey on August 11, 2013.

Posted in [Uncategorized](https://mdavey.wordpress.com/category/uncategorized/)
Tags: [BigData](https://mdavey.wordpress.com/tag/bigdata/), [NSA](https://mdavey.wordpress.com/tag/nsa/)