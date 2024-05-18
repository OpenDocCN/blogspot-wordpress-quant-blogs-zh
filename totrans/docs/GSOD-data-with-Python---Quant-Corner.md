<!--yml
category: 未分类
date: 2024-05-18 08:07:02
-->

# GSOD data with Python | Quant Corner

> 来源：[https://quantcorner.wordpress.com/2016/10/02/gsod-data-with-python/#0001-01-01](https://quantcorner.wordpress.com/2016/10/02/gsod-data-with-python/#0001-01-01)

This one-file project fetches  [Global Surface Summary of the Day (GSOD)](https://data.noaa.gov/dataset/global-surface-summary-of-the-day-gsod) from the **National Oceanic and Atmospheric Administration** (**NOAA**)’s HTTP server (data are also available on their FTP).

See the code on [github](https://github.com/tagomatech/ETL/tree/master/gsod).

## station_search()

Whether a given weather station is part of the **GSOD** project can be checked using the **station_search()** function. For instance, the station Stanton (UK) can be retrieved as follows:

```
gsod = GSOD()
stanton = gsod.station_search({'station_name' : 'STANTON'})

```

This function also allows to retrieve all weather stations in a given country or US State, e.g. all stations in Iowa can be listed as folllows:

```
iowa = gsod.station_search({'state' : 'IA'})
```

## get_data()

Basic usage requires only requires (what I call) weather ***station id*** which actually combines **USAF** (6-digit) and **WBAN** (5-digit) identification numbers linked by a dash sign. For instance, **699604-03145** is  the ***station id*** for **YUMA MCAS** (US) weather station. Getting **YUMA MCAS** weather data for the current year is as simple as:

```
yuma = GSOD('699604-03145').get_data()

```

The object returned is a **pandas.DataFrame()**.

User can also be willing to download **YUMA MCAS** weather data for several consecutive years, with a single call to the function*:

```
yuma_13_15 = GSOD(station='699604-03145', start=2013, end=2015).get_data()

```

Original data are reported in **Fahrenheit**, **miles**, **knots**, and **inches**. It is possible to convert them to **Celsius**, **km**, **kph**, and **cm**, respectively. To do so, one passes an extra argument *unit* with a string as value if only one conversion is desired or a list of strings instead if 2+ unit conversions are required, e.g.:

```
yuma_converted = GSOD(station='699604-03145', units=['celsius', 'km', 'kph', 'cm']).get_data()

```

##### * Still, behind the scene, NOAA servers are called once for each single year of required data