<!--yml

类别: 未分类

日期: 2024-05-12 19:34:52

-->

# Satchmo on Symbiosis | Coding the markets

> 来源：[`etrading.wordpress.com/2011/12/20/satchmo-on-symbiosis/#0001-01-01`](https://etrading.wordpress.com/2011/12/20/satchmo-on-symbiosis/#0001-01-01)

## Satchmo on Symbiosis

### 2011 年 12 月 20 日

我这里有点偏题了，因为这篇文章没有与交易或金融相关的内容。然而，分享是好的，希望这能帮助到那些在使用[Django](https://www.djangoproject.com/)作为基础的 web 开发堆栈，在[Bytemark](http://www.bytemark.co.uk)的[Symbiosis](http://www.bytemark.co.uk/hosting/symbiosis)主机上挣扎的人。我正在为一个电子商务网站使用[Satchmo](http://www.satchmoproject.com/)。但是很多细节对于任何基于 Django 的网站都是适用的。如果你托管的是普通的 HTML 或 PHP，那么 Symbiosis 就很好。如果你想要运行 Satchmo 或 Django，你需要做更多的工作，因为 Symbiosis 是 Bytemark 自己的 Debian Lenny 发行版，带有 Python 2.5 和没有 GCC。我正在部署的电子商务网站是使用 Python 2.7.2，Django 1.3.1 和 Satchmo 0.9.2 开发的。所以我需要从头开始构建整个东西，从 apt-get 安装 GCC 和 Python 2.7.2 源码开始。这是我遵循的配方。请注意，我省略了所有特定于目录树的 cds、gunzips 和“tar xvf”的命令，但保留了所有可能花费很长时间才能弄清楚的琐碎 cmd 行选项...

```
## GCC + Python 1.7
apt-get install gcc-4.3
wget www.python.org/ftp/python/2.7.2/Python-2.7.2.tgz
# We need to bld Python with zlib support compiled in, otherwise 
# Satchmo's easy_install setuptools with fail with a zlib ImportError.
# Check that /usr/include/zlib.h exists
apt-get install zlib1g-dev
# We need the mercurial hg client to pull stuff off bitbucket repositories
apt-get install mercurial
# Also get pip installer
wget http://python-distribute.org/distribute_setup.py
python distribute_setup.py
wget https://raw.github.com/pypa/pip/master/contrib/get-pip.py
python get-pip.py
# Now build Python
./configure -with-zlib=/usr/include
make
make install 
# Python 2.7.2 is now the default on this host
## sqlite 2.6.3 - not a std part of Linux source build
apt-get install libsqlite3-dev
wget pysqlite.googlecode.com/files/pysqlite-2.6.3.tar.gz
python setup.py install
## Django
wget https://www.djangoproject.com/download/1.3.1/tarball
python setup.py install
python
>>> import django
## Satchmo
wget https://bitbucket.org/chris1610/satchmo/get/v0.9.1.tar.gz
# gunzip, untar then follow Satchmo install notes. First, get easy_install. This will fail if
# you didn't get the zlib stuff right.
wget pypi.python.org/packages/2.7/s/setuptools/setuptools-0.6c11-py2.7.egg
sh setuptools-0.6c11-py2.7.egg
easy_install pycrypto
easy_install http://www.satchmoproject.com/snapshots/trml2pdf-1.2.tar.gz
easy_install django-registration
wget effbot.org/downloads/Imaging-1.1.7.tar.gz
python setup.py install
# ReportLab
wget www.reportlab.com/ftp/reportlab-2.5.tar.gz
python setup.py install
hg clone http://bitbucket.org/bkroeze/django-threaded-multihost/
python setup.py install
hg clone http://bitbucket.org/bkroeze/django-caching-app-plugins/
python setup.py install
pip install sorl-thumbnail==3.2.5
hg clone http://bitbucket.org/bkroeze/django-signals-ahoy/
python setup.py install
hg clone http://bitbucket.org/bkroeze/django-livesettings/
python setup.py install
hg clone http://bitbucket.org/bkroeze/django-keyedcache/
python setup.py install
hg clone http://bitbucket.org/chris1610/satchmo/
python setup.py install
python
>>> import django
>>> import satchmo_store
# Now clone the default Satchmo store
python scripts/clonesatchmo.py
python manage.py runserver
# Fix Symbiosis firewall to allow incoming on port 8000
# http://symbiosis.bytemark.co.uk/docs/ch-reference-firewall.html
cd /etc/symbiosis/firewall/incoming-d
touch 11-8000
firewall
# Finally, run satchmo. Note 0.0.0.0 to be available to any connection
python manage.py runserver 0.0.0.0:8000
```
