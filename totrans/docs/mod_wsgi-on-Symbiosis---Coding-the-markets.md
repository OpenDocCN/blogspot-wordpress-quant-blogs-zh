<!--yml
category: 未分类
date: 2024-05-12 19:34:45
-->

# mod_wsgi on Symbiosis | Coding the markets

> 来源：[https://etrading.wordpress.com/2012/01/08/mod_wsgi-on-symbiosis/#0001-01-01](https://etrading.wordpress.com/2012/01/08/mod_wsgi-on-symbiosis/#0001-01-01)

## mod_wsgi on Symbiosis

### January 8, 2012

Bytemark’s Symbiosis Linux doesn’t have mod_wsgi installed in its Apache2 deployment. To make it work with the Python 2.7 I built from source I  had to build mod_wsgi from source too. mod_wsgi’s Makefile needs Apache’s apxs2 tool, which isn’t in the standard Symbiosis. Fortunately that is in the apache-threaded-dev package. Here are the steps I used to make mod_wsgi work…

```
# get apxs2 so we can install mod-wsgi from source. Needs to be built from source to
# get the Python.h from the Python we built from source.
sudo apt-get install apache2-threaded-dev
# for mod_wsgi: configure should find apxs2
# the soft link is needed so that libtool can find gcc
./configure 
 ln -s /usr/bin/gcc-4.3 /usr/bin/i486-linux-gnu-gcc
 make
 make install
 /etc/init.d/apache2 restart
```