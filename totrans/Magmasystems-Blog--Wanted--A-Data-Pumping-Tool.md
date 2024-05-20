<!--yml
category: 未分类
date: 2024-05-18 05:17:59
-->

# Magmasystems Blog: Wanted: A Data Pumping Tool

> 来源：[http://magmasystems.blogspot.com/2006/09/wanted-data-pumping-tool.html#0001-01-01](http://magmasystems.blogspot.com/2006/09/wanted-data-pumping-tool.html#0001-01-01)

In the companies that I have been involved with in my Wall Street consulting career, it is remarkable how many systems do not have Unit Testing set up.

Concepts like Unit Testing, TDD, code metrics, etc are just starting to make their ways into development groups in IB's. However, one of the areas that has been ignored is stress and soak testing.

One of the tools that we need is what I refer to as a generic Data Pumper. This is a service that can be run to generate data of a certain shape, and pump the data into waiting applications. Some types of data that we may need to pump include quotes, executions, risk, etc.

Here are the features that I would like to see from a Data Pumper:

**Playback Modes**

We need to have the data replayed in certain temporal formats. We can also apply a distribution curve to the replay interval.

- Burst Mode: Play back data all at once, as fast as we can.

- Interval Mode: Play the data back at certain intervals. For example, playback 500 messages per second. We can also put some sort of distribution on the interval, so that the intervals would be the lowest at the beginning and at the end of the playback period (simulating market open and close).

- Timed Mode: This would cause playback at the exact timings that actual data was generated. In this mode, we would have to first capture real data and record the exact time that the real data was received. Then we would play back the simulated data using the timings of the real data.

**Transports**

We need to configure the transport mechanism which the data is delivered to the waiting application.

- Tibco RV or EMS (Right now, most IB's use Tibco for the distribution of high-frequency data)

- LBM (a Tibco competitor)

- Sockets (or SmartSockets)

- MQ or MSMQ

- CPS (Morgan Stanley)

**Data Generation** 

- Capture actual data for several days in order to provide some reference data

- We can tag certain fields for random data generation. For example, we can vary the prices of the various instruments.

- We can generate completely random data.

**Formats**

XML seems to be used in many places, but you have the latency involved in deserialization. Binary Objects is fast, but necessitates a homogeneous environment.

- XML

- Tibco binary message map

- delimited strings

- binary object

- Fixed-length ASCII

- Reuters (Craig will tell me about the legality of simulating data in Reuters format)

**Other Considerations** 

- Instead of sending data directly to the end application, we can send it to an object cache, and let the object cache handle distribution.

- We need a GUI for monitoring the transmission of data, and controls to let the user dynamically modify the timing intervals.

- We need to have probes in the target application so we can monitor its performance in real time under various loads.