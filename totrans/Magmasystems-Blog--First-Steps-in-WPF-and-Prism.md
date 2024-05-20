<!--yml
category: 未分类
date: 2024-05-18 04:49:34
-->

# Magmasystems Blog: First Steps in WPF and Prism

> 来源：[http://magmasystems.blogspot.com/2011/08/first-steps-in-wpf-and-prism.html#0001-01-01](http://magmasystems.blogspot.com/2011/08/first-steps-in-wpf-and-prism.html#0001-01-01)

As I mentioned in my last posting, I want to spend a little time to better educate myself on WPF and Microsoft Prism. I see both of these being used more and more in Capital Markets applications, and I want to see if these two will truly allow me to build better applications faster.

I spent the last few days on a little sprint to come up with a prototype of a "Quote Workbench" that I could eventually expand into an algo trading platform or a backtesting platform. All of this code was written from scratch. My only tool was Visual Studio 2010\. There are no third-party commercial controls involved, so that if you wanted to download this code and build it yourself, you would not have to purchase any additional software.

I ended up using two small DLLs that I found on CodeProject and CodePlex. One was a

[set of themes](http://datagridthemesfromsl.codeplex.com/)

for the Microsoft WPF DataGrid, and the other was a

[color picker control](http://wpfcolorpicker.codeplex.com/)

that I needed to enhance in order to support WPF Databinding.

I am also curious to see if the Microsoft DataGrid can keep up with a high volume of real-time quotes. Most of the time, there is some sort of quote throttling that goes on before the quotes ever reach the grid. The general rule of thumb is that human eyes can only follow two updates per second. And, unless your GUI has some sort of CEP system or business rules embedded in it, you can usually get away of throttling quotes to the GUI. Nevertheless, I am curious to see if WPF-based grids can keep up with a high volume of quotes. From what I have heard, some of the commercial grids (DevExpress, Syncfusion, Infragistics, Xceed) are more performant that the out-of-the-box Microsoft DataGrid, but I do not have these commercial UI toolkits at my disposal right now.

From my recent experience, it seems that most developers are wrapping Winforms grids in a WindowsFormsHost control, and are not going to native WPF grids. If you have any opinions on the performance of Winforms vs WPF grids, please post a comment here.

The idea for this sprint was to write two applications, a quote server and a quote client. The quote server spits out two types of quotes, Level 1 and Level 2 equity quotes. The quote client consumes these quotes and displays the Level 1 quotes in a WPF DataGrid and displays the Level 2 quotes in a standard Depth-of-Book control.

Since the overall theme of this exercise was to learn as much WPF and Prism as possible in the shortest amount of time, I did not pay attention to the way that the GUI looks. Nor did I try to optimize the internal plumbing. A lot of the application was designed to explore as much of WPF as possible, especially aspects surrounding Data Binding. My goal for Prism was to have as much loose coupling as possible.

The first task was to write a Level 1 Equity Quote simulator. This is always a useful thing to have in your bag of tools. I preloaded a quote cache with a few symbols, and implemented a few strategies with which I could pump out quotes. Right now the strategies are limited to Round Robin and Random. A next step would be to download a list of the S&P 500 and corresponding Average Daily Volumes (ADV) for each instrument. A new strategy would be to generate quotes based on the weighted ADVs.

I also put GUIs in both the quote server and quote client so that I can see if there is any noticeable latency in delivering quotes from the server to a GUI. Of course, since I am delivering it between processes on my laptop, there shouldn't be any latency. But, if I decide to experiment with Comet and deliver the quotes across the Internet to a web-based GUI, then it's useful to have a monitoring GUI attached to the quote server.

The Level 1 quote simulator is fairly dumb right now. All it does is push out a lot of quotes at a user-specified rate. Additional improvements to the quote simulator would be

*   Let the client subscribe and unsubscribe to specific quotes

*   Use the FIX QuoteRequest  message for this

*   When no clients are interested in a symbol, automatically stop publishing
*   Use something like Google Finance or Yahoo Finance to seed the initial quotes with realistic values

Once I got the quote simulator working, and the quotes updating the server-side DataGrid in real-time, I wanted to send the quotes from the server to the client. For that, I decided to publish the quotes using the FIX Protocol. I downloaded a copy of QuickFIX.Net, and created a Prism module that would take a stream of internally generated quote objects and push them across the wire to a FIX subscriber. Generally, you would not use FIX to push across a high volume of equity quotes. But, since this is a toolbox for experimentation, and since we want to stick with some free tools that implement a quasi-standard, let's just use FIX.

*Note - The QuickFIX assembly is built with .NET 2.0, so we need to add  useLegacyV2RuntimeActivationPolicy="true" to the app.config file for any application that uses QuickFix.NET.*

<configuration>
  <startup uselegacyv2runtimeactivationpolicy="true">
    <supportedruntime sku=".NETFramework,Version=v4.0" version="v4.0"/>
  </startup>
</configuration>

Now I had Level 1 equity quotes flowing between the client and server, I wanted to start publishing Level 2 quotes. I wrote a simple Book Generator that, given a certain symbol, generates an entire new book at a specified interval. Of course, this is not how the real world works. Generally, when you receive a book, you receive the initial image of the book and then incremental updates. The job of the book builder module would be to build up a complete order book for all of the subscribed instruments, and ship out deltas to the GUI. The GUI would then need to insert new rows in the book, delete rows in the book, or modify rows in the book. I will leave this for a later exercise.

How can I transmit the book from the server to the GUI? I coded up a quick WCF PubSub mechanism using the NetTCP binding. The book was transmitted across the wire as a SOAP message. Not very good for performance, but OK for interoperability in case I want to write an iOS-based or web-based GUI.

Improvements for the Level 2 Simulator are similar to the improvements I need to make to the Level 1 simulator, and include:

*   Improve performance - use binary encoding where possible, and investigate WCF-specific improvements
*   When a client subscribes to a symbol, send the full image and deltas, not the entire book.
*   The pub-sub "topics" should contain information about the specific security
*   Let the client subscribe and unsubscribe to specific quotes
*   When no clients are interested in a symbol, automatically stop publishing
*   Use something like Google Finance or Yahoo Finance to seed the initial quotes with realistic values
*   In the GUI, let the user switch between aggregated and non-aggregated views of the book. In an aggregated view, we aggregate the volume at each price point.

A screenshot of version 0.0001 is included below. Just a reminder that the GUI was coded so that I could explore different aspects of WPF and Prism, and is intended to be a test bench for learning.

What's next?

Probably a very light exchange simulator. I don't have access to a high-quality commercial product like the Aegis Exchange Simulator, but several years ago, a reader of this blog sent me the binary of a small exchange simulator that he wrote.

To keep on the track of investigating new technology, I would like to explore Microsoft-specific frameworks like TPL and perhaps Rx. I need to go over Matt Davey's blog and get some ideas :-)

The depth-of-book view can use some new kind of visualization in aggregated mode.

There is some unfinished business that I have with Microsoft StreamInsight. I would like to provide a GUI that allows the user to create CEP queries, and have StreamInsight monitor the quote stream and provide alerting. I haven't looked at SI in two years, and I don't even know if I have access to it if I don't have a MSDN subscription. I can always used NEsper as a fallback (is Esper still around?)

©2011 Marc Adler - All Rights Reserved. All opinions here are personal, and have no relation to my employer.