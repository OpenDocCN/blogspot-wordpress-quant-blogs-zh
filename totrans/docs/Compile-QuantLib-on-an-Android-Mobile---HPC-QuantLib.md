<!--yml
category: 未分类
date: 2024-05-13 00:16:15
-->

# Compile QuantLib on an Android Mobile – HPC-QuantLib

> 来源：[https://hpcquantlib.wordpress.com/2018/08/19/compile-quantlib-on-an-android-mobile/#0001-01-01](https://hpcquantlib.wordpress.com/2018/08/19/compile-quantlib-on-an-android-mobile/#0001-01-01)

[Termux](https://termux.com/) is an Android terminal emulator and Linux environment app which can be installed directly w/o rooting. It comes with a minimal Linux base system and additional packages can be installed afterwards. The following script compiles and runs QuantLib in a Termux session

```
pkg install clang autoconf automake libtool boost-dev nano git
git clone https://github.com/lballabio/quantlib.git
cd quantlib
./autogen.sh
./configure --disable-static CXXFLAGS='-O2' CXX='clang++'
make
./test-suite/quantlib-test-suite

```