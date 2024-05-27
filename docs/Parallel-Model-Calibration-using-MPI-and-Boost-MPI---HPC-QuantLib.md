<!--yml

类别：未分类

日期：2024-05-17 23:41:36

-->

# 使用 MPI 和 Boost.MPI 的并行模型校准 – HPC-QuantLib

> 来源：[`hpcquantlib.wordpress.com/2012/04/09/parallel-model-calibration-using-mpi-and-boost-mpi/#0001-01-01`](https://hpcquantlib.wordpress.com/2012/04/09/parallel-model-calibration-using-mpi-and-boost-mpi/#0001-01-01)

消息传递标准[MPI](http://www.mpi-forum.org/)是一个语言无关的通信协议。MPI 支持在大型并行计算机和对称多处理器系统上并行化数值算法。MPI 是标准化的、高度可移植的，并且在大型并行超级计算机上是事实上的标准。尽管 MPI 可以在多线程环境中使用，但它通常在多进程环境中使用。因此，MPI 是为基于非线程安全的 QuantLib 算法量身定制的并行化工具。

MPI 规范的根源可以追溯到上世纪 90 年代初，如果你使用 C-API，你会感受到它的年代感，这个 API 是为了达到最大性能而设计的。Boost.MPI 库 – 从网页上引用 – “是一个对标准消息传递接口的 C++友好接口… Boost.MPI 可以使用 Boost.Serialization 库为用户定义的类型构建 MPI 数据类型”。

模型校准可能是一个非常耗时的任务，例如使用美式期权和离散股息对 Heston 或 Heston-Hull-White 模型进行校准。类 MPICalibrationHelper 作为给定 CalibrationHelper 的 MPI 包装器，允许对现有的模型校准例程进行并行化（希望影响/努力最小）。源代码可在[这里](http://hpc-quantlib.de/src/mpicalibrationhelper.zip)获得。它包含了 MPICalibrationHelper 类，作为一个例子，还有 DAXCalibration 测试用例的并行版本（位于 test-suite/hestonmodel.cpp 中）。该代码依赖于[QuantLib 1.0](http://quantlib.org)或更高版本，[Boost.Thread](http://www.boost.org/doc/libs/1_49_0/doc/html/thread.html)和[Boost.MPI](http://www.boost.org/doc/libs/1_49_0/doc/html/mpi.html)。

![图](https://hpcquantlib.wordpress.com/wp-content/uploads/2012/04/plot.png)上面的图表显示了使用有限差分定价引擎在八核机器上对离散股息的 Heston-Hull-White 校准的速度提升。子线性缩放的主要原因是在 CPU 和主内存之间的有限内存带宽，而不是 MPI 通信开销。
