<!--yml

category: 未分类

日期：2024 年 5 月 18 日 06:36:57

-->

# OSX 上的 ZeroMQ + Java 绑定 | 一名交易台的故事

> 来源：[`mdavey.wordpress.com/2012/08/02/zeromq-java-bindings-on-osx/#0001-01-01`](https://mdavey.wordpress.com/2012/08/02/zeromq-java-bindings-on-osx/#0001-01-01)

## OSX 上的 ZeroMQ + Java 绑定

不久前，我进行了在 OSX 上构建 ZeroMQ 的乐趣体验。由于通常的 Google 帮助，这实际上并不是一次糟糕的经历。以下是给那些在追随的人的笔记：

+   从[这里](http://www.zeromq.org/area:download/)下载最新稳定版本

+   “在类 UNIX 系统上构建”通常对 OSX 来说是正确的，除了如果你在构建之前不执行“brew install pkg-config”，你将会遇到“换行标记”和 PKG_CHECK_MODULES 错误，如[stackoverflow](http://stackoverflow.com/questions/3522248/how-do-i-compile-jzmq-for-zeromq-on-osx)所述

+   如上所述安装 pkg-config 时，我发现我必须将 pkg.m4 文件复制到/usr/share/aclocal 和/usr/share/aclocal-1.10 中，因为我懒得检查使用了哪个 aclocal 😦

+   用“sudo make install”[完成](http://www.zeromq.org/area:download/)后，前往下载 ZeroMQ 的 Java[绑定](http://www.zeromq.org/bindings:java)

+   构建 Java 绑定是非常简单的，允许快速测试以验证一切是否正常在两个分离的终端运行以下内容：

> java -Djava.library.path=/usr/local/lib -classpath /usr/local/share/java/zmq.jar:../src/zmq.jar:zmq-perf.jar local_lat tcp://127.0.0.1:5555 1 100
> 
> java -Djava.library.path=/usr/local/lib -classpath /usr/local/share/java/zmq.jar:../src/zmq.jar:zmq-perf.jar remote_lat tcp://127.0.0.1:5555 1 100

现在是时候在一些家庭项目中利用 ZeroMQ 了 😉

~ 由 mdavey 于 2012 年 8 月 2 日发布。

Posted in [Java](https://mdavey.wordpress.com/category/languages/java/)

标签：[消息传递](https://mdavey.wordpress.com/tag/messaging/)
