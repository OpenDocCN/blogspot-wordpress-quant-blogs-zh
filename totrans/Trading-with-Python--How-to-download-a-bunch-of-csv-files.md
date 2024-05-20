<!--yml
category: 未分类
date: 2024-05-18 15:43:24
-->

# Trading with Python: How to download a bunch of csv files

> 来源：[http://tradingwithpython.blogspot.com/2011/10/how-to-download-bunch-of-csv-files.html#0001-01-01](http://tradingwithpython.blogspot.com/2011/10/how-to-download-bunch-of-csv-files.html#0001-01-01)

I'll be analyzing VIX futures data, so to start with, I need all the files from CBOE. They use a consistent format for file names, which is easy to generate. The following script creates a data directory and then downloads all csv files for the period 2004-2011\. As you can see, not much coding is required, less than 30 lines!

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