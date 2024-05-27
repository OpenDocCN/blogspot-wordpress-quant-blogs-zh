<!--yml

分类：未分类

日期：2024-05-18 15:43:24

-->

# 用 Python 交易：如何下载一堆 csv 文件

> 来源：[`tradingwithpython.blogspot.com/2011/10/how-to-download-bunch-of-csv-files.html#0001-01-01`](http://tradingwithpython.blogspot.com/2011/10/how-to-download-bunch-of-csv-files.html#0001-01-01)

我将分析 VIX 期货数据，因此首先，我需要 CBOE 的所有文件。他们对于文件名使用一致的格式，这很容易生成。以下脚本创建一个数据目录，然后下载 2004-2011 年间的所有 csv 文件。正如你所看到的，不需要太多的编码，不到 30 行！

```
from urllib import urlretrieve
import os

m_codes = ['F','G','H','J','K','M','N','Q','U','V','X','Z'] #month codes of the futures
dataDir = os.getenv("USERPROFILE")+'\\twpData\\vixFutures' # data directory

def saveVixFutureData(year,month, path):
    ''' Get future from CBOE and save to file '''
    fName = "CFE_{0}{1}_VX.csv".format(m_codes[month],str(year)[-2:])
    urlStr = "http://cfe.cboe.com/Publish/ScheduledTask/MktData/datahouse/{0}".format(fName)

    try:
        urlretrieve(urlStr,path+'\\'+fName)
    except Exception as e:
        print e

if __name__ == '__main__':
    if not os.path.exists(dataDir):
        os.makedirs(dataDir)

    for year in range(2004,2012):
        for month in range(12):
            print 'Getting data for {0}/{1}'.format(year,month)
            saveVixFutureData(year,month,dataDir)

    print 'Data was saved to {0}'.format(dataDir)

```
