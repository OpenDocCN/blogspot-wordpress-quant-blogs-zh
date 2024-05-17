<!--yml
category: 未分类
date: 2024-05-18 06:23:03
-->

# Language Coherence across the Stack | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2013/06/28/language-coherence-across-the-stack/#0001-01-01](https://mdavey.wordpress.com/2013/06/28/language-coherence-across-the-stack/#0001-01-01)

## Language Coherence across the Stack

Slashdot has an [interesting](http://slashdot.org/topic/bi/node-js-and-mongodb-turn-javascript-into-a-full-stack-language/) article, “Node.js and MongoDB Turn JavaScript into a Full-Stack Language” that basically makes a play for JavaScript client and server side being advantageous to avoid the historical fragmentation of incompatible disciplines within a project.  This fragmentation between client and server often leads to a disconnect when engineering user stories due to the simple fact that two software engineer are required with differing skill-set’s to work on the solution.

I’m not entirely clear what “widely supported path to security” means within the article.  I don’t see JavaScript server side being the solution to server side security issues.

Further, I think it will be a some while before we see down-stream servers written in JavaScript within the financial services world – by this I mean trade, matching, OMS’s etc

Additionally, I think Google is continuing to help move the game forwards in the JavaScript space.  Spending time with [AngularJS](http://angularjs.org/) has been nice.  The [tutorial](http://docs.angularjs.org/tutorial) is well written, and easy to follow.  [Angular-seed](https://github.com/angular/angular-seed) makes life easy, especially with inclusion of Karma.  Not tried adding in [Istanbul](http://karma-runner.github.io/0.8/config/coverage.html), but am expecting to like it for coverage.  Need to get time with [Polymer](http://www.polymer-project.org/) – maybe the next flight – especially given that AngularJS 2.0 will [build](http://www.2ality.com/2013/05/web-components-angular-ember.html) on [top](https://groups.google.com/forum/#!msg/polymer-dev/4RSYaKmbtEk/uYnY3900wpIJ) of Web [Components](http://www.2ality.com/2013/05/google-polymer.html).

Which all leads to though around D3’s [data](http://www.d3coder.com/2012/06/16/getting-started-with-data-joins/) joins and [binding](http://bost.ocks.org/mike/join/) to DOM elements.

~ by mdavey on June 28, 2013.

Posted in [JavaScript](https://mdavey.wordpress.com/category/languages/javascript/)
Tags: [AngularJS](https://mdavey.wordpress.com/tag/angularjs/), [D3](https://mdavey.wordpress.com/tag/d3/), [Istanbul](https://mdavey.wordpress.com/tag/istanbul/), [Polymer](https://mdavey.wordpress.com/tag/polymer/)