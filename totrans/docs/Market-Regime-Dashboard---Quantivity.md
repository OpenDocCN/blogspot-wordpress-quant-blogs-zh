<!--yml
category: 未分类
date: 2024-05-18 13:55:46
-->

# Market Regime Dashboard | Quantivity

> 来源：[https://quantivity.wordpress.com/2009/08/23/market-regime-dashboard/#0001-01-01](https://quantivity.wordpress.com/2009/08/23/market-regime-dashboard/#0001-01-01)

The [previous post](https://quantivity.wordpress.com/2009/08/16/naive-backtesting-is-bogus/), and excellent attendant reader comments, posited that effective quantitative trading needs to dynamically adapt to context. Yet, one of the most difficult systemic quant problems is *identifying relevant “context”, how to measure it, and how to visualize it*.

All too often, people focus exclusively on analyzing raw price charts for context ([technical analysis](http://en.wikipedia.org/wiki/Technical_analysis) is particular guilty). This is unfortunate, as basic time-series analysis offers to tickle out and visualize myriad richness otherwise invisible.

A series of four posts seek to build a “visual dashboard” for *market regime of a single instrument* (in pictures, as one is worth a 1000 words). For simplicity, each post focuses on SPY during 2007 – 2008 and explore both [time domain](http://en.wikipedia.org/wiki/Time-domain) and [frequency domain](http://en.wikipedia.org/wiki/Frequency_domain). The first two posts will focus on identifying regime structure in the time domain:

*   Raw structure: visualize distribution and moments
*   Correlation structure: visualize measures of self-correlation

The latter two posts will focus on identifying regime structure in the frequency domain:

*   Frequency structure: visualize stationary sinusoidal frequencies via [Fourier analysis](http://en.wikipedia.org/wiki/Fourier_analysis)
*   Wavelet structure: visualize non-stationary [wavelets](http://en.wikipedia.org/wiki/Wavelet_analysis)

For readers new to these techniques, they can be understood via analogy to appreciating orchestra. First, one must appreciate the progression and sequence of notes, as expressed by a sheet of music, played by each instrument; this is the time domain. Second, one must appreciate how to distinguish the [melodies](http://en.wikipedia.org/wiki/Melodies) and [harmonies](http://en.wikipedia.org/wiki/Harmonies) played by each instrument or group of instruments; this is the frequency domain. Both are important, each providing an [orthogonal](http://en.wikipedia.org/wiki/Orthogonality) (or [orthonormal](http://en.wikipedia.org/wiki/Orthonormal)) perspective on the same phenomenon.

This dashboard strives to provide basic visualizations which can capture the regime of many instruments, as applicable to both trading and risk management.