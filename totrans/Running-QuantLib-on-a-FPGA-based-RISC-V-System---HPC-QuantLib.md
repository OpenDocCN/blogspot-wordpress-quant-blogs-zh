<!--yml
category: 未分类
date: 2024-05-13 00:14:21
-->

# Running QuantLib on a FPGA based RISC-V System – HPC-QuantLib

> 来源：[https://hpcquantlib.wordpress.com/2019/10/31/running-quantlib-on-a-fpga-based-risc-v-system/#0001-01-01](https://hpcquantlib.wordpress.com/2019/10/31/running-quantlib-on-a-fpga-based-risc-v-system/#0001-01-01)

The RISC-V softcore [Rocket](http://lowrisc.org) runs on smaller FPGA development board like the NEXYS A7 and supports instruction set version RV64GC. Even though these are 64 bit cores they are only running at 25MHz. Hence we are better off cross compiling QuantLib on the host system. As expected quantlib-benchmark results are really low, around 2.4 MFlops.