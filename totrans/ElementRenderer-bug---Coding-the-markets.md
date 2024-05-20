<!--yml
category: 未分类
date: 2024-05-12 19:41:38
-->

# ElementRenderer bug | Coding the markets

> 来源：[https://etrading.wordpress.com/2008/08/14/elementrenderer-bug/#0001-01-01](https://etrading.wordpress.com/2008/08/14/elementrenderer-bug/#0001-01-01)

## ElementRenderer bug

### August 14, 2008

Just fixed a renderer bug, so I feel like I’m getting traction with my [Caplin Trader](http://www.caplin.com/caplintrader/) [Firebug](http://getfirebug.com/) [JavaScript](http://developer.mozilla.org/en/docs/Core_JavaScript_1.5_Guide) dev environment. Fixing that bug has allowed me to invoke a [DataSource](http://www.freeliberator.com/documentation/DataSourceJava/javadoc/index.html) subscription request via the [Liberator](http://www.freeliberator.com/) in one of my server components. Which happily is coded in [Python](http://www.python.org/). With JavaScript in the client, and Python on the server side, we should have a very flexible environment for ad hoc client/server RPC.

The [SL4B](http://lib1.freeliberator.com/docs/sl4b/jsdoc/overview-summary.html) docs online at [freeliberator](http://lib1.freeliberator.com/) are proving very handy. It’s easy to find stuff by pasting classes and methods into my Google toolbar. It would be good to see all Caplin docs fully indexed by Google…