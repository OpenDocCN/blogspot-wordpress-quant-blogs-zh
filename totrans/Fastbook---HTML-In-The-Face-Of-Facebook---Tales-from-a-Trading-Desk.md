<!--yml
category: 未分类
date: 2024-05-18 06:31:20
-->

# Fastbook – HTML In The Face Of Facebook | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2013/01/07/fastbook-html-in-the-face-of-facebook/#0001-01-01](https://mdavey.wordpress.com/2013/01/07/fastbook-html-in-the-face-of-facebook/#0001-01-01)

## Fastbook – HTML In The Face Of Facebook

Curious read over on the Sencha [blog](http://www.sencha.com/blog/the-making-of-fastbook-an-html5-love-story) – Mark Zuckerberg HTML5 view vs Sencha HTML5 view.  What’s nice about the Sencha Fastbook PoC is the resulting video:

> four-minute video gives you a quick overview of Sencha Fastbook, and shows you a side-by-side comparison of how well our HTML5 app performs against both the native iOS and the native Android Facebook apps

Reading the blog posting, its worrying to find that “much of the application was still raw HTML pages” – did Facebook forget to read the HTML/JS best practices guide?  Part of Fastbook’s solution is leveraging the sandbox container to allow partitioning of the DOM tree, rending the partitions in separate iFrames.  However, the sandbox container isn’t a silver bullet, and needs to be used appropriately given the proxied calls between parent window and sandbox.

Another surprise is the amount of news feed data Sencha found that is being transferred from Facebook::

> In average, 15KB to 20KB of gzipped JSON data is transferred for every 10 items, much of that is not needed to render the actual views.

Web workers also make an appearance in the area of networking and serialization.

~ by mdavey on January 7, 2013.

Posted in [JavaScript](https://mdavey.wordpress.com/category/languages/javascript/)