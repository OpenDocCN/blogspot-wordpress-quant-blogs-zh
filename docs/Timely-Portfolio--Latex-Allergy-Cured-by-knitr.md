<!--yml

类别：未分类

日期：2024-05-18 15:07:48

-->

# 及时投资组合：Latex 过敏通过 knitr 治愈

> 来源：[`timelyportfolio.blogspot.com/2012/04/latex-allergy-cured-by-knitr.html#0001-01-01`](http://timelyportfolio.blogspot.com/2012/04/latex-allergy-cured-by-knitr.html#0001-01-01)

我一直知道在某个时刻我必须屈服于 Latex 的力量，但 Latex 对我来说一直非常令人畏惧。我终于找到了治愈我 Latex 过敏的灵丹妙药，那就是来自谢益辉的令人惊叹的[knitr 包](http://yihui.name/knitr/)。付出非常小的努力，我运行了我的第一个实验，现在我非常兴奋地将其纳入生产质量性能报告（我计划在未来的帖子中记录到达那里的步骤）。

对于那些在 Windows 上从头开始的人，我认为最简单的方法是[安装 LyX](http://wiki.lyx.org/Windows/Windows)，这将同时安装[MikTex](http://www.miktex.org/)。如果这些成功安装，那么你应该准备好使用 knitr 进行 R 实验。

我将使用 knitr 的 stich 函数，这显然不是为 knitr 的健壮生产使用而设计的，但非常适合非常简单的第一次测试。stitch 将打开一个非常短的脚本，应用一个模板，并生成一个 Sweave 风格的.Rnw 文件（可以更改）。knit2pdf 将.Rnw 文件转换为 pdf，你只需要几行代码就能得到[一个惊人的结果](http://www.box.com/shared/fdcc4483e733f9b00c44)。

<嵌入 src="http://www.box.com/嵌入/i2ho666gmcn6dt4.swf" wmode="不透明" 类型="应用程序/x-shockwave-flash" 允许全屏="真" 允许脚本访问="总是">

[R 代码来自 GIST（难以置信地只有 7 行）：](https://gist.github.com/2362469)
