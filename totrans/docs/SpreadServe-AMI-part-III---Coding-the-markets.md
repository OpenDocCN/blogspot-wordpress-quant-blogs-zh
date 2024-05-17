<!--yml
category: 未分类
date: 2024-05-12 19:29:58
-->

# SpreadServe AMI part III | Coding the markets

> 来源：[https://etrading.wordpress.com/2017/03/06/spreadserve-ami-part-iii/#0001-01-01](https://etrading.wordpress.com/2017/03/06/spreadserve-ami-part-iii/#0001-01-01)

## SpreadServe AMI part III

### March 6, 2017

The SpreadServe 0.4.2b AMI is now available in the US West Oregon region: just search for SpreadServe in public images. There’s a now YouTube video on launching a SpreadServe AMI.

 [https://www.youtube.com/embed/1e5ffwtl-QA?version=3&rel=1&showsearch=0&showinfo=1&iv_load_policy=1&fs=1&hl=en&autohide=2&wmode=transparent](https://www.youtube.com/embed/1e5ffwtl-QA?version=3&rel=1&showsearch=0&showinfo=1&iv_load_policy=1&fs=1&hl=en&autohide=2&wmode=transparent)

VIDEO

Two points of interest came up in preparing the AMI: Admin password persistence, and the region bound nature of AMIs. [This blog from 2013](http://technotes.khitrenovich.com/notes-creation-windows-ami-ec2/) suggests that Admin passwords don’t persist in AMIs, but I’ve found they do now. So the Administrator password for a SpreadServe 0.4.2b AMI is SpreadServe042b. If you launch your own SpreadServe instance using the AMI, then I suggest you change the password!

The SpreadServe 0.4.2b AMI is only published in the US West Oregon region. Only AMI owners can copy to another region, so if you want a SpreadServe AMI in another region you’ll need to do a simple workaround: start an image in US West Oregon, stop it and create your own image, then [copy to your preferred region](https://aws.amazon.com/premiumsupport/knowledge-center/copy-ami-region/).