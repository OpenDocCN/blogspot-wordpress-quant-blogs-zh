<!--yml

类别：未分类

日期：2024-05-18 15:42:59

-->

# 用 Python 交易：从 CBOE 期货数据重建 VXX

> 来源：[`tradingwithpython.blogspot.com/2012/01/reconstructing-vxx-from-cboe-futures.html#0001-01-01`](http://tradingwithpython.blogspot.com/2012/01/reconstructing-vxx-from-cboe-futures.html#0001-01-01)

博客圈中的许多人重建了 VXX，以了解它成立之前的表现如何。进行此操作的程序并不复杂，在 VXX prospectus 和上面

智能投资者博客[`investing.kuchita.com/2011/08/16/how-the-vxx-is-calculated-and-why-backwardation-amplfies-it/`](http://investing.kuchita.com/2011/08/16/how-the-vxx-is-calculated-and-why-backwardation-amplfies-it/)

手动进行这项工作是非常繁琐的，需要分别下载每个期货的数据，然后在电子表格中合并它们等。

下面的脚本自动化了这一过程。第一个脚本，

*下载 VixFutures.py*

从 cboe 获取数据，将每个文件保存到数据目录中，然后将它们合并到一个 csv 文件中，

*vix_futures.csv*

第二个脚本

*重建 VXX.py*

解析了

*vix_futures.csv,*

计算 VXX 的日收益并保存结果到

*重建 VXX.csv*

。

为了检查计算结果，我将我的模拟结果与 SPVXSTR 指数数据进行了比较，两者相当一致，请看下面的图表。

**注意：我可以提供费用支持来运行代码或创建一个独立程序，如果你有兴趣请联系我。**

--------------------------------源代码--------------------------------------------

从 CBOE 获取期货数据并将它们合并到一个表中的代码

*下载 VixFutures.py*

```
#-------------------------------------------------------------------------------
# Name:        download CBOE futures
# Purpose:     get VIX futures data from CBOE, process data to a single file
#
#
# Created:     15-10-2011
# Copyright:   (c) Jev Kuznetsov 2011
# Licence:     BSD
#-------------------------------------------------------------------------------
#!/usr/bin/env python

from urllib import urlretrieve
import os
from pandas import *
import datetime
import numpy as np

m_codes = ['F','G','H','J','K','M','N','Q','U','V','X','Z'] #month codes of the futures
codes = dict(zip(m_codes,range(1,len(m_codes)+1)))

dataDir = os.path.dirname(__file__)+'/data'

def saveVixFutureData(year,month, path, forceDownload=False):
    ''' Get future from CBOE and save to file '''
    fName = "CFE_{0}{1}_VX.csv".format(m_codes[month],str(year)[-2:])
    if os.path.exists(path+'\\'+fName) or forceDownload:
        print 'File already downloaded, skipping'
        return

    urlStr = "http://cfe.cboe.com/Publish/ScheduledTask/MktData/datahouse/{0}".format(fName)
    print 'Getting: %s' % urlStr
    try:
        urlretrieve(urlStr,path+'\\'+fName)
    except Exception as e:
        print e

def buildDataTable(dataDir):
    """ create single data sheet """
    files = os.listdir(dataDir)

    data = {}
    for fName in files:
        print 'Processing: ', fName
        try:
            df = DataFrame.from_csv(dataDir+'/'+fName)

            code = fName.split('.')[0].split('_')[1]
            month = '%02d' % codes[code[0]]
            year = '20'+code[1:]
            newCode = year+'_'+month
            data[newCode] = df
        except Exception as e:
            print 'Could not process:', e

    full = DataFrame()
    for k,df in data.iteritems():
        s = df['Settle']
        s.name = k
        s[s<5] = np.nan
        if len(s.dropna())>0:
            full = full.join(s,how='outer')
        else:
            print s.name, ': Empty dataset.'

    full[full<5]=np.nan
    full = full[sorted(full.columns)]

    # use only data after this date
    startDate = datetime.datetime(2008,1,1)

    idx = full.index >= startDate
    full = full.ix[idx,:]

    #full.plot(ax=gca())
    print 'Saving vix_futures.csv'
    full.to_csv('vix_futures.csv')

if __name__ == '__main__':

    if not os.path.exists(dataDir):
         print 'creating data directory %s' % dataDir
         os.makedirs(dataDir)

    for year in range(2008,2013):
        for month in range(12):
            print 'Getting data for {0}/{1}'.format(year,month+1)
            saveVixFutureData(year,month,dataDir)

    print 'Raw wata was saved to {0}'.format(dataDir)

    buildDataTable(dataDir)

```

重建 VXX 的代码

*重建 VXX.py*

```
"""
Reconstructing VXX from futures data

author: Jev Kuznetsov

License : BSD
"""
from __future__ import division
from pandas import *
import numpy as np

class Future(object):
    """ vix future class, used to keep data structures simple """
    def __init__(self,series,code=None):
        """ code is optional, example '2010_01' """
        self.series = series.dropna() # price data
        self.settleDate = self.series.index[-1]
        self.dt = len(self.series) # roll period (this is default, should be recalculated)
        self.code = code # string code 'YYYY_MM'

    def monthNr(self):
        """ get month nr from the future code """
        return int(self.code.split('_')[1])

    def dr(self,date):
        """ days remaining before settlement, on a given date """
        return(sum(self.series.index>date))

    def price(self,date):
        """ price on a date """
        return self.series.get_value(date)

def returns(df):
    """ daily return """
    return (df/df.shift(1)-1)

def recounstructVXX():
    """ 
    calculate VXX returns 
    needs a previously preprocessed file vix_futures.csv     
    """
    X = DataFrame.from_csv('vix_futures.csv') # raw data table

    # build end dates list & futures classes
    futures = []
    codes = X.columns
    endDates = []
    for code in codes:
        f = Future(X[code],code=code)
        print code,':', f.settleDate
        endDates.append(f.settleDate)
        futures.append(f)

    endDates = np.array(endDates) 

    # set roll period of each future
    for i in range(1,len(futures)):
        futures[i].dt = futures[i].dr(futures[i-1].settleDate)

    # Y is the result table
    idx = X.index
    Y = DataFrame(index=idx, columns=['first','second','days_left','w1','w2','ret'])

    # W is the weight matrix
    W = DataFrame(data = np.zeros(X.values.shape),index=idx,columns = X.columns)

    # for VXX calculation see http://www.ipathetn.com/static/pdf/vix-prospectus.pdf
    # page PS-20
    for date in idx:
        i =nonzero(endDates>=date)[0][0] # find first not exprired future
        first = futures[i] # first month futures class
        second = futures[i+1] # second month futures class

        dr = first.dr(date) # number of remaining dates in the first futures contract
        dt = first.dt #number of business days in roll period

        W.set_value(date,codes[i],100*dr/dt)
        W.set_value(date,codes[i+1],100*(dt-dr)/dt)

        # this is all just debug info
        Y.set_value(date,'first',first.price(date))
        Y.set_value(date,'second',second.price(date))
        Y.set_value(date,'days_left',first.dr(date))
        Y.set_value(date,'w1',100*dr/dt)
        Y.set_value(date,'w2',100*(dt-dr)/dt)

    valCurr = (X*W.shift(1)).sum(axis=1) # value on day N
    valYest = (X.shift(1)*W.shift(1)).sum(axis=1) # value on day N-1
    Y['ret'] = valCurr/valYest-1    # index return on day N

    return Y

##-------------------Main script---------------------------

Y = recounstructVXX()

print Y.head(30)#
Y.to_csv('reconstructedVXX.csv')

```
