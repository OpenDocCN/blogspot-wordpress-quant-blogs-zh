<!--yml
category: 未分类
date: 2024-05-18 07:04:48
-->

# Physics Perspective: Brouwer's fixed point theorem...why mathematics is fun

> 来源：[http://physicsoffinance.blogspot.com/2011/09/brouwers-fixed-point-theoremwhy.html#0001-01-01](http://physicsoffinance.blogspot.com/2011/09/brouwers-fixed-point-theoremwhy.html#0001-01-01)

**UPDATE BELOW**

I'm not going to post very frequently on Brouwer's fixed point theorem, but I had to look into it a little today. A version of it was famously used by Ken Arrow and Gerard Debreu in their 1954 proof that general equilibrium models in economics (models of a certain kind which require about 13 assumptions to define) do indeed have an equilibrium set of prices which makes supply equal demand for all goods. There's a nice review article on that

[here](http://cowles.econ.yale.edu/P/cp/p10b/p1090.pdf)

for anyone who cares.

Brouwer's theorem essentially says that when you take a convex set (a disk, say, including both the interior and the boundary) and map it into itself in some smooth and continuous way, there has to be one point which stays fixed, i.e. is mapped into itself. This has some interesting and counter-intuitive implications, as some contributor to Wikipedia has pointed out:

> The theorem has several "real world" illustrations. For example: take two sheets of graph paper of equal size with coordinate systems on them, lay one flat on the table and crumple up (without ripping or tearing) the other one and place it, in any fashion, on top of the first so that the crumpled paper does not reach outside the flat one. There will then be at least one point of the crumpled sheet that lies directly above its corresponding point (i.e. the point with the same coordinates) of the flat sheet. This is a consequence of the *n* = 2 case of Brouwer's theorem applied to the continuous map that assigns to the coordinates of every point of the crumpled sheet the coordinates of the point of the flat sheet immediately beneath it.
> 
> Similarly: Take an ordinary map of a country, and suppose that that map is laid out on a table inside that country. There will always be a "You are Here" point on the map which represents that same point in the country.

**UPDATE**

In comments, "computers can be gamed" rightly points out that the theorem only works if one considers a smooth mapping of a set into itself. This is very important.

Indeed, go to the Wikipedia page for Brouwer's theorem and in addition to the examples I mentioned above, they also give a three dimensional example -- the liquid in a cup. Stir that liquid, they suggest, and -- since the initial volume of liquid simply gets mapped into the same volume, with elements rearranged -- there must be one point somewhere which has not moved. But this is a mistake unless you carry out the stirring with extreme care -- or use a high viscosity liquid such as oil or glycerine.

Ordinary stirring of water creates fluid turbulence -- disorganized flow in which eddies create smaller eddies and you quickly get discontinuities in the flow down to the smallest molecular scales. In this case -- the ordinary case -- the mapping from the liquid's initial position to its later position is NOT smooth, and the theorem doesn't apply.