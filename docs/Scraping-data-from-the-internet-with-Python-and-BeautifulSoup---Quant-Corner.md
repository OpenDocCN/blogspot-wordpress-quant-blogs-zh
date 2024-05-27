<!--yml

类别：未分类

日期：2024 年 5 月 18 日 08:08:21

-->

# 使用 Python 和 BeautifulSoup 从互联网抓取数据 | 量化角落

> 来源：[`quantcorner.wordpress.com/2014/03/05/scraping-data-from-the-internet-with-python-and-beautifulsoup/#0001-01-01`](https://quantcorner.wordpress.com/2014/03/05/scraping-data-from-the-internet-with-python-and-beautifulsoup/#0001-01-01)

我需要中伊利诺伊州粗大黄豆油价格的每日时间序列（是的，我需要……）。经过一番搜索，我发现我需要的数据在[Iowa 农场局](http://www.iowafarmbureau.com "Iowa 农场局")的网站上可获得。

具体来说，没有可用的时间序列，但可以通过玩弄 URL 来访问数据。这是**Python**和**BeautifulSoup**的一个案例！

下面提供的代码片段非常直接，可以轻松地根据特定需求进行修改。没有优化或异常机制。那只是在做工作。

![爱荷华农场局](https://quantcorner.wordpress.com/wp-content/uploads/2014/03/iowa_farm_bureau.jpg)

```

```

##################################################

# Edouard TALLENT @TaGoMa . Tech, March, 2014    #

# 抓取中伊利诺伊州粗大黄豆油价格 #

# from http://markets.iowafarmbureau.com/        #

# 量化角落 @ https://quantcorner.wordpress.com #

##################################################

# 所需标题

import urllib2                          # 读取网页

from bs4 import BeautifulSoup           # bs4 函数

import time                             # 时间，流逝时间

import re                               # 正则表达式，删除字符

# 将包含所需数据的数组

#d = []      # 日期

#l = []      # 最低价

#h = []      # 最高价

# URL

start_urls = 4539   # 最新的网页开始解析

nb_quotes = 200     # 所需行情数

for urls in range (start_urls, start_urls - nb_quotes, -1):

    # 开始时间

    start_time = time.time()

    # 构造 URL 字符串

    url = 'http://markets.iowafarmbureau.com/pages/usdacash.php?id=' + str(urls)

    # 读取 HTML 页面内容

    page = urllib2.urlopen(url)

    # 创建一个 beautifulsoup 对象

    soup = BeautifulSoup(page)

    # 在整个 HTML 代码中搜索要解析的表格

    tables = soup.findAll('table')

    tab = tables[1]                 # 这是要解析的表格

    # 搜索日期

    # <option value='4539'>2014 年 3 月 3 日</option>

    date = str(soup.find('option', {'value' : str(urls)}).string)

    # 在 tab 中获取所需单元格的内容

    # http://www.briancarpio.com/2012/12/02/website-scraping-with-python-and-beautiful-soup/

    '''

    <td>粗大黄豆油</td>

    <td>处理器</td>

    <td>+40.01</td>

    <td>+40.36</td>

    <td>

    '''

    low_tmp = str(tab.findAll('tr')[8].findAll('td')[2].string)     # 最低价格

    low = re.sub('[+]', '', low_tmp)                                # 移除'+'符号

    high_tmp = str(tab.findAll('tr')[8].findAll('td')[3].string)    # 最高价格

    高值 = re.sub('[+]', '', 高值 _tmp)                              # 移除 '+' 符号

    # 停止时间

    停止时间 = 时间.time()

    # 在屏幕上打印输出

    打印日期，'\t'，低值，'\t'，高值，'(%0.1f 秒)' % (停止时间 - 开始时间)

    ## 将解析的值存储在数组中以供以后使用

    #d.append(date)

    #l.append(low)

    #h.append(high)

```

```
