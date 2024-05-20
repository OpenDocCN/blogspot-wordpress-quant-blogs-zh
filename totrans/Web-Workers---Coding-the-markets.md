<!--yml
category: 未分类
date: 2024-05-12 19:39:17
-->

# Web Workers | Coding the markets

> 来源：[https://etrading.wordpress.com/2009/07/22/web-workers/#0001-01-01](https://etrading.wordpress.com/2009/07/22/web-workers/#0001-01-01)

## Web Workers

### July 22, 2009

One of the hard restrictions that JavaScript GUIs like [Caplin Trader](http://www.caplin.com/caplintrader/) run up against is the single threadedness of the browser’s JavaScript engine. Organising the asynchronous execution of code to service both user interface and network events in a responsive and timely manner from a [Comet server](http://www.freeliberator.com/documentation/) is fiendishly difficult.

So I was heartened to read about [Web Workers](http://ejohn.org/blog/web-workers/) today. In future they would enable a GUI like Caplin Trader to handle network events on a background thread…