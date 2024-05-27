<!--yml

分类：未分类

日期：2024-05-12 19:34:45

-->

# mod_wsgi 在 Symbiosis 上的应用 | 编码市场

> 来源：[`etrading.wordpress.com/2012/01/08/mod_wsgi-on-symbiosis/#0001-01-01`](https://etrading.wordpress.com/2012/01/08/mod_wsgi-on-symbiosis/#0001-01-01)

## mod_wsgi 在 Symbiosis 上的应用

### 2012 年 1 月 8 日

Bytemark 的 Symbiosis Linux 在其 Apache2 部署中没有安装 mod_wsgi。为了使其与我从源代码构建的 Python 2.7 一起工作，我不得不也从源代码构建 mod_wsgi。mod_wsgi 的 Makefile 需要 Apache 的 apxs2 工具，而这个工具并不在标准的 Symbiosis 中。幸运的是，这个工具在 apache-threaded-dev 包中。以下是我用来使 mod_wsgi 工作的步骤…

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
