<!--yml

category: 未分类

date: 2024-05-12 19:29:58

-->

# SpreadServe AMI 第三部分 | 编码市场

> 来源：[`etrading.wordpress.com/2017/03/06/spreadserve-ami-part-iii/#0001-01-01`](https://etrading.wordpress.com/2017/03/06/spreadserve-ami-part-iii/#0001-01-01)

## SpreadServe AMI 第三部分

### March 6, 2017

美国西部俄勒冈地区的 SpreadServe 0.4.2b AMI 现在可用：只需在公共镜像中搜索 SpreadServe。现在有一个 YouTube 视频介绍了如何启动一个 SpreadServe AMI。

[`www.youtube.com/embed/1e5ffwtl-QA?version=3&rel=1&showsearch=0&showinfo=1&iv_load_policy=1&fs=1&hl=en&autohide=2&wmode=transparent`](https://www.youtube.com/embed/1e5ffwtl-QA?version=3&rel=1&showsearch=0&showinfo=1&iv_load_policy=1&fs=1&hl=en&autohide=2&wmode=transparent)

VIDEO

在准备 AMI 时出现了两个有趣的问题：管理员密码持久性以及 AMI 的区域绑定性质。[这篇 2013 年的博客](http://technotes.khitrenovich.com/notes-creation-windows-ami-ec2/)表明管理员密码在 AMI 中不持久，但我发现它们现在确实如此。因此，SpreadServe 0.4.2b AMI 的管理员密码是 SpreadServe042b。如果您使用 AMI 启动自己的 SpreadServe 实例，我建议您更改密码！

请注意，SpreadServe 0.4.2b AMI 仅发布在美国西部俄勒冈地区。只有 AMI 所有者才能将其复制到其他地区，因此如果您想在其他地区拥有一个 SpreadServe AMI，您需要做一个简单的绕过：在美国西部俄勒冈启动一个镜像，停止它并创建您自己的镜像，然后[将其复制到您选择的地区](https://aws.amazon.com/premiumsupport/knowledge-center/copy-ami-region/)。
