<!--yml

分类：未分类

日期：2024-05-18 08:08:05

-->

# 使用 Python 和 PDFMiner 解析 pdf 文件 | 量化角

> 来源：[`quantcorner.wordpress.com/2014/03/16/parsing-pdf-files-with-python-and-pdfminer/#0001-01-01`](https://quantcorner.wordpress.com/2014/03/16/parsing-pdf-files-with-python-and-pdfminer/#0001-01-01)

这次我需要爱荷华州现金生物柴油价格的时间序列（是的，我确实……）。

爱荷华州每周生物柴油价格可在美国农业部市场营销服务局（AMS/USDA）每周五发布的《国家每周农业能源汇总》报告中找到。[报告](http://www.ams.usda.gov/mnreports/lswagenergy.pdf "National Weekly Ag Energy Round-Up")以**pdf**格式发布，而我们最近使用**html**格式[通过 Python 和 BeautifulSoup](https://quantcorner.wordpress.com/2014/03/05/scraping-data-from-the-internet-with-python-and-beautifulsoup/ "Scraping data from the internet with Python and BeautifulSoup")对其进行了解析。

以下是一个使用[PDFMiner](http://www.unixuser.org/~euske/python/pdfminer/ "PDFMiner")库的**Python**代码片段。它遍历一定数量的 AMS 在线 pdf 文件，提取所需的数据。

不能说它非常健壮，但完成任务还是相当不错的。我们编写了一个基本的错误处理机制，以便在任何情况下程序都能继续运行。实际上，可能会有星期五报告没有发布，例如因为银行假日，美国农业部的一些报告因去年 11 月的美国政府部分关门而缺失……。其他可能的错误类型也会被忽略，并输出 NA。

```
#############################################################
# Edouard TALLENT @ TaGoMa.Tech, March, 2014                #
# Parse a series of online PDF documents to  build          #
# historical time series                                    #
# QuantCorner @ https://quantcorner.wordpress.com            #
#############################################################

# Some sources
# http://www.unixuser.org/~euske/python/pdfminer/programming.html
# http://denis.papathanasiou.org/2010/08/04/extracting-text-images-from-pdf-files/
# http://stackoverflow.com/questions/25665/python-module-for-converting-pdf-to-text

# Required headers
from pdfminer.pdfparser import PDFParser
from pdfminer.pdfdocument import PDFDocument
from pdfminer.pdfpage import PDFPage
from pdfminer.pdfinterp import PDFResourceManager, PDFPageInterpreter
from pdfminer.pdfdevice import PDFDevice
from pdfminer.layout import LAParams
from pdfminer.converter import  TextConverter # , XMLConverter, HTMLConverter
import urllib2
from urllib2 import Request
import datetime
import re

# Define a PDF parser function
def parsePDF(url):

    # Open the url provided as an argument to the function and read the content
    open = urllib2.urlopen(Request(url)).read()

    # Cast to StringIO object
    from StringIO import StringIO
    memory_file = StringIO(open)

    # Create a PDF parser object associated with the StringIO object
    parser = PDFParser(memory_file)

    # Create a PDF document object that stores the document structure
    document = PDFDocument(parser)

    # Define parameters to the PDF device objet 
    rsrcmgr = PDFResourceManager()
    retstr = StringIO()
    laparams = LAParams()
    codec = 'utf-8'

    # Create a PDF device object
    device = TextConverter(rsrcmgr, retstr, codec = codec, laparams = laparams)

    # Create a PDF interpreter object
    interpreter = PDFPageInterpreter(rsrcmgr, device)

    # Process each page contained in the document
    for page in PDFPage.create_pages(document):
        interpreter.process_page(page)
        data =  retstr.getvalue()

    # Get values for Iowa B100 prices 
    reg = '(?<=\n---\n\n)\d.\d{2}-\d.\d{2}'
    matches = re.findall(reg, data)                 # Our data are contained in matches[0]

    # Compute the average
    # Extract value from previous regex 
    low = re.search('\d.\d{2}(?=-)', matches[0])
    high = re.search('(?<=-)\d.\d{2}', matches[0])

    # Cast string variables to float type
    low_val = float(low.group(0))
    high_val = float (high.group(0))

    # Calculate the average
    #import numpy
    #value = [high_val, low_val]
    #print value.mean
    ave = (high_val + low_val) /2

    # Search the date of the report 
    reg = '\w{3},\s\w{3}\s\d{2},\s\d{4}'
    match = re.search(reg, data)        # Result is contained in matches[0]
    dat = match.group(0)

    # Cast to date format
    #import datetime
    #form = datetime.datetime.strptime(match.group(0), '%a, %b %d, %Y')
    #print form

    # http://stackoverflow.com/questions/9752958/how-can-i-return-two-values-from-a-function-in-python
    return (dat, ave)

# The date of the latest weekly price bulletin
start_date = raw_input("Enter the date of the latest weekly price bulletin (dd/mm/yyyy): ")

# Convert start_date string to Python date format
dat = datetime.datetime.strptime(start_date,  '%d/%m/%Y')

# Time series length
back_weeks = raw_input("How many weeks back in time: ")

# A bit of order onto the screen
print '\n'
print 'Date as read in PDF' + '\t' + 'Formatted date' + '\t' + 'Value'

# Loop through the dates
for weeks in xrange(0, int(back_weeks)):

    # Basic exception handling mechamism
    try:           
        wk = datetime.timedelta(weeks = weeks)
        date_back = dat - wk

        # Construct the url
        url = 'http://search.ams.usda.gov/mndms/' + str(date_back.year) + \
              '/' + str(date_back.month).zfill(2) + '/LS' + str(date_back.year) + \
              str(date_back.month).zfill(2) + str(date_back.day).zfill(2) + \
              'WAGENERGY.PDF'

        # Call to function
        fun =  parsePDF(url)

        # Information we are after
        res = str(fun[0]) + '\t' +  str(date_back.day).zfill(2) + '/' + \
              str(date_back.month).zfill(2) +  '/' + str(date_back.year) + \
              '\t' + str(fun[1])

    except Exception:
        print 'NA\t\t\t' +  str(date_back.day).zfill(2) + '/' + \
              str(date_back.month).zfill(2) +  '/' + str(date_back.year) + \
              '\t' + 'NA'

    # Output onto the screen
    print res

'''
Result example:

>>> 

Date as read in PDF Formatted date  Value
Fri, Mar 07, 2014   07/03/2014  3.67
Fri, Feb 28, 2014   28/02/2014  3.57
Fri, Feb 21, 2014   21/02/2014  3.475
Fri, Feb 14, 2014   14/02/2014  3.225
Fri, Feb 07, 2014   07/02/2014  3.175
Fri, Jan 31, 2014   31/01/2014  3.15
Fri, Jan 24, 2014   24/01/2014  3.295
Fri, Jan 17, 2014   17/01/2014  3.24
Fri, Jan 10, 2014   10/01/2014  3.2
Fri, Jan 03, 2014   03/01/2014  3.825
Fri, Dec 27, 2013   27/12/2013  3.845
Fri, Dec 20, 2013   20/12/2013  3.855
Fri, Dec 13, 2013   13/12/2013  3.885
Fri, Dec 06, 2013   06/12/2013  4.025
Fri, Nov 29, 2013   29/11/2013  4.05
Fri, Nov 22, 2013   22/11/2013  4.025
Fri, Nov 15, 2013   15/11/2013  4.075
Fri, Nov 08, 2013   08/11/2013  4.325
Fri, Nov 01, 2013   01/11/2013  4.365
Fri, Oct 25, 2013   25/10/2013  4.54

'''
```
