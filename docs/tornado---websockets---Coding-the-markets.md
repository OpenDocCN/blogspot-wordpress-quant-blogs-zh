<!--yml

类别：未分类

日期：2024-05-12 19:33:06

-->

# tornado & websockets | 编码市场

> 来源：[`etrading.wordpress.com/2014/04/26/tornado-websockets/#0001-01-01`](https://etrading.wordpress.com/2014/04/26/tornado-websockets/#0001-01-01)

## tornado & websockets

### 2014 年 4 月 26 日

我的[POC 原型](https://etrading.wordpress.com/2014/02/16/poc-m1-running/ "Proof of concept")的核心是一个服务器引擎，这并不适合做一个很好的演示。通常，如果人们能看到一个实在的实现，他们会更快地掌握概念。所以我需要一个现实的方法来展示服务器产生的实时跳动数据。一个浏览器 GUI 似乎是一个自然的选择。作为一个 Python 主义者，我想要用 Python 进行服务器编码。直到最近，将实时跳动数据推送到浏览器上是一件大事，需要像[Caplin Liberator](http://www.caplin.com/developer/component/liberator)这样的复杂服务器产品，以及像[Caplin Trader](http://www.caplin.com/caplin-trader)这样的丰富 GUI 工具包。幸运的是，现在使用一些非常简单的[jQuery](http://jquery.com/) & [websockets](http://www.websocket.org/)在浏览器中以及[tornado](http://www.tornadoweb.org/en/stable/)在服务器端编写一些演示软件是可能的，形式为一个实时跳动网页。JavaScript 和浏览器 GUI 不是我的强项，所以我不再评论，只是要注意这看起来比五年前容易多了。尽管如此，在服务器端，我的经验确实更多。早在 2000 年，我就在使用 Python 进行服务器端网络开发，使用的是[Zope](http://www.zope.org/)。Zope 是一个非常强大的系统，具有内置的对象数据库和实例继承而不是类机制的称为获取。因此，它有一个相当陡峭的学习曲线。近年来，[Plone](http://plone.org/)作为建立在 Zope 之上的 CMS 获得了一些关注。在 2001/2 年，我发现了[Twisted Matrix](https://twistedmatrix.com/trac/)，一个你可以用来构建任何基于 IP 的网络功能的通用网络工具包。再次，有一个陡峭的学习曲线，但它比 Zope 轻得多，现在非常成熟。我将使用 Twisted 为我的核心产品构建一个通用的套接字服务器功能：我已经有 C++和 Python API，但我需要一个套接字服务器用于 Java 支持。但我在演示目的上需要的是实时服务器推送到浏览器。而 tornado 被证明是一个很好的选择。简单，轻量级，有很多工作示例，完全集中在 websockets 上。很快就把跳动数据带入网页。推荐！
