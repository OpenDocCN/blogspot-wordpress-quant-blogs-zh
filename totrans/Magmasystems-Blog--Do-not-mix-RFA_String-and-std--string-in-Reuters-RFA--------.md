<!--yml
category: 未分类
date: 2024-05-18 04:57:10
-->

# Magmasystems Blog: Do not mix RFA_String and std::string in Reuters RFA !!!!!!!

> 来源：[http://magmasystems.blogspot.com/2008/11/do-not-mix-rfastring-and-stdstring-in.html#0001-01-01](http://magmasystems.blogspot.com/2008/11/do-not-mix-rfastring-and-stdstring-in.html#0001-01-01)

Some days, it's good to Always Be Coding. Today, it wasn't.

I just spent an entire day chasing down a problem, trying to merge the Reuters OMM API into our MarketFeed-based app. Thanks to Apurva, I was led to a small paragraph in a Readme file that said:

Known Deficiencies- Mixing of RFA_String and std::string in application interface and implementation

As soon as I got rid of the std::string references in the code, everything magically worked!

©2008 Marc Adler - All Rights Reserved.

All opinions here are personal, and have no relation to my employer.