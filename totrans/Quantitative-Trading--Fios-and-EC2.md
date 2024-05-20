<!--yml
category: 未分类
date: 2024-05-12 19:18:05
-->

# Quantitative Trading: Fios and EC2

> 来源：[http://epchan.blogspot.com/2009/04/fios-and-ec2.html#0001-01-01](http://epchan.blogspot.com/2009/04/fios-and-ec2.html#0001-01-01)

As an algorithmic trader, I am constantly in search of a better physical infrastructure where I can connect via the internet to my execution broker at the highest speed and with the least possibility of outage, and at a reasonable cost.

To that end, I would like to mention

[Fios](http://www22.verizon.com/Residential/FiOSInternet/FiOSvsCable/FiOSvsCable.htm)

, a fiber-optics service from Verizon with download speed of 50 Mpbs, upload speed is 20 Mbps, both faster than your typical T-1 line (1.5 Mbps). Furthermore, it costs only $45/month. Hey, even

[Paul Krugman](http://krugman.blogs.nytimes.com/2009/03/23/incommunicado-probably/)

has installed it at his home!

(I haven't tried it myself, and would like to hear from those of you who have and see if it is time to say goodbye to T-1.)

And as I have

[reported](http://epchan.blogspot.com/2009/01/algorithmic-trading-technology-update.html)

earlier, I am also constantly looking for a good cloud computing platform so that I can run more strategies without cluttering my office with computers. Finding one will obviate the need for any big investment in internet connectivity at the office.

To that end, I have been trying out Amazon's EC2 for several months. I use it to run one of our strateiges, and I have to report that my experience is mixed.

Firstly, if you are not an IT person, it does take a lot of time (8 person-hours?) to get set up and running, especially with their securities precautions. The learning curve is steep.

Secondly, and more annoyingly, the instances sometimes fail to start properly, or fail to bundle properly. (Bundling means saving the software configuration for future use.) I am using Windows instances. Maybe those who use Linux instances have better experiences?

Thirdly, and most annoyingly, when a new instance is started, Windows often cannot automatically synchronize its clock with time.windows.com or any other internet clock. As a result, the time is often wrong. Now, this may not be a big deal for usual office work. But when your automated trading strategy depends crucially on the time of the day, it can be quite fatal to your profit. If anyone has experienced a similar problem with Window's clock and know a fix, please let me know!

Despite all these hassles, I am still running strategies on EC2, hoping that once EC2 get past the beta release, things will be better.