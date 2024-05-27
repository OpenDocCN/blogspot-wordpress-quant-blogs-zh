<!--yml

分类：未分类

日期：2024-05-18 05:39:51

-->

# 层计数问题 | 交易桌上的故事

> 来源：[`mdavey.wordpress.com/2015/03/10/the-layer-count-problem/#0001-01-01`](https://mdavey.wordpress.com/2015/03/10/the-layer-count-problem/#0001-01-01)

## 层计数问题

如今，Retina 显示屏总是测试 UI 渲染性能问题的一个好工具——GPU 的影响。以下是几个相关阅读材料

+   优化固定位置[元素](http://benfrain.com/improving-css-performance-fixed-position-elements/)的 CSS 性能

+   Chrome 中的 GPU 加速[合成](http://www.chromium.org/developers/design-documents/gpu-accelerated-compositing-in-chrome)

+   坚持只使用合成器属性和管理[层](https://developers.google.com/web/fundamentals/performance/rendering/stick-to-compositor-only-properties-and-manage-layer-count)计数

+   Chrome 中的加速[渲染](http://www.html5rocks.com/en/tutorials/speed/layers/)

考虑使用`will-change: transform`进行层[优化](http://www.w3.org/TR/css-will-change-1/)，以避免固定定位元素导致的层爆炸。

~ mdavey 于 2015 年 3 月 10 日。

发布于[未分类](https://mdavey.wordpress.com/category/uncategorized/)
