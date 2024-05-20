<!--yml
category: 未分类
date: 2024-05-18 05:06:29
-->

# Magmasystems Blog: More on the first CEP Use Case

> 来源：[http://magmasystems.blogspot.com/2007/11/more-on-first-cep-use-case.html#0001-01-01](http://magmasystems.blogspot.com/2007/11/more-on-first-cep-use-case.html#0001-01-01)

Yesterday, I had a great two-hour session with Henry and Bob from Coral8 in which most of the use case was done.

Henry is our designated pre-sales engineer. His job is to do what it takes to make sure that the prospective customer is happy with the product before making a decision to purchase the product. Bob is the head architect of Coral8, and his job (as he described it) is to make sure that the product is as easy to use as possible.

Between Henry and Bob, two solutions were offered. I will go into the first solution in this blog entry. The second solution revolves around custom timestamping of messages by the input adapter, and this topic deserves a blog entry of its own.

The main problem was to analyze the order flow for each sector over a one minute timeslice, and determine if any sectors showed abnormal activity. The problem that I was faced with was that the concept of “time” was determined by the TransactTime field in the FIX message, and not by the “clock on the wall”. So, if for some reason, I received two FIX messages in a row, one whose TransactTime field was 14:24:57 and one whose TransactTime field was 14:25:01, then the receipt of the second FIX message should cause a new timeslice, regardless of what the wall clock said.

The solution that Henry came up with was to use a pulse in a stream. Although the concept of raising an event is very common is programming, it is not really something that you tend to do in SQL stored procedure. The thing is that programming in Coral8’s CCL (as well as the SQL-like dialects that many of the CEP vendors have) is a combination of procedural and SQL programming, and the trick is to find the correct “pattern” to solve your problem. This is where many of the CEP vendors can improve; they can publish a listing of patterns, they can come up with FAQs, etc. I mentioned this to Bob of Coral8, so expect to see some movement on this front from the Coral8 folks.

Here is what the pulse stream looks like in Coral8’s CCL:

----------------------------------------------------------------------------------
-- LastTimeSlice holds the maximum timeslice (0 to 389) of the order stream.
-- When we see an order with a TransactTime greater than the current max timeslice,
-- then we set the new max timeslice. We also use this as a signal (pulse)
-- to one of the streams below.
----------------------------------------------------------------------------------
CREATE VARIABLE INTEGER LastTimeslice = -1;
CREATE LOCAL STREAM stream_Pulse;

INSERT INTO stream_Pulse
SELECT
TimeToTimeBucket(FlattenNewOrder.TransactTime) AS epoch
FROM
FlattenNewOrder
WHERE
TimeToTimeBucket(FlattenNewOrder.TransactTime) > LastTimeSlice;

-- When we insert a new timeslice into the stream_Pulse stream, we also
-- set the new maxmimum timeslice.
ON stream_Pulse
SET LastTimeSlice = stream_Pulse.epoch; 

We have a global variable that keep the maximum timeslice that is flowing through our system. Since there are 6.5 hours in the trading day, there are 390 minute-sized timeslices that we want to consider.

In the INSERT statement, if the timeslice from the incoming FIX message is greater than the current maximum timeslice, then we insert a new record into the pulse stream.

The ON statement functions like a trigger. When a new record is inserted into a stream, you can have one or more ON statements that react to the event of inserting a record into the stream. Here, we set the new maximum timeslice.

We need to maintain a Window that contains all of the orders for the current timeslice. The order information includes the stock ticker, the sector that the stock belongs to, the number of shares in the order, and the current timeslice. In Coral8, a Window provides retention of records. You can specify a retention policy on a Window, whether it been a time-based retention policy (keep records in the window for 5 minutes) or a row-based retention policy (keep only the last 100 rows). What is missing here is a retention policy based on a boolean expression or on a certain column value changing. Streambase has this, and Coral8 knows that this feature should be implemented down the road.

----------------------------------------------------------------------------------
-- The TickerAndSector window holds all FIX orders for the current timeslice.
-- Each row of the window contains the FIX order and the sector information.
-- When we see a new timeslice, the TickerAndSelector window is cleared
-- using a DELETE statement.
----------------------------------------------------------------------------------
CREATE WINDOW TickerAndSector
SCHEMA (Ticker STRING, SectorName STRING, SectorId INTEGER, Shares INTEGER, TransactTimeBucket INTEGER)
KEEP ALL;

INSERT INTO TickerAndSector
SELECT
FlattenNewOrder.Ticker,
TickerToSectorMap.SectorName,
TickerToSectorMap.SectorId,
TO_INTEGER(FlattenNewOrder.Qty),
TimeToTimeBucket(FlattenNewOrder.TransactTime)
FROM
FlattenNewOrder,
TickerToSectorMap
WHERE
TickerToSectorMap.Ticker = FlattenNewOrder.Ticker
AND TimeToTimeBucket(FlattenNewOrder.TransactTime) >= LastTimeSlice; 

Now that we have a list of orders that occur for the current timeslice, we need to know when a new timeslice occurs. At this point, we need to analyze the orders for the current timeslice, find out which sectors are showing abnormal activity, and clear out the TickerAndSector window so that new orders can be accumulated for the new timeslice.

----------------------------------------------------------------------------------
-- The OrdersPerSectorPerMinute window contains the aggregated totals
-- for each sector for the previous timeslice. The aggregated totals include
-- the number of orders for each sector and the total number of shares for each sector.
--
-- The interesting part of this is the join between the TickerAndSector window
-- and the stream_Pulse. The stream_Pulse will be triggered when we see a new
-- timeslice.
--
-- When we insert rows into the OrdersPerSectorPerMinute window, we will trigger
-- a deletion of the old info in the TickerAndSector window.
----------------------------------------------------------------------------------
CREATE WINDOW OrdersPerSectorPerMinute
SCHEMA (SectorName STRING, SectorId INTEGER, OrderCount INTEGER, TotalShares INTEGER, Timeslice INTEGER)
KEEP 2 MINUTES;

INSERT INTO OrdersPerSectorPerMinute
SELECT
tas.SectorName, tas.SectorId, COUNT(*), SUM(tas.Shares), stream_Pulse.epoch
FROM
TickerAndSector tas, stream_Pulse
GROUP BY
tas.SectorId;

ON OrdersPerSectorPerMinute
DELETE FROM TickerAndSector
WHERE TransactTimeBucket < LastTimeSlice; 

As you can see from the above code, when a new timeslice appears, we aggregate the number of orders and the total number of shares that are in the TickerAndSector window. The interesting thing here, and the thing that I might not have figured out on my own, was that we need to join with the pulse stream that we talked about before. The pulse stream here is being used to “kick start” the calculating and dumping of the records in the current timeslice.

Finally, since we have aggregated the information for each sector for the current timeslice, we want to see if any sector exceeded the maximum “normal” number of orders.

----------------------------------------------------------------------------------
-- This output stream will alert the user when a sector exceeds the
-- max orders for that timeslice.
----------------------------------------------------------------------------------
INSERT INTO AlertStream
SELECT
R.SectorId, R.SectorName, R.OrderCount, R.TotalShares
FROM
OrdersPerSectorPerMinute AS R, NormalOrdersPerSectorPerTimeslice AS H
WHERE
R.SectorId = H.SectorId AND R.Timeslice = H.Timeslice AND R.OrderCount > H.MaxOrders; 

And, that’s it! If we attach a JMS output adapter to the AlertStream, we can generate a new, derived event, put that event back on the EMS bus (or we can send it into another Coral8 stream), and alert some kind of monitoring application.

Thanks to the Coral8 guys for helping me slog my way through the learning process.

©2007 Marc Adler - All Rights Reserved