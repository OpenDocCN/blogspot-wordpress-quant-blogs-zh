<!--yml

分类：未分类

日期：2024-05-13 00:14:21

-->

# 在基于 FPGA 的 RISC-V 系统上运行 QuantLib – HPC-QuantLib

> 来源：[`hpcquantlib.wordpress.com/2019/10/31/running-quantlib-on-a-fpga-based-risc-v-system/#0001-01-01`](https://hpcquantlib.wordpress.com/2019/10/31/running-quantlib-on-a-fpga-based-risc-v-system/#0001-01-01)

基于 RISC-V 的软核[Rocket](http://lowrisc.org)可以在较小的 FPGA 开发板上运行，如 NEXYS A7，并支持指令集版本 RV64GC。尽管这些是 64 位核心，但它们只能以 25MHz 的频率运行。因此，我们最好在主机系统上交叉编译 QuantLib。如预期所料，QuantLib 的基准测试结果非常低，大约为 2.4 MFlops。
