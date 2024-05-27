<!--yml

category: 未分类

日期：2024 年 5 月 18 日 08:07:15

-->

# 使用 Python 从 NASDAQ 网站获取期权数据 | 量化投资角

> 来源：[`quantcorner.wordpress.com/2015/11/02/fetching-nasdaq-options-data-with-python/#0001-01-01`](https://quantcorner.wordpress.com/2015/11/02/fetching-nasdaq-options-data-with-python/#0001-01-01)

下面是一段**Python**代码，可以从[NASDAQ](http://www.nasdaq.com/)网站下载期权链。它基本上是一个大函数，严重依赖于**BeautifulSoup**，并封装成一个类（‘c’est chic’）。用户提供股票代码、到期日和其他一些参数。然后会得到一个包含期权数据的**pandas.DataFrame**对象。

请注意，我编写这段代码是为了一些家庭研究项目。如果您要使用它并实际从[NASDAQ](http://www.nasdaq.com/)网站下载数据，请确保它符合其[使用条款](http://www.nasdaq.com/about/terms.aspx)中规定的“合理使用”条件。无论以何种方式，我都不会直接或间接地对任何事情负责或承担责任。

```
'''
Copyright (C) 2015, Edouard 'tagoma' Tallent
Class fetching options data from www.nasdaq.com 
Nasdaq_option_quotes.py v0.2 (Nov15)
QuantCorner @ https://quantcorner.wordpress.com
'''
from bs4 import BeautifulSoup
import requests
import re
import numpy as np
import pandas as pd

class NasdaqOptions(object):
    '''
    Class NasdaqOptions fetches options data from Nasdaq website

    User inputs:
        Ticker: ticker
            - Ticker for the underlying
        Expiry: nearby
            - 1st Nearby: 1
            - 2nd Nearby: 2
            - etc ...
        Moneyness: money
            - All moneyness: all
            - In-the-money: in
            - Out-of-the-money: out
            - Near the money: near
        Market: market
            - Composite quote: Composite
            - Chicago Board Options Exchange: CBO
            - American Options Exchange: AOE
            - New York Options Exchange: NYO
            - Philadelphia Options Exchange: PHO
            - Montreal Options Exchange: MOE
            - Boston Options Exchange: BOX
            -  International Securities Exchange: ISE
            - Bats Exchange Options Market: BTO
            - NASDAQ Options: NSO
            - C2(Chicago) Options Exchange: C2O
            - NASDAQ OMX BX Options Exchange: BXO
            - MIAX: MIAX
        Option category: expi
            - Weekly options: week
            - Monthly options: stand
            - Quarterly options: quart
            - CEBO options (Credit Event Binary Options): cebo   
    '''
    def __init__(self, ticker, nearby, money='near', market='cbo', expi='stan'):
        self.ticker = ticker
        self.nearby = nearby-1  # ' refers 1st nearby on NASDAQ website
        #self.type = type   # Deprecated
        self.market = market
        self.expi = expi
        if money == 'near':
            self.money = ''
        else:
            self.money =  '&money=' + money 

    def get_options_table(self):
        '''
        - Loop over as many webpages as required to get the complete option table for the
        option desired
        - Return a pandas.DataFrame() object 
        '''
        # Create an empty pandas.Dataframe object. New data will be appended to
        old_df = pd.DataFrame()

        # Variables
        loop = 0        # Loop over webpages starts at 0
        page_nb = 1     # Get the top of the options table
        flag = 1        # Set a flag that will be used to call get_pager()
        old_rows_nb = 0 # Number of rows so far in the table

        # Loop over webpages
        while loop < int(page_nb):
            # Construct the URL
            '''url = 'http://www.nasdaq.com/symbol/' + self.ticker + '/option-chain?dateindex='\
               + str(self.nearby) + '&callput=' + self.type + '&money=all&expi='\
               + self.expi + '&excode=' + self.market + '&page=' + str(loop+1)'''
            url = 'http://www.nasdaq.com/symbol/' + self.ticker + '/option-chain?excode=' + self.market + self.money + '&expir=' + self.expi + '&dateindex=' + str(self.nearby) + '&page=' + str(loop+1)

            # Query NASDAQ website
            try:
                response = requests.get(url)#, timeout=0.1)
            # DNS lookup failure
            except requests.exceptions.ConnectionError as e:
                print('''Webpage doesn't seem to exist!\n%s''' % e)
                pass
            # Timeout failure
            except requests.exceptions.ConnectTimeout as e:
                print('''Slow connection!\n%s''' % e)
                pass
            # HTTP error
            except requests.exceptions.HTTPError as e:
                print('''HTTP error!\n%s''' % e)
                pass

            # Get webpage content
            soup = BeautifulSoup(response.content, 'html.parser')

            # Determine actual number of pages to loop over
            if flag == 1:   # It is run only once
                # Get the number of page the option table lies on
                last_page_raw = soup.find('a', {'id': 'quotes_content_left_lb_LastPage'})
                last_page = re.findall(pattern='(?:page=)(\d+)', string=str(last_page_raw))
                page_nb = ''.join(last_page)
                flag = 0

            # Extract table containing the option data from the webpage
            table = soup.find_all('table')[4] # table #4 in the webpage is the one of interest

            # Extract option data from table as a list
            elems = table.find_all('td') # Python object
            lst = [elem.text for elem in elems] # Option data as a readable list

            # Rearrange data and create a pandas.DataFrame
            arr = np.array(lst)
            reshaped = arr.reshape((len(lst)/16, 16))
            new_df = pd.DataFrame(reshaped)
            frames = [old_df, new_df]
            old_df = pd.concat(frames)
            rows_nb = old_df.shape[0]

            # Increment loop counter
            if rows_nb > old_rows_nb:
                loop+=1
                old_rows_nb = rows_nb
            elif rows_nb == old_rows_nb:
                print('Problem while catching data.\n## You must try again. ##')
                pass
            else:   # Case where rows have been deleted
                    # which shall never occur
                print('Failure!\n## You must try again. ##')
                pass

        # Name the column 'Strike'
        old_df.rename(columns={old_df.columns[8]:'Strike'}, inplace=True)

        ## Split into 2 dataframes (1 for calls and 1 for puts)
        calls = old_df.ix[:,1:7]
        puts = old_df.ix[:,10:16] # Slicing is not incluse of the last column

        # Set 'Strike' column as dataframe index
        calls = calls.set_index(old_df['Strike'])
        puts = puts.set_index(old_df['Strike'])

        ## Headers names
        headers = ['Last', 'Chg', 'Bid', 'Ask', 'Vol', 'OI']
        calls.columns = headers
        puts.columns = headers

        return calls, puts

if __name__ == '__main__':
    # Get data for Dec-15 SPX options, Dec-15 being the 2nd nearby options = NasdaqOptions('SPX',2)
    calls, puts = options.get_options_table()

    # Write on the screen
    print('\n######\nCalls:\n######\n', calls,\
        '\n\n######\nPuts:\n######\n', puts)

'''
######
Calls:
######
           Last    Chg Bid Ask    Vol      OI
Strike                                      
1900    179.40                     0   38292
1905    103.75                     0    9693
1910    191.30                     0    8378
1915    186.45  -1.97              0    3671
1920    173.95                     0    7218
1925    181.51   6.38              1   23678
1930    170.90   5.30             10   15743
1935    160.37                     0   17814
1940    152.30                     0   10564
1945     88.82                     0   10687
1950    149.73                     0   66844
1955    124.81                     0   11206
1960    120.60                     0   10682
1965    123.60                     0   10737
1970    143.00   5.50            789   15184
1975    136.48   3.70              1   25654
1980    129.15   0.01             41   12569
1985    127.90  12.45              3   15602
1990     98.86                     0    7900
1995     98.25                     0   10133
2000    114.40   1.30             31  116981
2005    103.20   3.90              3   15097
2010     98.45  -4.07              2    8119
2015     94.33  12.83              2    7058
2020     86.40                     0   17249
2025     90.50  -1.35             20   59959
2030     89.65   3.35             99    3303
2035     80.45   1.55              1    2979
2040     77.10  -1.55             13    5517
2045     74.25   0.15             15    3768
...        ...    ...  ..  ..    ...     ...
2115     28.75   1.45            136    6475
2120     26.12   1.42             64    5201
2125     23.90   1.40            154   28130
2130     21.27   1.67          10077    1647
2135     19.65   2.25             82   13484
2140     17.50   1.54            218    5150
2145     14.80   1.10             85    3644
2150     13.01   1.16           2073   55095
2155     11.23   0.98             71    1543
2160      9.90   1.05             70   10684
2165      8.60   1.05             14    1124
2170      7.23   0.52             28    2911
2175      6.30   0.77            166   22039
2180      5.30   0.70             74    5608
2185      4.55   0.65              8     524
2190      3.80   0.50             47    2154
2195      3.10   0.30             25    3563
2200      3.00   0.70           1815   63117
2205      2.15   0.13             32     429
2210      2.05   0.40             33   12771
2215      1.35                     0     129
2220      1.50   0.40              5    2807
2225      1.10   0.09             61   18367
2230      0.90   0.05             25     187
2235      1.10   0.41              7      81
2240      0.70                     0     444
2245      0.60                     0    1060
2250      0.70   0.10           4058   42602
2275      0.35                     0   37307
2300      0.30   0.05           9004   91173

[73 rows x 6 columns] 

######
Puts:
######
           Last      Chg Bid Ask   Vol      OI
Strike                                       
1900      5.80    -0.16          3135  115697
1905      5.95    -0.90             1    9772
1910      5.70    -0.75             1    8667
1915      6.90     0.41            13    4304
1920      6.70    -0.20          1146    9707
1925      7.02    -1.18           271   50314
1930      7.40     0.10            61   21183
1935      7.85                      0   16832
1940      8.25    -0.05            19   12021
1945      8.35    -0.05             4   20285
1950      9.05     0.17          5308  115872
1955      9.28     0.06             8   11626
1960      9.55    -0.08          5051   16218
1965     10.13     0.11             9   11052
1970     10.50    -0.10           115   16865
1975     10.80    -0.33           218   35755
1980     11.35    -0.35            13   15200
1985     12.05    -1.81             3   16854
1990     12.80     0.01            67    8195
1995     13.59     0.19            14   10430
2000     14.00    -1.00          5473  142800
2005     14.13    -0.63            20   16162
2010     14.96    -0.76             4   11485
2015     16.46    -0.32             1    7123
2020     16.55    -0.75           144   21422
2025     17.84    -0.06            88   47092
2030     18.17    -0.88           166    7872
2035     21.55                     16    2749
2040     20.02    -0.62           106    5465
2045     21.33    -0.32            20    4603
...        ...      ...  ..  ..   ...     ...
2115     51.10                      0      10
2120     47.10    -0.40             6     147
2125     48.40    -1.15            19    5128
2130     50.00   -14.01           132      37
2135     54.50                      0       1
2140     57.84                      0      44
2145     64.35    -0.60            10      15
2150     63.16     0.51             5    9430
2155                                0        
2160     68.02  -142.03            40       1
2165                                0        
2170     79.50   -14.30             4       2
2175     98.90                      0     153
2180                                0        
2185                                0        
2190                                0        
2195    112.28                      0       8
2200    101.90    -5.30             1    5498
2205                                0        
2210                                0        
2215    208.50                      0       5
2220    245.20                      0       1
2225    247.66                      0      84
2230    209.50                      0      42
2235                                0        
2240    253.95                      0       4
2245                                0        
2250    182.85                      0     354
2275    205.80                      0     796
2300    230.70                      0    2562

[73 rows x 6 columns]
'''
```

**版本历史**

v0.1 (Nov 02, 15)：首次发布

v0.2 (Nov 03, 15)：现在返回唯一的看涨期权和看跌期权 DataFrame；用户现在可以在 4 个期权价格水平（所有、实值、虚值、平值）中选择
