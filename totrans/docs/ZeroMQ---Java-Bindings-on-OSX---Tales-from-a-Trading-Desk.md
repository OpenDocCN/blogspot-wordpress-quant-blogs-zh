<!--yml
category: 未分类
date: 2024-05-18 06:36:57
-->

# ZeroMQ + Java Bindings on OSX | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2012/08/02/zeromq-java-bindings-on-osx/#0001-01-01](https://mdavey.wordpress.com/2012/08/02/zeromq-java-bindings-on-osx/#0001-01-01)

## ZeroMQ + Java Bindings on OSX

Sometime ago I under took the joy of building ZeroMQ on OSX.  It wasn’t actually that bad an experience thanks to the usual Google assistance.  Here are the notes for anyone following:

*   Download the latest stable release from [here](http://www.zeromq.org/area:download/)
*   The “To build on UNIX-like systems” is generally correct for OSX, apart from the fact that if you don’t execute “brew install pkg-config” prior to the building, you’ll end up with the “newline token” and PKG_CHECK_MODULES error as per [stackoverflow](http://stackoverflow.com/questions/3522248/how-do-i-compile-jzmq-for-zeromq-on-osx)
*   When installing pkg-config as per above, I found I had to copy the pkg.m4 file into /usr/share/aclocal and /usr/share/aclocal-1.10 as I couldn’t be bothered to check which aclocal was being used 😦
*   With “sudo make install” [complete](http://www.zeromq.org/area:download/), go and download the Java [bindings](http://www.zeromq.org/bindings:java) for ZeroMQ
*   The building of the Java bindings is pain free, allowing a quick test to validate everything running the following in separate terminals:

> java -Djava.library.path=/usr/local/lib -classpath /usr/local/share/java/zmq.jar:../src/zmq.jar:zmq-perf.jar local_lat tcp://127.0.0.1:5555 1 100
> java -Djava.library.path=/usr/local/lib -classpath /usr/local/share/java/zmq.jar:../src/zmq.jar:zmq-perf.jar remote_lat tcp://127.0.0.1:5555 1 100

Time now to leverage ZeroMQ in some home project 😉

~ by mdavey on August 2, 2012.

Posted in [Java](https://mdavey.wordpress.com/category/languages/java/)
Tags: [Messaging](https://mdavey.wordpress.com/tag/messaging/)