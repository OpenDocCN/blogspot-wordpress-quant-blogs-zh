<!--yml
category: 未分类
date: 2024-05-12 19:34:52
-->

# Satchmo on Symbiosis | Coding the markets

> 来源：[https://etrading.wordpress.com/2011/12/20/satchmo-on-symbiosis/#0001-01-01](https://etrading.wordpress.com/2011/12/20/satchmo-on-symbiosis/#0001-01-01)

## Satchmo on Symbiosis

### December 20, 2011

I’m going a little bit off topic here, as this post has no trading or finance content. However, it’s good to share, and hopefully this will help anyone out there struggling with a [Django](https://www.djangoproject.com/) based web dev stack on a [Bytemark](http://www.bytemark.co.uk) [Symbiosis](http://www.bytemark.co.uk/hosting/symbiosis) host. I’m using [Satchmo](http://www.satchmoproject.com/) for an ecommerce site. But a lot of the detail will be applicable to any Django based web site. If you’re hosting plain old HTML, or PHP, then Symbiosis is fine and dandy. If you want to get Satchmo or Django running you’ve got a bit more work to do as Symbiosis is Bytemark’s own Debian Lenny distro with Python 2.5 and no GCC. The ecommerce site I’m deploying has been developed with Python 2.7.2, Django 1.3.1 and Satchmo 0.9.2\. So I needed to build up the whole thing from scratch, starting with an apt-get for GCC and a Python 2.7.2 source build. Here’s the recipe I followed. Note that I’m omitting all the directory tree specific cds, gunzips and ‘tar xvf’s from the commands, but leaving in all the fiddly cmd line options that can take ages to figure out…

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