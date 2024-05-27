<!--yml

类别：未分类

日期：2024 年 05 月 12 日 19:32:32

-->

# YieldCurveBootstrapping _BLOCK_TYPE_IS_VALID in SpreadServe | Coding the markets

> 来源：[`etrading.wordpress.com/2014/12/18/yieldcurvebootstrapping-_block_type_is_valid-in-spreadserve/#0001-01-01`](https://etrading.wordpress.com/2014/12/18/yieldcurvebootstrapping-_block_type_is_valid-in-spreadserve/#0001-01-01)

## YieldCurveBootstrapping _BLOCK_TYPE_IS_VALID 在 SpreadServe 中

### 2014 年 12 月 18 日

老话说得好，昨天我花了太多时间在一个经典的 Windows bug 上撞头了。我正在测试 [SpreadServeEngine](http://spreadserve.com/product/user-guide/) 处理 XLL 供应的函数嵌套调用的优化。我使用的是 [QuantLib](http://quantlib.org/index.shtml) 的 YieldCurveBootstrapping 电子表格和 QuantLib 1.4.0 的 XLL addin。该表格调用了 [qlPiecewiseYieldCurve](http://www.bnikolic.co.uk/ql/addindoc/f/qlPiecewiseYieldCurve.html) 函数，并且第四个参数 RateHelpers 是由 ohPack 的调用提供的。通常在这种情况下，ohPack 返回的 XLOPER 会被编组到引擎的内部表示中，然后再被编组回一个 XLOPER 以便传递给 qlPiecewiseYieldCurve。我添加了一个快捷方式，使得 XLOPER 和内部表示都可用，因此如果可能的话，编组过程可以通过快捷方式进行。不知不觉中，我在一个 DLL 中新建了一个对象，当 qlPiecewiseYieldCurve 返回并释放了其堆栈帧时，另一个 DLL 释放了它。我的调试版本在 _BLOCK_TYPE_IS_VALID 上抛出了运行时断言。于是我开始了一场病毒猎手般的搜索，通过代码库寻找双重删除或缓冲区溢出。电子表格引擎是复杂的生物，因为它们基本上是一个函数式编程语言的运行时，所以必须维护一个对象图，并在节点上以命令方式分发令牌化的代码和 XLL 提供的 C/C++ 函数。在所有这些过程中都需要进行大量的内存池和堆栈管理！所以我确信，在我优化了嵌套 XLL 函数边缘情况后，某处暴露了一个微妙的内存管理错误。当我在寻找错误时，我确实对 Windows 堆调试进行了一些好的阅读：[这个](http://msdn.microsoft.com/en-us/library/bebs9zyz%28v=vs.90%29.aspx) 和 [这个](http://msdn.microsoft.com/en-us/library/ms235460.aspx) 是推荐的。在调试时，很容易不断地深入追求一个被认为是微妙的错误。最好停下来喘口气，尝试拓宽自己的视野。正是这篇文章让我再次思考到每个 DLL 都有自己的 C 运行时链接，如果它们的内存管理实现不同，就会有问题。在这种情况下就是这样。向负责释放对象的 DLL 添加一个静态分配器函数，确保新建和删除由同一个 DLL 完成，引导模型顺利运行。当然，现在我需要重新审视我的构建系统的链接模型，并确保所有的 DLL 和 EXE 都链接到相同的 CRT 实现...
