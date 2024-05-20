<!--yml
category: 未分类
date: 2024-05-18 05:22:34
-->

# Magmasystems Blog: The Wall Street Stack

> 来源：[http://magmasystems.blogspot.com/2005/11/wall-street-stack_27.html#0001-01-01](http://magmasystems.blogspot.com/2005/11/wall-street-stack_27.html#0001-01-01)

It has been done plenty of times on Wall Street..... what I call the Wall Street Stack.

I just came off of a large project where I architected (yet another) one. I am current involved in one now. So are plenty of other people that I know in other companies.

Everyone's trading applications seems to be the same. Here are the standard elements:

1) The UI layer. The UI layer is usually designed around the Model-View-Controller pattern. It generally uses some third-party UI suite, such as Infragistics, Component One, or Syncfusion.

2) The UI usually contains an Outlook-style navigation bar on the left side. On the right is usually an MDI-ish area. There are multiple tabbed controls, each containing a grid control. The grid is a respresentation of the underlying business objects.

3) Filter criteria that is used to filter the results on the grid. The filter UI is usually placed on the same panel as the grid and consists of a number of comboboxes and edit fields that represent dates and static criteria. Filters can usually be translated into an SQL statement.... a dataview-like pattern can be applied to the underlying model to produce a filtered view.

4) User preferences and workspace persistence. Users can save the layout of the workspace, and load the layout when they log onto a new session from any machine.

5) Entitlements by role. Entitlements control various aspects of the UI, such as what menus, toolbar buttons, and controls are available to the user.

6) A Data layer that sits between the UI layer and the middle-tier. The data layer can contain a business facade, smart business objects (that are decorated with .NET attributes), a data access layer (contains a reference to the cache), and service providers that interface with a database and/or a middle-tier. The data layer can communicate with the middle-tier in both synchronous and asynchronous fashion.

7) Middle-tier (usually Java-based) that accesses the underlying database. Communication with the middle-tier is through some variant of XML (usually SOAP). (Sorry, .NET middle-tiers have not caught on yet in Wall Street ... I cite projects at Lehman, Wachovia, Citicorp, Goldman...)

8) Schemas shared between the client and middle-tier.

9) Subscription to asynchronous events, usually by some mechanism as a message bus (Tibco RV or EMS), or Smart Sockets (which is now owned by Tibco). When something happens to the underlying data, the middle-tier will broadcast an event to all of the clients that are hooked up to it. Each client has something that I call a "service agent", which is like a web service in reverse. The service agent receives the subscription event, and propogates the evented data up the chain.

10) A rich event manager. The event manager can be thought of as a mini-Tibco that resides totally within the client. The event manager should support wildcarding.

This stack is being implemented over and over again. The closest thing that I have seen to a corporate standard is the OCEAN framework that Goldman has.

There has to be a vendor who can commercialize this stack and sell it across the various financial companies. Anyone want to start a company with me????

As an aside, the Microsoft Composite Application Block bears close watching. However, it is only available for .NET 2.0\. Many of the current .NET-based projects are still using 1.1.

©2005 Marc Adler - All Rights Reserved