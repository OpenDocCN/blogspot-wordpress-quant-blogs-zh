<!--yml
category: 未分类
date: 2024-05-18 05:05:01
-->

# Magmasystems Blog: Visualizations Update

> 来源：[http://magmasystems.blogspot.com/2007/12/visualizations-update.html#0001-01-01](http://magmasystems.blogspot.com/2007/12/visualizations-update.html#0001-01-01)

[Stephen Few](http://www.perceptualedge.com/about.php)

is rapidly positioning himself as the guru of business visualizations. His name has been brought to my attention several times over the past few weeks as someone to pay attention to .... "a new

[Edward Tufte](http://www.edwardtufte.com/tufte/)

", if you will.

Few has an online library with a lot of free articles to read. Right now, I'm reading

[Multivariate Analysis using Heatmaps](http://www.perceptualedge.com/articles/b-eye/heatmaps.pdf)

. This is especially worthwhile reading following last week's visit by Richard and Markus of

[Panopticon](http://www.panopticon.com/panopticon/)

, who showed more reasons why we should graduate from the free Microsoft

heatmap

control to the more feature-laden,

doubleplusunfree

,

Panopticon

product. As

Panopticon

adds more features in the value chain, it will be increasingly difficult to justify using a free product.

------------------------------------

Which brings me to another point that I have been thinking of ... a point that I raised on my previous blog posting. In the field of Enterprise Software, where do the responsibilities of a vendor begin and where do they end?

Take

Panopticon

, for instance. You can bind a streaming "

dataset

" to

Panopticon

, and

Panopticon

will render a

realtime

updating

Heatmap

to visualize that

dataset

. Of course, you ask how you get data into

Panopticon

, and you come back with the concept of input adapters.

Then, gradually, you wonder if their input adapters cover

KDB

, Wombat, Reuters,

Vhayu

,

OpenTick

, generic

JMS

, sockets, etc.

Then you wonder if

Panopticon

has input adapters that take the output of

CEP

engines, like Coral8 and

Streambase

. Or, you have a crazy thought like

Panopticon

embedding a copy of

Esper

/

NEsper

inside of itself.

Then, you get really greedy and wonder if

Panopticon

provides built-in FIX adapters that will devour a FIX 4.4 stream of orders and executions and show you what exchanges are slow today.

Then you wonder what kinds of analytical tools

Panopticon

might interface with ... since

Panopticon

is doing parsing and analysis of the streaming data anyway, can't it just take an extra step and analyze the silly data.

But, then if you are demanding all of these things of

Panopticon

and Coral8, how do you hook them together? Does the dog wag the tail or does the tail wag the dog?

Or, do we just consider

Panopticon

a simple visualization tool, demanding nothing more of it then the ability to display brightly colored rectangles of streaming data, and likewise, do we ask nothing more of Coral8 than to do what it does best ... recognize patterns and perform filtering and aggregations.

As Dali-

esque

as these thoughts may appear, this is the kind of things that I need to consider. In my quest for an ecosystem around the

CEP

engine, do we ask for the

CEP

engine vendors to expand outwards, or do we take the outer layer of components (

ie

: the visualization and analysis tools) and ask them to expand inwards to meet the

CEP

engine. Whatever it is, my wish would be for a true plug-and-play architecture between the

CEP

engine, its input components, and its output components.

©2007 Marc Adler - All Rights Reserved