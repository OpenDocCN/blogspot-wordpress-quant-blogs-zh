<!--yml

category: 未分类

date: 2024-05-18 08:07:24

-->

# 使用 Python 下载 EIA 的数据 | 量化角落

> 来源：[`quantcorner.wordpress.com/2014/11/18/downloading-eias-data-with-python/#0001-01-01`](https://quantcorner.wordpress.com/2014/11/18/downloading-eias-data-with-python/#0001-01-01)

下面是一个片段，用于下载**美国能源信息署（US EIA）**网站上提供的众多数据集（www.eia.gov）。

用户需要提供的输入是一个**EIA**令牌和要下载的系列的代码。输出是一个**pandas**数据框。返回的日期是字符串。无论如何，将它们解析为**Python**日期对象都很容易。

```
import json
import numpy as np
import pandas as pd
from urllib.error import URLError, HTTPError
from urllib.request import urlopen

class EIAgov(object):
    def __init__(self, token, series):
        '''
        Purpose:
        Initialise the EIAgov class by requesting:
        - EIA token
        - id code(s) of the series to be downloaded

        Parameters:
        - token: string
        - series: string or list of strings
        '''
        self.token = token
        self.series = series

    '''
    def __repr__(self):
        return str(self.series)
    '''

    def Raw(self, ser):
        # Construct url
        url = 'http://api.eia.gov/series/?api_key=' + self.token + '&series_id=' + ser.upper()

        try:
            # URL request, URL opener, read content
            response = urlopen(url);
            raw_byte = response.read()
            raw_string = str(raw_byte, 'utf-8-sig')
            jso = json.loads(raw_string)
            return jso

        except HTTPError as e:
            print('HTTP error type.')
            print('Error code: ', e.code)

        except URLError as e:
            print('URL type error.')
            print('Reason: ', e.reason)

    def GetData(self):
        # Deal with the date series 
        date_ = self.Raw(self.series[0])        
        date_series = date_['series'][0]['data']
        endi = len(date_series) # or len(date_['series'][0]['data'])
        date = []
        for i in range (endi):
            date.append(date_series[i][0])

        # Create dataframe
        df = pd.DataFrame(data=date)
        df.columns = ['Date']

        # Deal with data
        lenj = len(self.series)
        for j in range (lenj):
            data_ = self.Raw(self.series[j])
            data_series = data_['series'][0]['data']
            data = []
            endk = len(date_series)         
            for k in range (endk):
                data.append(data_series[k][1])
            df[self.series[j]] = data

        return df

if __name__ == '__main__':
    tok = 'YOUR_EIA_TOKEN'

    # Natural Gas - Daily prices
    # http://www.eia.gov/beta/api/qb.cfm?category=462457&sdid=NG.RNGC1.D
    ng = ['NG.RNGC1.D']  # w/ several series at a time ['ELEC.REV.AL-ALL.M', 'ELEC.REV.AK-ALL.M', 'ELEC.REV.CA-ALL.M']
    data = EIAgov(tok, ng)
    print(data.GetData())

'''
              Date  NG.RNGC1.D
0     20150714       2.840
1     20150710       2.770
2     20150709       2.726
3     20150708       2.685
4     20150707       2.716
5     20150706       2.756
6     20150702       2.822
7     20150701       2.783
8     20150630       2.832
9     20150629       2.805
10    20150626       2.773
11    20150625       2.850
12    20150624       2.759
13    20150623       2.726
14    20150622       2.733
15    20150619       2.816
16    20150618       2.777
17    20150617       2.855
18    20150616       2.894
19    20150615       2.889
20    20150612       2.750
21    20150611       2.825
22    20150610       2.891
23    20150609       2.846
24    20150608       2.705
25    20150605       2.590
26    20150604       2.626
27    20150603       2.634
28    20150602       2.698
29    20150601       2.649
...        ...         ...
5359  19940224       2.248
5360  19940223       2.232
5361  19940222       2.296
5362  19940218       2.418
5363  19940217       2.385
5364  19940216       2.345
5365  19940215       2.253
5366  19940214       2.252
5367  19940211       2.356
5368  19940210       2.374
5369  19940209       2.358
5370  19940208       2.411
5371  19940207       2.347
5372  19940204       2.369
5373  19940203       2.383
5374  19940202       2.585
5375  19940201       2.639
5376  19940131       2.554
5377  19940128       2.528
5378  19940127       2.417
5379  19940126       2.359
5380  19940125       2.246
5381  19940124       2.470
5382  19940121       2.305
5383  19940120       2.250
5384  19940119       2.252
5385  19940118       2.318
5386  19940117       2.360
5387  19940114       2.268
5388  19940113       2.194

[5389 rows x 2 columns]
Press any key to continue . . .
'''

```

这篇文章发表在[计算机编程](https://quantcorner.wordpress.com/category/computer-programming/)、[原油](https://quantcorner.wordpress.com/category/crude-oil/)、[数据](https://quantcorner.wordpress.com/tag/data/)、[DoE](https://quantcorner.wordpress.com/category/doe/)、[EIA](https://quantcorner.wordpress.com/category/eia/)、[能源](https://quantcorner.wordpress.com/category/energy/)、[互联网](https://quantcorner.wordpress.com/tag/internet/)、[pandas](https://quantcorner.wordpress.com/tag/pandas/)、[产品](https://quantcorner.wordpress.com/category/products/)、[Python](https://quantcorner.wordpress.com/tag/python/)分类，并且用[data](https://quantcorner.wordpress.com/tag/data/)、[互联网](https://quantcorner.wordpress.com/tag/internet/)、[pandas](https://quantcorner.wordpress.com/tag/pandas/)、[Python](https://quantcorner.wordpress.com/tag/python/)标记于[2014 年 11 月 18 日](https://quantcorner.wordpress.com/2014/11/18/downloading-eias-data-with-python/ "10:32 PM")由[édouard](https://quantcorner.wordpress.com/author/tallente/ "查看édouard 的所有文章")发布。
