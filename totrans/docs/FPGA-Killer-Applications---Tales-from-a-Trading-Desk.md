<!--yml
category: 未分类
date: 2024-05-18 06:27:34
-->

# FPGA Killer Applications | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2013/04/18/fpga-killer-applications/#0001-01-01](https://mdavey.wordpress.com/2013/04/18/fpga-killer-applications/#0001-01-01)

## FPGA Killer Applications

*   Throughput reduction e.g market data line reduction.  To avoid data loss its beneficial to consume both A and B lines of market data from a venue. However, microbursts can cause queuing delays. FPGA network adapter line arb allow the throughput that a server CPU consumes to be halved, thus improving application latency, and reduce jitter (pre-processing packets of data prior to application consumption)
*   Order Book on the FPGA and off the server CPU.  Value-add: from cutting down on data that needs to cross the bus.
*   Pre-Trade checks.  Value-add: Off-loaded from the server CPU’s
*   Storage – off the back of the FPGA.  Value-add: Off-loaded from the server CPU’s
*   Ethernet Resilient

Remember, reading from PCI is expensive compared to memory – hence offload to the FPGA can be beneficial in certain cases.

~ by mdavey on April 18, 2013.

Posted in [Trading](https://mdavey.wordpress.com/category/trading/)