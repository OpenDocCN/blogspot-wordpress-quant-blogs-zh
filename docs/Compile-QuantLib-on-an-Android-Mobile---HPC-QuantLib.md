<!--yml

category: 未分类

date: 2024-05-13 00:16:15

-->

# 在 Android 手机上编译 QuantLib – HPC-QuantLib

> 来源：[`hpcquantlib.wordpress.com/2018/08/19/compile-quantlib-on-an-android-mobile/#0001-01-01`](https://hpcquantlib.wordpress.com/2018/08/19/compile-quantlib-on-an-android-mobile/#0001-01-01)

[Termux](https://termux.com/) 是一款可以直接安装而不需要 root 的 Android 终端模拟器和 Linux 环境应用程序。它带有一个精简的 Linux 基本系统，之后可以安装额外的软件包。以下脚本在 Termux 会话中编译并运行 QuantLib。

```
pkg install clang autoconf automake libtool boost-dev nano git
git clone https://github.com/lballabio/quantlib.git
cd quantlib
./autogen.sh
./configure --disable-static CXXFLAGS='-O2' CXX='clang++'
make
./test-suite/quantlib-test-suite

```
