<!--yml
category: 未分类
date: 2024-05-12 19:37:54
-->

# F# for single dealer platforms | Coding the markets

> 来源：[https://etrading.wordpress.com/2009/12/21/f-for-single-dealer-platforms/#0001-01-01](https://etrading.wordpress.com/2009/12/21/f-for-single-dealer-platforms/#0001-01-01)

## F# for single dealer platforms

### December 21, 2009

Matt [shares his thoughts](http://mdavey.wordpress.com/2009/12/21/thoughts-on-f-within-a-single-dealer-platform-sdp/) on F# for SDP implementation [here](http://mdavey.wordpress.com/2009/12/21/thoughts-on-f-within-a-single-dealer-platform-sdp/). I don’t know as much about F# as he does, but I have dabbled with VS2010 and played with OCAML on Ubuntu at home. I’m sure the stateless functional approach will be a big help in structuring asynchrony and concurrency in server processes. So I agree with the general thrust of his argument here.

I would take issue with one of Matt’s statements: “If you think about an SDP, its primarily an integration build”. I have heard the same view espoused by managers who think an SDP build is just a trivial matter of hooking up some vendor servers like Caplin’s Liberator to internal middleware like the TIB, and hey presto, quotes and executions will flow. It’s nowhere near that simple. I prefer to say that building an SDP is like building an ECN. Think of it as building you’re own Bloomberg or TradeWeb.