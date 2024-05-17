<!--yml
category: 未分类
date: 2024-05-12 19:30:40
-->

# Starting out with RethinkDB | Coding the markets

> 来源：[https://etrading.wordpress.com/2016/04/21/starting-out-with-rethinkdb/#0001-01-01](https://etrading.wordpress.com/2016/04/21/starting-out-with-rethinkdb/#0001-01-01)

## Starting out with RethinkDB

### April 21, 2016

I’ve been wanting to use [RethinkDB](https://rethinkdb.com/) for the cloud based [SpreadServe](http://spreadserve.com/) service offering for sometime, so when I heard the Windows version had gone into beta there was no excuse for further delay. NoSQL DBs are all the rage now, with [Mongo](https://www.amon.cx/blog/rethinkdb-reviewed-by-a-mongo-fan/), [Cassandra, Couch and Redis](http://kkovacs.eu/cassandra-vs-mongodb-vs-couchdb-vs-redis) to choose from. For me, RethinkDB stood out from the crowd for several reasons. Firstly, its [changefeeds](https://rethinkdb.com/docs/changefeeds/python/). All distributed systems have to resolve the challenge of keeping process caches in sync with the DB. I’ve seen two quality hand rolled solutions to this at major banks in the past few years. One based on SQL Server triggers that caused pub sub broadcasts of XML formatted updated or inserted rows. And on [JP Morgan’s Athena](http://techcareers.jpmorgan.com/cm/BlobServer/athena_jpmc.pdf) project I saw [Twisted](https://github.com/twisted/twisted) object serialisaton used to update socket subscribers with recently changed objects. Both approaches scaled up well. What makes RethinkDB special is that it solves that problem for you out of the box with changefeeds. The second appealing feature of RethinkDB for me is that the Python API is a first class citizen andnot an afterthought. The Python API’s event handling and coroutine implementation style is neatly integrated with [Tornado](http://www.tornadoweb.org/en/stable/), which I’m also using in SpreadServe. And thirdly, I liked the fact that RethinkDB’s core implementation is in C++, and is open source. Like RethinkDB, and like JP’s Athena for that matter, SpreadServe is C++ on the inside with Python APIs.

So I’ve been working with the [RethinkDB 2.3.0 beta build for Windows](https://rethinkdb.com/docs/install/windows/) for a few days now. I’ve been delighted by several aspects of Rethink, and I’ve hit a few gotchas. I’ve also realised that the shift to coroutine based coding is a big, big deal. So let me lay that out here, for the record. First, the things that have delighted me…

*   Very simple install process
*   Nice docs
*   Great admin UI: the data explorer is very good.

And here are the gotchas that I hit…

*   When coding in Python, don’t forget a .run( ) on the end of your r.table( ).get( ) or r.table( ).insert( )
*   Method names aren’t consistent across APIs. For instance getAll( ) in JS is get_all( ) in Python. Even if you’re coding in Python, as I am, you’ll still find yourself using JS in the admin GUI’s data explorer, so this is an irritation.
*   You need tornado 4 or better as RethinkDB’s Tornado integration imports tornado.tcpclient, which isn’t in 3.x. It took me a while to track down as the server process which I was connecting to RethinkDB was exiting silently, with no trace of an import error in log or console. However, Python docs do say that imp.load_module( ), as used in r.set_loop_type( ) can throw ImportError. Once I got a try/except clause around r.set_loop_type( ) I caught the exception and realised I needed to upgrade from Tornado 3.2 to 4.2.1.

Once I was past the gotchas I realised I needed to upgrade my coding style to embrace coroutines. They’ve been in Python since 2.7, and Tornado has adopted them. They’re all over the RethinkDB examples. I’ve been coding in a single or low threaded async callback style for at least ten tears now, having realised that the multiple blocking worker thread approach is horribly inefficient and prone to deadlocks and races. But all my code has been very callback oriented, and coroutines are a big shift away from that. One of my big challenges over the last few days has been figuring out how to combine the two styles. I have my own C++ & Python framework with uses a single threaded async style. And I’ve got a load of Tornado based code in the same style. Now I need to combine that with RethinkDB code written in a coroutine style. I found this fantastic blog post with detailed commentary on refactoring a bunch of callback style Tornado code to use coroutines: [https://emptysqua.re/blog/refactoring-tornado-coroutines/](https://emptysqua.re/blog/refactoring-tornado-coroutines/)

It’s been invaluable. One mistake I’ve made is thinking that Rethink/Tornado coroutines can be invoked directly like generators. They can’t, you must use loop.add_callback( ) to schedule them. I’ll be back with more as I explore RethinkDB and coroutines more, and I aim to post more code samples like this [gist of a minimal, complete Tornado Web Server](https://gist.github.com/osullivj/e0faf2348528285a388b74e398307bae) with RethinkDB changefeed.