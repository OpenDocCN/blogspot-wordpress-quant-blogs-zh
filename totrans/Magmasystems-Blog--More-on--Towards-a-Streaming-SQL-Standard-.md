<!--yml
category: 未分类
date: 2024-05-18 04:59:37
-->

# Magmasystems Blog: More on "Towards a Streaming SQL Standard"

> 来源：[http://magmasystems.blogspot.com/2008/08/more-on-towards-streaming-sql-standard.html#0001-01-01](http://magmasystems.blogspot.com/2008/08/more-on-towards-streaming-sql-standard.html#0001-01-01)

The title of the presentation "Towards a Streaming

SQL

Standard" might be a little misleading, in my opinion. The title of the paper might have been "Oracle does this,

Streambase

does that, let's make a new language construct that enables both products to do this and that". And this is a great example of cooperation between vendors who researchers probably share a common academic heritage.

I don't pretend to understand why the new SPREAD construct is important. It will probably dawn on me when my team has an actual use case that the SPREAD construct solves. This is the case that I experienced a few months ago with Coral8 when we needed windows that flushed themselves when a certain column changed value (

to be fair, Streambase

already had this in their language).

A few points:

1) Despite what I think about

Streambase's

marketing and sales organization, you must admit that

Zdonik

and

Cherniack

are first-class researchers, and have contributed a lot to the field of

CEP

.

2) I get confused about Oracle's

CEP

offering. Is this paper talking about the

CEP

product that came with the BEA purchase or the original Oracle

CEP

product? Does any of this include work that they may have incorporated from the purchase of

ESPER

?

3) I would love to see Coral8's and

Aleri's

responses to this paper. Do their versions of Streaming

SQL

already do what the new SPREAD operator is purporting to do?

4) Will any of this standards work bubble up to the work that the

STAC

A1 council is doing? The

STAC

A1 council must be vigilant to ensure that we don't include benchmarks that might show off a certain, vendor-specific feature, unless this new feature solves an important business case. Likewise, if the SPREAD operator is important enough that all vendors rush to implement it, then this should be part of the

STAC

benchmark suite.

5) If the SPREAD operator is important, I expect that Coral8 will implement it right away.

©2008 Marc Adler - All Rights Reserved.

All opinions here are personal, and have no relation to my employer.