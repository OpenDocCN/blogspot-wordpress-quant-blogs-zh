<!--yml
category: 未分类
date: 2024-05-18 04:48:17
-->

# Magmasystems Blog: Brazil and Other Closing Thoughts for 2011

> 来源：[http://magmasystems.blogspot.com/2011/12/brazil-and-other-closing-thoughts-for.html#0001-01-01](http://magmasystems.blogspot.com/2011/12/brazil-and-other-closing-thoughts-for.html#0001-01-01)

Last week, I came back energized from the first two weeks of my engagement in Sao Paolo, Brazil. I am amazed at how Brazil is exploding, and there seems to be a lot of evidence to support my observations.

But, before I go into Brazil, I want to backtrack a few weeks.

After the demise of the investment banking arm of Citadel Securities (search Google News for the term "Citadel Securities" to reconstruct the happenings), I rejoined some old friends in the world of capital markets consulting. It feels a bit strange to be sitting on the other side of the table from where I sat for the past 5 years, but since I came from a consulting background, the transition was pretty smooth. Now I am the vendor, and my former colleagues are clients, and I expect to get beaten up by them in the same way that I used to micro-examine the vendors who courted me. But, a challenge is a challenge, and I hope that my Wall Street experience can serve my new clients well.

The first engagement that I had was in Miami Beach (yeah, life sucks, right?) for a few weeks in November. A client of ours has a product that is widely used in its industry, but there is a need for the product to be able to scale out massively in order to handle tens of thousands of simultaneous requests, and to be able to deal with more and more complex products. The current product was a mixture of some new .NET technology, combined with a lot of legacy VB6, ATL, C++, MFC, and the current system is designed to handle one request at a time.

[![](img/0ceb8143ba4103a7f25e783e796e1d00.png)](http://2.bp.blogspot.com/-uESONHXhimM/Tvsd7d07jyI/AAAAAAAABzM/5LrRGIwepe8/s1600/Miami+Beach+-+View+from+Balcony+of+Doubletree+-+2011-11.jpg)

My job was to propose a future state architecture that would allow them to scale up, handle failures gracefully, and allow pluggable components for pipelined processing of their data. One restriction was that their clients would incur zero or little additional cost. Without going into much detail, I ended up implementing a typical Wall Street compute-grid-like architecture using Rabbit MQ (hence, my previous posts on Rabbit) and Microsoft's Velocity Cache. This was an example where I was able to bring the kind of architecture that is typically found in Wall Street to a client who had never heard of grid computing before.

For my current engagement, I am traveling down to Sao Paolo, Brazil, for two-week stretches for the next several months. I am the head technologist on a small team that is analyzing the current state and proposing a new future state architecture for our capital markets client. I am not going to talk about what we are doing for the client, but I want to give my impressions of Brazil and Sao Paolo.

 Every day, it seems that articles like these are appearing in my news feed:

[Brazil overtakes UK as sixth-largest economy](http://www.guardian.co.uk/business/2011/dec/26/brazil-overtakes-uk-economy) [Miami Has a Hearty Oi (Hello) for Free-Spending Brazilians](http://www.nytimes.com/2011/12/28/us/miami-courts-free-spending-brazilians.html) [Brazil Offers Opportunities and Risks For Wall Streeters On the Move](http://news.efinancialcareers.com/69727/brazil-offers-opportunities-and-risks-for-wall-streeters-on-the-move/)

Traveling through Sao Paolo, you can feel the excitement of the city. Like they know that they are the next big thing. New York, without the tension and angst of New York. There are new office buildings springing up everywhere. Brookfield has an incredible new building under construction by the Faria Lima financial center. The Grand Hyatt's executive lounge crowded with all sorts of foreigners trying to get in on the action before others do.

Sao Paolo is huge ... bigger than NYC ... but the office buildings are spread out all over the city. I did not get the feeling of a single financial district as you would find in NYC, Miami, Charlotte, or San Francisco. The subway (metro) is not as extensive as it is in NYC, so odds are that you need to take a taxi to go from office to office. Taxis are convenient and relatively inexpensive, but the traffic ....

You really need to be able to speak Brazilian Portuguese. Whoever told me that everyone under 30 speaks English was lying. Your high school Spanish might bring you some comfort, but not much. Brazilians do not like speaking Spanish, but if you speak Spanish with a strong American accent, they might be willing to forgive you.

Not everything is sunshine and lollipops .... Crime is something tangible and is definitely the huge thorn on the rose. I was told never to show a hint of my laptop while in a taxi, because roving gangs of motorcycle thieves are everywhere, and they will surround your taxi and take your laptop at gunpoint. A Brazilian that I was having dinner with had to take a taxi for the 5-block walk to his hotel because he was afraid of being robbed... and this was in a good section of Sao Paolo. Luxury hi-rise apartments look beautiful from your hotel room, but when you view them from the sidewalk, you see the 30-foot barbed-wire walls and teams of black-booted security guards patrolling the grounds.

Traffic is a mess too. Stand-still traffic at almost all hours of the day. If you are traveling between offices and you choose to go by taxi, give yourself an hour to go two miles.

The traffic and the fear of crime combine to make Sao Paolo the city with the greatest number of helicopters per capita. Almost every office building has a helipad on the roof, and for a pilot like myself, it's exciting to see the constant flow of helicopters 500 feet above your head.

It will be interesting to see if Sao Paolo and Rio can get their acts together before the World Cup in 2014 and the Olympics in 2016\. Lots of problems to be solved. But, if Athens can do it, then Brazil should be able to pull it off too.

Sao Paolo to make it an interesting challenge. But, I think that they are very receptive to Wall Street and City experience. A bunch of people have been anxious to know about my experience in Brazil because it seems that the mood on Wall Street has never been gloomier, and people want to have a bit of a change-up in their lives. My opinion is that a bit of international experience in Brazil will be very helpful to a career in Capital Markets, especially in the IT world. Certain investment banks are willing to send their folks to Brazil on a 3-year program. Why not roll the dice!

Have a happy 2012\. As always, comments and questions are welcome.

-marc

©2011 Marc Adler - All Rights Reserved. All opinions here are personal, and have no relation to my employer.