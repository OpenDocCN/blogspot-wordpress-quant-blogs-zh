<!--yml
category: 未分类
date: 2024-05-12 19:31:04
-->

# Upgrading the SpreadServe GUI | Coding the markets

> 来源：[https://etrading.wordpress.com/2015/09/19/upgrading-the-spreadserve-gui/#0001-01-01](https://etrading.wordpress.com/2015/09/19/upgrading-the-spreadserve-gui/#0001-01-01)

## Upgrading the SpreadServe GUI

### September 19, 2015

Recently I’ve been updating [SpreadServe](http://spreadserve.com)‘s JavaScript web GUI. The edit facility presented on the livesheet page was quite crude. It used a [bootstrap-editable](https://vitalets.github.io/x-editable/) to pop up an edit field in a message box. Not really a seamless user experience, so I’ve upgraded to a JavaScript grid that supports in place editing. The end result is a user experience closer to Excel itself. I chose to use [webismymind’s editablegrid](https://github.com/webismymind/editablegrid) since it can attach to an existing HTML table. In the case of SpreadServe the HTML table is generated in C++ code inside the [SpreadServeEngine](http://spreadserve.readthedocs.org/en/latest/guide.html) whenever a running spreadsheet is published to the [RealTimeWebServer](http://spreadserve.readthedocs.org/en/latest/config.html?highlight=realtimewebserver). I changed the C++ code to add attributes to the table and tr elements that editablegrid uses to latch on to. I made a couple of small changes to the editablegrid JavaScript so that the isEditable and modelChanged callbacks passed through more information. My isEditable implementation needed to get hold of the DOM element as well as the row column address so it could check for an ssedit attribute. And modelChanged needed the element ID so it could POST the changed data back to the RealTimeWebServer with a unique ID. The RealTimeWebServer sends the updated value back in to the SpreadServeEngine. I’ve [forked editablegrid](https://github.com/osullivj/editablegrid) [on github here](https://github.com/osullivj/editablegrid) with my changes. While I was doing this JS dev I found two resources very helpful: [Oscar Rotero’s jQuery cheat sheet](http://oscarotero.com/jquery/), and the [Chrome debugger](https://developer.chrome.com/devtools). I was a Firefox advocate for a long time, as Firebug was the first JavaScript debugger I used. The Chrome debugger is just faster, snappier, breakpointing is easier, and examining the DOM and variables seems better too.