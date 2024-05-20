<!--yml
category: 未分类
date: 2024-05-12 19:29:27
-->

# TFWebSock: TransFICC web socket server | Coding the markets

> 来源：[https://etrading.wordpress.com/2017/09/05/tfwebsock-transficc-web-socket-server/#0001-01-01](https://etrading.wordpress.com/2017/09/05/tfwebsock-transficc-web-socket-server/#0001-01-01)

## TFWebSock: TransFICC web socket server

### September 5, 2017

I’ve just updated my Netty based TransFICC web socket server to work with [version 330cb31-3670](https://github.com/TransFICC/client-library/releases/tag/2de5581) of the [TransFICC API](https://transficc.com/products) and service. [TFWebSock](https://github.com/SpreadServe/TFWebSock) enables web socket clients to subscribe to TransFICC sourced market data. Those web socket clients could of course be browsers, but in the case of [this demo](http://sscalc0.online/tfsock3.xls/Swaps) the client is the [SSAddin Excel addin](https://github.com/SpreadServe/SSAddin). Which means that you can use TFWebSock and SSAddin to pull live ticking [ICAP iSwap](http://www.icap.com/what-we-do/electronic-markets/i-swap.aspx) swap rates into Excel on your desktop. And if you want to automate and serverize that spreadsheet you can do so with [SpreadServe](http://spreadserve.com).

I should point out that the ticking rates in this demo are from the iSwap test system, and are not live production rates. Many thanks to the teams at TransFICC and ICAP for making this data available!