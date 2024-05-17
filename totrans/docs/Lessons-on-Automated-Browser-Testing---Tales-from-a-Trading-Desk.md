<!--yml
category: 未分类
date: 2024-05-18 05:49:10
-->

# Lessons on Automated Browser Testing | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2014/06/02/lessons-on-automated-browser-testing/#0001-01-01](https://mdavey.wordpress.com/2014/06/02/lessons-on-automated-browser-testing/#0001-01-01)

## Lessons on Automated Browser Testing

Socket.io provides some [thoughts](http://socket.io/blog/introducing-socket-io-1-0/#automated-testing) around browser testing in this age of n browsers all with slightly different issues:

> Every commit to the Socket.IO codebase now triggers a testing matrix totaling to 25 browsers, including Android and iOS.
> 
> We accomplish this by having make test seamlessly set up a reverse tunnel to ephemeral ports in your computer (thus making it accessible from the outside world), and have them execute on the [Sauce](https://saucelabs.com/) Labs cloud, which is in charge of virtualizing and executing browsers on all the environments we care about.

~ by mdavey on June 2, 2014.

Posted in [Agile](https://mdavey.wordpress.com/category/agile/)