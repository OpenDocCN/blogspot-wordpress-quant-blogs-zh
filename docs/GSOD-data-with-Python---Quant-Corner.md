<!--yml

类别：未分类

日期：2024 年 05 月 18 日 08:07:02

-->

# 使用 Python 获取 GSOD 数据 | 数量角

> 来源：[`quantcorner.wordpress.com/2016/10/02/gsod-data-with-python/#0001-01-01`](https://quantcorner.wordpress.com/2016/10/02/gsod-data-with-python/#0001-01-01)

这个单文件项目从**国家海洋和大气管理局**（**NOAA**）的 HTTP 服务器上获取了[全球每日地面摘要（GSOD）](https://data.noaa.gov/dataset/global-surface-summary-of-the-day-gsod) 数据（数据也可以在他们的 FTP 上找到）。

查看 [github](https://github.com/tagomatech/ETL/tree/master/gsod) 上的代码。

## station_search()

一个给定的气象台是否参与了**GSOD** 项目，可以使用**station_search()** 函数进行检查。例如，可以按照以下方式检索英国斯坦顿（UK）的气象台：

```
gsod = GSOD()
stanton = gsod.station_search({'station_name' : 'STANTON'})

```

这个函数还允许检索给定国家或美国州的所有气象台，例如，可以列出爱荷华州所有的气象台如下：

```
iowa = gsod.station_search({'state' : 'IA'})
```

## get_data()

基本用法只需要（我称之为）**气象台 id**，它实际上是由**USAF**（6 位数字）和**WBAN**（5 位数字）识别号组合而成，通过破折号连接。例如，**699604-03145** 是美国**YUMA MCAS** 气象台的**气象台 id**。获取**YUMA MCAS** 当年的气象数据就像这样简单：

```
yuma = GSOD('699604-03145').get_data()

```

返回的对象是一个**pandas.DataFrame()** 。

用户也可能想要通过单次调用函数下载多年的**YUMA MCAS** 的气象数据：

```
yuma_13_15 = GSOD(station='699604-03145', start=2013, end=2015).get_data()

```

原始数据是**华氏度**、**英里**、**结**和**英寸**报告的。可以将它们分别转换为**摄氏度**、**千米**、**公里每小时**和**厘米**。为此，如果只需要一个转换，可以传入一个额外的参数*unit*，用字符串作为值；如果需要 2 个或更多单位的转换，则传入一个字符串列表，例如：

```
yuma_converted = GSOD(station='699604-03145', units=['celsius', 'km', 'kph', 'cm']).get_data()

```

##### * 然而，在幕后，NOAA 服务器将会针对每个所需数据的单年调用一次
