<!--yml

category: 未分类

date: 2024-05-18 15:42:51

-->

# 用 Python 进行交易：从短期成交量数据构建指标

> 来源：[`tradingwithpython.blogspot.com/2013/08/building-indicator-from-short-volume.html#0001-01-01`](http://tradingwithpython.blogspot.com/2013/08/building-indicator-from-short-volume.html#0001-01-01)

资产或 ETF 的价格当然是最好的指标，但不幸的是，它所包含的信息有限。有些人似乎认为指标越多（rsi、macd、移动平均线交叉等），越好，但如果它们都基于相同的基础价格序列，它们将都包含在价格中包含的有限信息的子集中。

我们需要更多信息

*额外的*

从所包含的价格中获取更多信息，以便对将来发生的事情作出更明智的猜测。结合各种信息进行聪明分析的绝佳例子可以在

[长期博客的短面](http://theshortsideoflong.blogspot.nl/)

。进行这种分析需要大量工作，我只是个兼职交易员，没有足够的时间。

所以我建立了自己的“市场仪表板”，它会自动为我收集信息并以易于理解的形式呈现出来。在这篇文章中，我将展示如何基于短期成交量数据构建指标。本文将说明数据收集和处理的过程。

**步骤 1: 查找数据源。 **

BATS 交易所免费提供每日成交量数据

[站点](http://www.batstrading.com/market_data/shortsales/)

。

**步骤 2: 手动获取数据并检查**

BATS 交易所的短期成交量数据包含在一个文本文件中，该文本文件被压缩。每天都有自己的 zip 文件。下载并解压缩 txt 文件后，其中包含以下内容（前几行）：

```
Date|Symbol|Short Volume|Total Volume|Market Center
20111230|A|26209|71422|Z
20111230|AA|298405|487461|Z
20111230|AACC|300|3120|Z
20111230|AAN|3600|10100|Z
20111230|AAON|1875|6156|Z

```

....

总共一个文件包含大约 6000 个符号。

这些数据需要进行相当多的处理，才能以有意义的方式呈现出来。

**步骤 3: 自动获取数据**

我真正想要的不仅仅是一天的数据，而是过去几年的短期成交量与总成交量的比率，而且我不太想手动下载 500 多个 zip 文件并将它们粘贴到 Excel 中。 

幸运的是，完全自动化只需要几行代码：

首先，我们需要动态创建一个 url，从中将下载一个文件：

```
from string import Template

def createUrl(date):
    s = Template('http://www.batstrading.com/market_data/shortsales/$year/$month/$fName-dl?mkt=bzx')
    fName = 'BATSshvol%s.txt.zip' % date.strftime('%Y%m%d')

    url = s.substitute(fName=fName, year=date.year, month='%02d' % date.month)

    return url,fName

```

输出：

```
http://www.batstrading.com/market_data/shortsales/2013/08/BATSshvol20130813.txt.zip-dl?mkt=bzx

```

现在我们可以一次下载多个文件：

```
import urllib

for i,date in enumerate(dates):
    source, fName =  createUrl(date)# create url and file name
    dest = os.path.join(dataDir,fName) 
    if not os.path.exists(dest): # don't download files that are present
        print 'Downloading [%i/%i]' %(i,len(dates)), source
        urllib.urlretrieve(source, dest)
    else:
        print 'x',

```

输出：

```
Downloading [0/657] http://www.batstrading.com/market_data/shortsales/2011/01/BATSshvol20110103.txt.zip-dl?mkt=bzx
Downloading [1/657] http://www.batstrading.com/market_data/shortsales/2011/01/BATSshvol20110104.txt.zip-dl?mkt=bzx
Downloading [2/657] http://www.batstrading.com/market_data/shortsales/2011/01/BATSshvol20110105.txt.zip-dl?mkt=bzx
Downloading [3/657] http://www.batstrading.com/market_data/shortsales/2011/01/BATSshvol20110106.txt.zip-dl?mkt=bzx

```

**步骤 4\. 解析下载的文件**

我们可以使用 zip 和 pandas 库解析单个文件：

```
import datetime as dt
import zipfile
import StringIO

def readZip(fName):
    zipped = zipfile.ZipFile(fName) # open zip file 
    lines = zipped.read(zipped.namelist()[0]) # unzip and read first file 
    buf = StringIO.StringIO(lines) # create buffer
    df = pd.read_csv(buf,sep='|',index_col=1,parse_dates=False,dtype={'Date':object,'Short Volume':np.float32,'Total Volume':np.float32}) # parse to table
    s = df['Short Volume']/df['Total Volume'] # calculate ratio
    s.name = dt.datetime.strptime(df['Date'][-1],'%Y%m%d')

    return s

```

它返回一个 Short Volume/Total Volume 的比率，适用于 zip 文件中的所有符号：

```
Symbol
A         0.531976
AA        0.682770
AAIT      0.000000
AAME      0.000000
AAN       0.506451
AAON      0.633841
AAP       0.413083
AAPL      0.642275
AAT       0.263158
AAU       0.494845
AAV       0.407976
AAWW      0.259511
AAXJ      0.334937
AB        0.857143
ABAX      0.812500
...
ZLC       0.192725
ZLCS      0.018182
ZLTQ      0.540341
ZMH       0.413315
ZN        0.266667
ZNGA      0.636890
ZNH       0.125000
ZOLT      0.472636
ZOOM      0.000000
ZQK       0.583743
ZROZ      0.024390
ZSL       0.482461
ZTR       0.584526
ZTS       0.300384
ZUMZ      0.385345
Name: 2013-08-13 00:00:00, Length: 5859, dtype: float32

```

```

```

```
Step 5: Make a chart:

Now the only thing left is to parse all downloaded files and combine them to a single table and plot the result:

 In the figure above I have plotted the 

*average*

 short volume ratio for the past two years. I also could have used a subset of symbols if I wanted to take a look at a specific sector or stock. Quick look at the data gives me an impression that high short volume ratios usually correspond with market bottoms and low ratios seem to be good entry points for a long position.

Starting from here, this short volume ratio can be used as a basis for strategy development. 
```

```

```
