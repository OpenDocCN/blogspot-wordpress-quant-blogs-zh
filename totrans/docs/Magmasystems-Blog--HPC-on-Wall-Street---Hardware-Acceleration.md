<!--yml
category: 未分类
date: 2024-05-18 05:12:08
-->

# Magmasystems Blog: HPC on Wall Street - Hardware Acceleration

> 来源：[http://magmasystems.blogspot.com/2007/02/hpc-on-wall-street-hardware.html#0001-01-01](http://magmasystems.blogspot.com/2007/02/hpc-on-wall-street-hardware.html#0001-01-01)

Sam Brown of the University of Utah just came out with

[some slides](http://www.chpc.utah.edu/hybrid_computing/talks/sam_brown_talk.ppt)

on his initial forays into hardware acceleration. He contrasts the use of Cell Processors,

FPGAs

, and

Multi

-core processors. He was trying to speed up 2-Way Wave Equation Modeling, which is not a financial application, but the lessons that he learned can be applied to those of use who are doing (or exploring)

HPC

in Wall Street.

The big effort is in unrolling loops and

parallelizing

your code. Using the

POSIX PThread API

and

multi

-core

cpus

is the easiest thing to do. With 4 threads (2 dual-core 2.2

Ghz Opterons

, 4 GB RAM), he got a 11x improvement on one set of benchmarks, and a 2x improvement on the big application.

The

FPGA

system used the

Altera Stratix

II

FPGA

. He got about a 14x

improvement

on the initial set of benchmarks, but the development effort was a lot harder. It took 12 hours to get the design onto the

FPGA

chip.

The Cell systems were a Sony

Playstation

3 (!!!) and a IBM Cell Blade with 2 Cell Processors with 8

SPEs

each (a Cell processor has 8

SPEs

, which function as coprocessors.) The Cell results were generally disappointing, with the author wondering if he programmed the Cell correctly. One thing that I have heard about the Cell is that it is very difficult to program. Perhaps companies like

PeakStream

can help you with this effort.

(For instant gratification, the money shots are slides 28, 29, and 30)

What can hardware acceleration do for you? Faster pricing of derivatives. Faster generation of risk values, especially for exotics. Better overnight stressing.

The problem is in acquiring the

skill set

to

parallelize

algorithms, deal with the development environments (especially debugging), learning new variants of C, and getting buy-in from the business.

©2007 Marc Adler - All Rights Reserved