<!--yml

category: 未分类

date: 2024-05-17 23:41:11

-->

# GPU 上的多维有限差分方法 – HPC-QuantLib

> 来源：[`hpcquantlib.wordpress.com/2012/12/27/multi-dimensional-finite-difference-methods-on-a-gpu/#0001-01-01`](https://hpcquantlib.wordpress.com/2012/12/27/multi-dimensional-finite-difference-methods-on-a-gpu/#0001-01-01)

基于算子分裂的多维有限差分方法性能的一个关键方面是基础三对角系统求解器的性能 [1]。 [2] 中的作者分析了不同的求解器策略，并报告了在非常大的系统上最佳求解器策略（循环约简）的 GPU 和 CPU 之间约 15 倍的加速比。CUDA 的稀疏矩阵库 cuSPARSE 包含一个基于循环约简的求解三对角系统的例程。nVIDIA 声称与英特尔的 MKL 库相比，速度提高了约十倍 [3]。

这些因素小于纯蒙特卡洛定价算法报告的速度提高因素。主要原因是三对角系统求解器不能像许多蒙特卡洛定价算法那样通过简单的分治方法进行并行化。

Hundsdorfer-Verwer 算子分裂方案的 GPU 实现的主要类包括：

1.  **GPUFdmLinearOp**：实现 FdmLinearOp 接口，并可通过 *toMatrix()/toMatrixDecomp()* 方法从 FdmLinearOp/FdmLinearOpComposite 的任何实例初始化。

1.  **GPUTripleBandLinearOp**：TripleBandLinearOp 的基于 GPU 的实现。该线性算子可以通过 toMatrix/toMatrixDecomp() 方法从 FdmLinearOp/FdmLinearOpComposite 类的任何实例初始化。三对角系统的求解器基于 cuSPARSE。

1.  **GPUHundsdorferScheme**：基于 GPU 的 Hundsdorfer-Verwer 算子分裂方案的实现。

![plot](https://hpcquantlib.wordpress.com/2012/12/27/multi-dimensional-finite-difference-methods-on-a-gpu/plot-50/)

![plot](https://hpcquantlib.wordpress.com/2012/12/27/multi-dimensional-finite-difference-methods-on-a-gpu/plot-51/)代码可在此处获得 [here](http://hpc-quantlib.de/src/gpuopsplitting.zip)，它基于来自 [trunk](http://sourceforge.net/p/quantlib/code/HEAD/tree/) 的最新 [QuantLib](http://quantlib.org) 版本、[CUDA 4.1](https://developer.nvidia.com/category/zone/cuda-zone) 或更高版本以及 [Cusp 0.3](http://code.google.com/p/cusp-library/) 或更高版本。如上图所示，速度提升系数取决于问题的大小。只有在非常大的二维问题或中等大小的三维问题中才能实现超过十倍的速度提升因子。GPU 精度在 cudatypes.hpp 中通过对类型 “real” 的 typedef 定义。

[1] Karel in ’t Hout，《ADI finite difference schemes for the Heston model with correlation.》（http://win.ua.ac.be/%7Ekihout/ADI_Heston_lecture.pdf）

[2] 帕 ablo·奎萨达-巴里奥斯，朱利安·拉马斯-罗德里格斯，多拉·B·埃拉斯，蒙塞拉特·布尔，弗朗西斯科·阿古埃略，[选择最佳的三对角系统求解器——基于多核 CPU 和 GPU 平台。](http://weblidi.info.unlp.edu.ar/worldcomp2011-mirror/pdp8294.pdf)

[3] 英伟达，[cuSPARSE](https://developer.nvidia.com/cusparse)
