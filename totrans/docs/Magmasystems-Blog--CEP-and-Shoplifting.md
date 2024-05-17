<!--yml
category: 未分类
date: 2024-05-18 04:59:29
-->

# Magmasystems Blog: CEP and Shoplifting

> 来源：[http://magmasystems.blogspot.com/2008/09/cep-and-shoplifting.html#0001-01-01](http://magmasystems.blogspot.com/2008/09/cep-and-shoplifting.html#0001-01-01)

Yesterday, I decided to drive the long way for a lunch with an ex-colleague of mine from Morgan Stanley. The local NPR public radio station (

WNYC

) has replaced the heavy metal station (

WSOU

) as my primary station in my car (sigh ... the joys of getting older ...), and I caught the last part of the Leonard

Lopate

show, a very popular news-talk show in New York.

Leonard was

[interviewing](http://www.wnyc.org/shows/lopate/episodes/2008/09/05)

John

Colapinto

, who had written an article for The New Yorker on loss prevention in stores ... commonly known as shoplifting.

What was fascinating was that, as John was talking about how store detectives monitor customer patterns for shoplifting, it seemed like the perfect thing for Complex Event Processing (I hope that Tim will agree that this is truly Complex).

Now, I am sure that this is not news to the

CEP

vendors out there. Fraud detection and surveillance is one of the big applications of

CEP

. But, after each detection pattern

Colapinto

described, I said to myself "How would we do this in Coral8?".

Some of the patterns

Colapinto

mentioned included:

1) Customers examining clothing without looking at the price tag.

2) Customers moving randomly from table to table. There seems to be a certain pattern of movement that is common amongst shoplifters.

In the "Shoplifter Alert System" that we would build, there would be multiple levels of complex events (Tim can correct me on the proper terminology to use) :

Level 1 Event

"This person is a shoplifter"

Level 2 Events

"This person is moving too randomly through the store"

"This person does not seem interested in the price"

Level 3 Events

The amount of time a person is spending at each "table" in the store

The amount of time a person handles each garment

A sensor on the price tag to indicate whether the person has looked at the price

Level 4 Events

A person has entered the store

A person has left the store

A person is moving through the store

I would love to hear any anecdotes about how

CEP

is actually being used in detecting shoplifting, so if you know of anything, please comment.

©2008 Marc Adler - All Rights Reserved.

All opinions here are personal, and have no relation to my employer.