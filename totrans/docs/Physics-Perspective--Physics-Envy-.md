<!--yml
category: 未分类
date: 2024-05-18 07:08:52
-->

# Physics Perspective: Physics Envy?

> 来源：[http://physicsoffinance.blogspot.com/2011/05/physics-envy.html#0001-01-01](http://physicsoffinance.blogspot.com/2011/05/physics-envy.html#0001-01-01)

I just came across

[this post](http://rick.bookstaber.com/2010/08/physics-envy-in-finance.html)

from late last year by Rick Bookstaber, someone I respect highly and consider well worth listening to. Last year when researching

[an article on high-frequency trading](http://www.wired.co.uk/magazine/archive/2010/04/start/investigation-the-business-of-high-frequency-trading)

for Wired UK, insiders in the field strongly recommended Bookstaber's book

[A Demon of Our Own Design: Markets, Hedge Funds and the Perils of Financial Innovation](http://www.amazon.com/Demon-Our-Own-Design-Innovation/dp/0471227277)

. It is indeed a great book as Bookstaber draws on a wealth of practical Wall St. experience in describing markets in realistic terms, without resorting to the caricatures of academic finance theory.

In his post, he makes an argument that seems to contradict everything I'm writing about here. Essentially, he argues that there's already too much "physics envy" in finance, meaning too much desire to make it appear that market functions can be wrapped up in tidy equations. As he puts it,

> ...physics can generate useful models if there is well-parameterized uncertainty, where we know the distribution of the randomness, it becomes less useful if the uncertainty is fuzzy and ill-defined, what is called Knightian uncertainty.
> 
> I think it is useful to go one step further, and ask where this fuzzy, ill-defined uncertainty comes from. It is not all inevitable, it is not just that this is the way the world works. It is also the creation of those in the market, created because that is how those in the market make their money. That is, the markets are difficult to model, whether with the methods of physics or anything else, because those in the market make their money by having it difficult to model, or, more generally, difficult for others to anticipate and do as well.

Bookstaber goes on to argue that it is this relentless innovation and emergence of true novelty in the market which makes physics methods inapplicable:

> The markets are not physical systems guided by timeless and universal laws. They are systems based on creating an informational advantage, on gaming, on action and strategic reaction, in a space without well structured rules or defined possibilities. There is feedback to undo whatever is put in place, to neutralize whatever information comes in.
> 
> The natural reply of the physicist to this observation is, “Not to worry. I will build a physics-based model that includes feedback. I do that all the time”. The problem is that the feedback in the markets is designed specifically not to fit into a model, to be obscure, stealthy, coming from a direction where no one is looking. That is, the Knightian uncertainty is endogenous. You can’t build in a feedback or reactive model, because you don’t know what to model. And if you do know – by the time you know – the odds are the market has changed.

I think this is an important and perceptive observation, yet it also strongly misrepresents what physicists -- the ones doing good work, at least -- are trying to do in modeling markets. Indeed, I think it's fair to say that much of the work in what I call the physics of finance starts from the key observation that "feedback in the markets is designed specifically not to fit into a model, to be obscure, stealthy, coming from a direction where no one is looking." The best work in no way hopes to wrap up everything in one final tidy equation (as in the cartoon version of physics, although very little real physics works like this), or even one final model solved on a computer, but to begin teasing out -- with a variety of models of different kinds -- the kinds of things that can happen and might be expected to happen in markets dense with interacting, intelligent and adaptive participants who are by nature highly uncertain and trying to go in directions no one has gone before.

A good example is

[a recent paper](http://arxiv.org/PS_cache/arxiv/pdf/1105/1105.1694v1.pdf)

(still a pre-print) by Bence Toth and other physicists. It's a fascinating and truly novel effort to tackle in a fundamental way the long-standing mystery of market impact -- the widely observed empirical regularity that a market order of size V causes the price of an asset to rise or fall in proportion (roughly) to the square root of V. The paper doesn't start from the old efficient markets idea that all information is somehow rapidly reflected in market prices, but rather tries to actually model how this process takes place. It begins with the recognition that when an investor has valuable information, they don't just go out and release it to the market in one big trade. To avoid the adverse effects of market impact -- your buying drives the price up so you have to buy at ever higher prices -- those with large orders typically break them up into lots of pieces and try to disguise their intentions and reduce market impact. As a result, the market isn't at all a place where all information rapidly becomes evident. Most of the trading is being driven by people trying to hide their information and keep it private as long as possible.

In particular, as Toth and colleagues argue, the sharp rise of market impact for very small trades (the infinite slope of the square root form at the origin) suggests a view very different from the standard one. Many people take the concave form of the observed impact function, gradually becoming flatter for larger trades, as reflecting some kind of saturation of the impact for large volumes. Perhaps. But the extremely high impact of small trades is perhaps a more interesting phenomenon. The square root form in fact implies that the "susceptibility" of the market -- the marginal price change induced per unit of market order -- heads toward infinity in the limit of zero trade size. A singularity of this kind in physics or engineering generally signals something special -- a point where the linear response of the system (reflecting outcomes in direct proportion to the size of their causes) breaks down. The market lives in a highly unstable state.

Toth and colleagues go on to show that this form can be understood naturally as arising from a critical shortage of liquidity -- that is, a perpetual scarcity of available small volume trades at the best prices. I won't get into the details here (as I will return to the topic in greater detail soon), but their model depends crucially on the idea that much information remains "latent" or hidden in the market, and only gets revealed over long timescales. It remains hidden precisely because market participants don't want to give it away and incur undue costs associated with market impact. The upshot -- although this needs further study to flesh out details -- is that this perpetual hiding of information, and the extreme market sensitivity it gives rise to for small trades, might well lie behind the surprising frequency with which markets experience relatively large movements up or down, apparently without any cause.

This is just the kind of the thing that anyone interested in a deeper picture of market dynamics should find valuable. It's the kind of fundamental insight that, with further development, might even suggest some very non-obvious policy steps for making markets more stable.

Much the same can be said for a variety of physics-inspired studies on complex financial networks,

[as reviewed recently in *Nature*](http://www.nature.com/nature/journal/v469/n7330/full/nature09659.html)

by May and Haldane. These models also share a great resonance with ecology and the study of evolutionary biology, which Bookstaber suggests might be more appropriate fields in which to find insights of value to financial theory. These fields do have much that is valuable, but even here it is hard to get away from physics. Indeed, some of the best models in either theoretical ecology or evolutionary biology -- especially for evolution at the genetic level over long timescales -- have also been strongly inspired by thinking in physics. A case in point

[is a recent theory](http://guava.physics.uiuc.edu/%7Enigel/REPRINTS/2011/Goldenfeld-Woese%20Life%20is%20Physics%202011.pdf)

for the evolution of so-called horizontal gene flow in bacteria and other organisms, developed by famous biologist Carl Woese along with physicist Nigel Goldenfeld.  

This wide reach of physics doesn't show, I think, that physicists are smarter than anyone else. Rather, just that physicists have inherited a very rich modeling culture and tools -- developed in statistical physics over the past few decades -- that are incredibly powerful. If there is physics envy  in finance -- and Bookstaber asserts there is -- it's only a problem because the wrong model of physics is being envied. Forget the elegant old equation based physics of quantum field theory. Nothing like that is going to be of much help in understanding markets. Think more of the more modern and much more messy physics of fluid and plasma instabilities in supernovae, or here on Earth in the project to achieve

[inertial confinement fusion](http://en.wikipedia.org/wiki/Inertial_confinement_fusion)

, where simple hot gases continue to find new and surprising ways to foil our best attempts to trap them long enough to produce practical fusion energy.

In his post, Bookstaber (politely) dismisses as nonsense a

[New York Times article](http://www.nytimes.com/2010/08/01/weekinreview/01dash.html?_r=2&scp=2&sq=econophysics&st=cse)

about physics in finance (or so-called 'econophysics'). Along the way, the article notes that...

> Macroeconomists construct elegant theories to inform their understanding of crises. Econophysicists view markets as far more messy and complex — so much so that the beauty and logic of economic theory is a poor substitute. Drawing on the tools of the natural sciences, they believe that by sorting through an enormous amount of data, they can work backward to find the underlying dynamics of economic earthquakes and figure out how to prepare for the next one.
> 
> Financial crises are difficult to predict, the econophysicists say, because markets are not, as some traditional economists believe, efficient, self-regulating and self-correcting. The periodic upheavals are the result of a cascade of events and feedback loops, much like the tectonic rumblings beneath the Earth’s surface.

As long as one doesn't push metaphors too far, I can't see anything wrong with the above, and much that makes absolutely obvious good sense. No one working in this field thinks there's going to be a "theory of everything for finance". But we might well get a deeper understanding than we have today -- and not be so misled by silly slogans like the old efficient markets idea -- if we accept the presence of myriad instabilities in markets and begin modeling the important feed back loops and evolving systems in considerable detail.