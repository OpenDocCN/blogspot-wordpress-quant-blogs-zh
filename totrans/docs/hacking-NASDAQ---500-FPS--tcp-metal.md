<!--yml
category: 未分类
date: 2024-05-13 00:05:29
-->

# hacking NASDAQ @ 500 FPS: tcp metal

> 来源：[http://hackingnasdaq.blogspot.com/2010/02/tcp-metal.html#0001-01-01](http://hackingnasdaq.blogspot.com/2010/02/tcp-metal.html#0001-01-01)

Quick update on what TCP metal vs linux look like? Our TCP stack is err... not finished but enough is done to get some sort of ballpark numbers.

[![](img/dddb35c1073537abf5760836fd78c6e3.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjUenWMNLgfsTdkzcZl_J0nywhLx2EeGgW4Y5Mm7qeuKKoVHP_bIp95S6KmcWuD-fNN2ivFARQaDv82KG5mfGrACRDtnDxgnssWdT0HSvhvC3aOIpthQuMM8N3INDWPjoXsG1nzAiPrzQ/s1600-h/round_tcp_metal.png)

128B TCP all metal

[![](img/389a23660063e1ac337da1defb2e3941.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjBkq3zagM53n8CW66Tl1zqCwhg3e8Pc5_wjve8MIb9LcVYr3o5n0G3Mz1GG1dirOjhXDhkGStcEZibX3hJFyAEp4NsaKmjOQ2gwrVz4UHggy_yMeD_C8Opdq3oyr5BWQRbMyC6xhvC0Q/s1600-h/round_tcp_linux.png)

128B TCP metal->linux->metal

As you can see we`re only just beating out linux here, to the tune of 1-2,000ns - and we`re not even a complete tcp stack yet! Certainly not what I expected but goes to show linux is pretty dam good... or my first pass code is really sucky. So need to slash around 5,000 cycles off our implementation... things finally getting interesting.