<!--yml
category: 未分类
date: 2024-05-18 06:24:56
-->

# Clojure in Finance | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2013/05/24/clojure-in-finance/#0001-01-01](https://mdavey.wordpress.com/2013/05/24/clojure-in-finance/#0001-01-01)

## Clojure in Finance

It’s interesting to read the various snippets of [Clojure](http://www.drdobbs.com/mobile/thoughtworks-eyes-seismic-shift-in-progr/240009675) bank usage that are on the web.  Based on a quick Google, there [Deutsche](http://techmeshconf.com/techmesh-london-2012/presentation/Sharing%20Data,%20hiding%20Complexity%20(with%20Clojure%20and%20RDF)), UBS (blogged about previously) and [Citi](http://dev.clojure.org/display/community/Clojure+Success+Stories) as a minimum.  The general pattern appears to be that within a bank, a particular area manages to persuade management to accept the “new” language into the fold. [Pithering About](http://www.pitheringabout.com/?p=693) provides some reasons for [Clojure](http://www.drdobbs.com/mobile/thoughtworks-eyes-seismic-shift-in-progr/240009675) usage on a middle office project.

What is even more interesting in the Clojure world is [Datomic](http://www.datomic.com/). InfoQ has a few articles on [Datomic](http://docs.datomic.com/architecture.html) which provide a good introduction to this new distributed database:

One interesting attribute of Datomic is the [time](http://www.datomic.com/rationale.html) component, offering anyone is finance the possible usage of Datomic from a tickDB perspective.  I’d be curious to know of anyone who has PoC’d this concept, as it would make an interesting alternative to other vendor products such as [kdb](http://kx.com/kdb-plus-tick.php) and oneTick.

~ by mdavey on May 24, 2013.

Posted in [Languages](https://mdavey.wordpress.com/category/languages/)
Tags: [Clojure](https://mdavey.wordpress.com/tag/clojure/), [Datomic](https://mdavey.wordpress.com/tag/datomic/)