<!--yml
category: 未分类
date: 2024-05-12 19:31:14
-->

# Spreadsheets are code | Coding the markets

> 来源：[https://etrading.wordpress.com/2015/08/13/spreadsheets-are-code/#0001-01-01](https://etrading.wordpress.com/2015/08/13/spreadsheets-are-code/#0001-01-01)

## Spreadsheets are code

### August 13, 2015

[Felienne Hermans](http://www.felienne.com/) has made it her mission to point out that [“spreadsheets are code”](http://www.slideshare.net/Felienne/spreadsheets-are-code-online). She’s most definitely right about that, and a whole host of the other consequences that she draws from that insight, specifically that we should apply the [techniques developed by mainstream software engineering to spreadsheets](http://spreadsheetlab.org/sems15/): version control, testing and design guidelines for clean structure, like the FAST standard. Whenever you create a sheet with formulae in it you’re programming. Ignoring that fact is one of the reasons spreadsheet disasters keep happening. I couldn’t agree more with Prof Hermans on that score. But I think we need to go further in the comparison of spreadsheets with code, and point out some major differences.

1.  Conventional code, when deployed to its production runtime environment does not come with an IDE that enables any user to change the implementation! A trader can’t reach inside his Bloomberg or TradeWeb terminal and change its implementation. But Excel allows any user to change any formula in a financial model.
2.  Well structured conventional code separates user interface from business logic. This separation of concerns is often called the MVC pattern. A typical modern web application has an HTML/CSS/JavaScript user interfaces running in browsers talking to a server hosted backend coded in Python on top of Django and an RDBMS. Excel makes it impossible to decouple the user interface from the logic expressed in formulae and VBA. Modern applications present a choice for their architects; does a given piece of code belong in the browser, the server tier or the DB ?
3.  Conventional code enables reuse through components. Each Excel spreadsheet is like an island, and monolithic. How can spreadsheets be composed together to draw input and feed output to each other? Only with manual, error prone operations.
4.  Unit testing: the unit testing philosophy calls for any significant component to have a set of separate test code that proves compliance with pre and post conditions as well as yielding specified results. Also required is the ability to run a set of tests automatically and record the results. All of that is a capability that Excel simply doesn’t have.

To realise points 1 to 4 for spreadsheets we need an alternate run time that can host spreadsheets on a server, and decouple the financial logic expressed in worksheet formulae, VBA & XLLs from the user interface. In the next post I’ll give more detail on how [SpreadServe](http://spreadserve.com) solves all the issues raised above.