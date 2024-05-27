```

分类：未分类

日期：2024-05-18 08:07:52

```

# 马来西亚棕榈油生产数据。使用 Python 和 BeautifulSoup 获取的另一项吸引人的数据 | 量化角

> 来源：[`quantcorner.wordpress.com/2014/04/13/mpobs-malaysian-crude-palm-oil-production-data-another-fetching-thing-with-python-and-beautifulsoup/#0001-01-01`](https://quantcorner.wordpress.com/2014/04/13/mpobs-malaysian-crude-palm-oil-production-data-another-fetching-thing-with-python-and-beautifulsoup/#0001-01-01)

我们需要最新的马来西亚棕榈油生产数据。MPOB 在其网站上提供此类数据。我们只需编写一些**Python**代码（相当丑陋但有点可靠），后者的功能仅用几行代码即可实现。我们使用了**BeautifulSoup**这个额外的库，我们之前在这里[](https://quantcorner.wordpress.com/2014/03/05/scraping-data-from-the-internet-with-python-and-beautifulsoup/ "Parsing pdf files with Python and PDFMiner")和这里[](https://quantcorner.wordpress.com/2014/03/05/scraping-data-from-the-internet-with-python-and-beautifulsoup/ "Scraping data from the internet with Python and BeautifulSoup")已经使用过。

需要额外一年数据（即 2005 年）的人可以很容易地修改原始代码以从 MPOB 网站获取它们。

数据输出到屏幕上，以便它们可以轻松地复制并粘贴到**微软 Excel**中（格式类似于*.csv*）。

```
#####################################################
# Edouard TALLENT @TaGoMa.Tech                      #
# Scraping MPOB's data on CPO                       #
# Website http://bepi.mpob.gov.my/                  #
# QuantCorner @ https://quantcorner.wordpress.com    #
# April, 2014                                       #
#####################################################

# Required headers
import urllib2                          # Read webpages
from bs4 import BeautifulSoup           # bs4 fonctions
import re                               # Regex, removing those bloody kommas

# Arrays that will contain the desired data
months = ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul',  'Aug', 'Sep', 'Oct', 'Nov', 'Dec']
data = []
dates = []

# URLs
oldest = 2006 # Data are available back to 2006
newest = 2014 # Most recent year for the data

for urls in range (oldest, newest + 1):
    # construct the URLs strings
    url = 'http://bepi.mpob.gov.my/stat/web_report1.php?val=' + str(urls) + '44'

    # Read the HTML page content
    page = urllib2.urlopen(url)

    # Create a beautifulsoup object
    soup = BeautifulSoup(page)

    # Search the table to be parsed in the whole HTML code
    tables = soup.findAll('table')

    for y in range (2, 16):
        m = 0
        for table in range(0, 2):
            for x in range(2, 13, 2):
                data.append(re.sub(',','', tables[table].findAll('tr')[y].findAll('td')[x].string))

# Construct the date series (%b-%Y format)
for year in range(oldest, newest + 1):
    for month in months:
        dates.append(str(month) + '-' + str(year)) # Construct the %b-%Y series

# Rearrange the data
ind = 0
cnt = 0
arr = [[],[],[],[],[],[],[],[],[],[],[],[],[],[]]

for dat in range(0, len(data)):
    arr[ind].append(data[dat])
    cnt += 1
    if (dat + 1)%12 == 0: 
        ind += 1
    if ind > 13:
        ind = 0

# Print out to screen
print 'date,johor,kedah,kelantan,negeri_sembilan,pahang,perak,selangor,terennganu,\
other_states,p_malaysia,sabah,sarawak,sabah_sarawak,malaysia'
for x in range (0, len(arr[0])):
    print str(dates[x]) + ',' + arr[0][x] + ',' + arr[1][x] + ',' + arr[2][x] + ',' + arr[3][x] + ',' + \
    arr[4][x] + ',' + arr[5][x] + ',' + arr[6][x] + ',' + arr[7][x] + ',' + arr[8][x] + ',' + \
    arr[9][x] + ',' + arr[10][x] + ',' + arr[11][x] + ',' + arr[12][x] + ',' + arr[13][x]

'''
# Output
date,johor,kedah,kelantan,negeri_sembilan,pahang,perak,selangor,terennganu,other_states,p_malaysia,sabah,sarawak,sabah_sarawak,malaysia
Jan-2006,145637,10794,12146,22321,108659,100251,34323,21896,8353,464380,376082,96131,472213,936593
Feb-2006,193908,16102,14455,33604,137622,130834,43014,23719,12684,605942,346248,99714,445962,1051904
...
...
Oct-2014, , , , , , , , , , , , , , 
Nov-2014, , , , , , , , , , , , , , 
Dec-2014, , , , , , , , , , , , , , 
'''

```
