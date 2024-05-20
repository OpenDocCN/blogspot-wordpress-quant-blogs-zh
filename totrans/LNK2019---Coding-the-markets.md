<!--yml
category: 未分类
date: 2024-05-12 19:35:51
-->

# LNK2019 | Coding the markets

> 来源：[https://etrading.wordpress.com/2011/01/30/lnk2019/#0001-01-01](https://etrading.wordpress.com/2011/01/30/lnk2019/#0001-01-01)

## LNK2019

### January 30, 2011

Every C++ dev gets bitten by unresolved symbols in their builds from time to time. You can stare at code for hours, sure that your library is defining a symbol. I just cracked one of these. Three methods in a lib were showing as unresolved when I built the exe. This [stackoverflow entry](http://stackoverflow.com/questions/261377/lnk2001-error-when-compiling-apps-referencing-stlport-5-1-4-with-vc-2008) was helpful, especially Raymond Chen’s blog entry which put me onto the undname utility. I’ve known about dumpbin for years, but undname was new to me. The problem turned out to be that one of my libs was built without the STLport headers on the include path. Visual Studio silently picks up its own STL. Then the linker complains it can’t resolve methods that return an std::string. The unresolved refs all had stlp_ in the signatures. Of course, I couldn’t see that until I compared methods defined in the lib using dumpbin /linkmembers:2 and undname with those unresolved by the linker.