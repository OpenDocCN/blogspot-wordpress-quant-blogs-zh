<!--yml

类别：未分类

日期：2024-05-18 05:46:37

-->

# 协议缓冲区 – 向后兼容性 | 交易桌旁的故事

> 来源：[`mdavey.wordpress.com/2014/09/16/protocol-buffer-backward-compatibility/#0001-01-01`](https://mdavey.wordpress.com/2014/09/16/protocol-buffer-backward-compatibility/#0001-01-01)

## 协议缓冲区 – 向后兼容性

值得[记住](https://developers.google.com/protocol-buffers/docs/javatutorial)：

+   你不可以更改任何现有字段的标签编号。

+   你不可以添加或删除任何必填字段。

+   你可能需要删除可选的或重复的字段。

+   你可以添加新的可选或重复字段，但必须使用全新的标签编号（即在这个协议缓冲区中从未使用过的标签编号，即使是被删除的字段也没有使用过）。

~ mdavey 于 2014 年 9 月 16 日。

发布在 [未分类](https://mdavey.wordpress.com/category/uncategorized/)
