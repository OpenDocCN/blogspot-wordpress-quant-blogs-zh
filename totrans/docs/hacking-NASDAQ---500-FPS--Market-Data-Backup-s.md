<!--yml
category: 未分类
date: 2024-05-12 23:56:34
-->

# hacking NASDAQ @ 500 FPS: Market Data Backup`s

> 来源：[http://hackingnasdaq.blogspot.com/2014/04/market-data-backups.html#0001-01-01](http://hackingnasdaq.blogspot.com/2014/04/market-data-backups.html#0001-01-01)

[![http://www.costar.com/webimages/bluray.jpg](img/32a372a4a161e23d30749fc34baab076.png)](http://www.costar.com/webimages/bluray.jpg)

Been doing some housekeeping, part of which is cleaning up and standardizing HDD arrays. One of the sucky things about RAID is you need each physical disk to be the same size otherwise the space just sits there empty. As such needed to shuffle a bunch of data around and realized its time to put all my ITCH data into cold storage - have not touched it for quite some time.

All up its about 1.5TB worth compressed, decompressed probably 5-6TB or so. There`s a few options out there for this level of data backup

1) disconnected HDD

2) cloud backup service

3) burn optical disks

Option 1) would be the most obvious choice. HDD are cheap, transfers are fast. In theory HDDs are less robust than optical media due to moving parts/bearing failure vs non-moving part.

Option 2) just dosent work for TBs of data. Amazon Glacier costs ~ $0.01c / GB / month which isnt so bad, the killer is the bandwidth cost of $0.20c / GB to retrieve the data. Pushing total cost significantly above the cost of HDD or optical. Guess if you factor in redundancy into the HDD or optical storage size and Amazon isnt that bad. Still just not comfortable with a fixed monthly cost vs a onetime expenditure. 

Which leaves Option 3) Optical, meaning BluRay 25GB & 50GB disks. The media costs are quite a lot less than a HDD cost -> 50 disks @ 25GB each is around $30 == 1.25TB. But its a complete pain in the ass to burn that many. Ended up writing a script to almost automate the whole, copy, burn, verify cycle with a single disk taking around 3H in total.

In total its taken about a month to burn the dataset. Some days would get 5-6 disks done, others 1 or 0\. But there`s some sort of piece of mind I get from having data backed up in ROM. where only sunlight and a hammer can delete the files.