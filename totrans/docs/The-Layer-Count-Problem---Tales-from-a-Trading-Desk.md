<!--yml
category: 未分类
date: 2024-05-18 05:39:51
-->

# The Layer Count Problem | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2015/03/10/the-layer-count-problem/#0001-01-01](https://mdavey.wordpress.com/2015/03/10/the-layer-count-problem/#0001-01-01)

## The Layer Count Problem

Retina displays are always a good test these days for UI rendering performance issues – the influence of the GPU.  Below are a few relevant reading items

*   Improving the CSS performance of fixed position [elements](http://benfrain.com/improving-css-performance-fixed-position-elements/)
*   GPU Accelerated [Compositing](http://www.chromium.org/developers/design-documents/gpu-accelerated-compositing-in-chrome) in Chrome
*   Stick to compositor-only properties and manage [layer](https://developers.google.com/web/fundamentals/performance/rendering/stick-to-compositor-only-properties-and-manage-layer-count) count
*   Accelerated [Rendering](http://www.html5rocks.com/en/tutorials/speed/layers/) in Chrome

Think layer [optimisation](http://www.w3.org/TR/css-will-change-1/) using will-change: transform to avoid layer explosion from fixed positioning elements.

~ by mdavey on March 10, 2015.

Posted in [Uncategorized](https://mdavey.wordpress.com/category/uncategorized/)