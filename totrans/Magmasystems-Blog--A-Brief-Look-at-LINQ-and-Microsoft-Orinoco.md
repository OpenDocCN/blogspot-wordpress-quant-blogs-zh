<!--yml
category: 未分类
date: 2024-05-18 04:53:22
-->

# Magmasystems Blog: A Brief Look at LINQ and Microsoft Orinoco

> 来源：[http://magmasystems.blogspot.com/2009/05/brief-look-at-linq-and-microsoft.html#0001-01-01](http://magmasystems.blogspot.com/2009/05/brief-look-at-linq-and-microsoft.html#0001-01-01)

This was taken from the Microsoft whitepaper on Orinoco. Thanks for the Orinoco team for providing this to me.

Let's assume that you have a number of power meters that you need to monitor. The "InputStream" contains a stream of tuples where each tuple contains a power reading from an individual meter. The reading happens to come in as the wattage times 10.

We can capture each reading a project a new stream that has the normalized wattage. We can also create a sliding 3-second window of meter readings that we can do calculations against.

var realValueStream =

from e in InputStream

select new MeterWattage((double)e.Consumption / 10);

var windowedStream =

from e in realValueStream.SlidingWindow(TimeSpan.FromSeconds(3))

select new MeterWattage(e.wattage);

We can then create a stream that has the average power reading over a sliding 3 second period.

var averagedStream =

from e in windowedStream

select new OneMeterAverage(CEPAggregates.Average(e.wattage));

(I think that this next query may be incorrect, as the ID field was not captured in the windowedStream, but I will continue with the example anyway).

If you want to get the 3-second sliding average for each individual meter, you can do the following 2 queries:

var meterStreamGroups =

from e in windowedStream

group e by e.id;

var groupedAveragedStream =

from eb in meterStreamGroups

from e in eb

select new MeterAverage(eb.Key, CEPAggregates.Avg(e.wattage));

Now, we want to compute the ratio of consumption for each meter over the 3-second window. 

var sumStream =

from e in groupedAveragedStream

select new MeterSum(CEPAggregates.Sum(e.wattage));

var ratioStream =

from e1 in groupedAveragedStream

join e2 in sumStream on true equals true

select new 

MeterRatio(e1.Id, e1.Wattage, e1.Wattage / e2.TotalWattage);

Finally, we just want to capture the ratio of power consumption from meter #2. 

var filteredStream =

from e in ratioStream

where e.id == 2

select e;

©2009 Marc Adler - All Rights Reserved.

All opinions here are personal, and have no relation to my employer.