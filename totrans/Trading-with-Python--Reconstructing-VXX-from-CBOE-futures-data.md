<!--yml
category: 未分类
date: 2024-05-18 15:42:59
-->

# Trading with Python: Reconstructing VXX from CBOE futures data

> 来源：[http://tradingwithpython.blogspot.com/2012/01/reconstructing-vxx-from-cboe-futures.html#0001-01-01](http://tradingwithpython.blogspot.com/2012/01/reconstructing-vxx-from-cboe-futures.html#0001-01-01)

Many people in the blogsphere have reconstructed the VXX to see how it should perform before its inception. The procedure to do this is not very complicated and well-described in the VXX prospectus and on the 

[Intelligent Investor Blog](http://investing.kuchita.com/2011/08/16/how-the-vxx-is-calculated-and-why-backwardation-amplfies-it/)

. Doing this by hand however is a very tedious work, requiring to download data for each future separately, combine them in a spreadsheet etc.

The scripts below automate this process. The first one,

*downloadVixFutures.py*

 , gets the data from cboe, saves each file in a data directory and then combines them in a single csv file,

*vix_futures.csv*

The second script

*reconstructVXX.py*

 parses the

*vix_futures.csv,*

calculates the daily returns of VXX  and saves results to

*reconstructedVXX.csv*

.

To check the calculations, I've compared my simulated results with the SPVXSTR index data, the two agree pretty well, see the charts below.

**Note: For a fee, I can provide support to get the code running or create a stand-alone program, contact me if you are interested.**

--------------------------------source codes--------------------------------------------

Code for getting futures data from CBOE and combining it into a single table

*downloadVixFutures.py*

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

Code for reconstructing the VXX

*reconstructVXX.py*

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