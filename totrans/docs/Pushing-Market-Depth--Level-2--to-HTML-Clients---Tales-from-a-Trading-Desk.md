<!--yml
category: 未分类
date: 2024-05-18 05:42:41
-->

# Pushing Market Depth (Level 2) to HTML Clients | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2015/05/01/pushing-market-depth-level-2-to-html-clients/#0001-01-01](https://mdavey.wordpress.com/2015/05/01/pushing-market-depth-level-2-to-html-clients/#0001-01-01)

## Pushing Market Depth (Level 2) to HTML Clients

Lightstreamer recently [published](http://blog.lightstreamer.com/2015/04/market-depth-with-lightstreamer.html#dontscroll84930) an article on pushing Level 2 market data to a HTML client.  An interesting article with offers the read source code and appropriate commentary on how the demo works.  What I think is missing, and maybe Lightstreamer can update the article in the future, is in my view the following:

*   Performance numbers for both websockets and non-websockets
*   Links from the article to other articles Lightstreamer might have on Data Adapter and filtering.  Filtering is particularly key when the client (HTML) become overwhelmed with data, and can’t keep up with paints (renders)
*   Commentary on disconnect of the client and reconnect and the impact on the market data feed.  Likewise commentary on server (adapter death) and the performance of fail-over, recovery
*   Bandwidth usage

Overall, an interesting article

~ by mdavey on May 1, 2015.

Posted in [Java](https://mdavey.wordpress.com/category/languages/java/), [JavaScript](https://mdavey.wordpress.com/category/languages/javascript/), [Trading](https://mdavey.wordpress.com/category/trading/)