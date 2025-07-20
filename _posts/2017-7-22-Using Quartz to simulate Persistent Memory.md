---
layout: post
title: Using Quartz to Simulate Persistent Memory
tags: NVM Simulator

---

前几篇博客介绍的[NVMain](http://wiki.nvmain.org/)是一个体系结构级的非易失内存模拟器，主要是提供给体系结构方面的研究者使用。关于NVM硬件级研究可以使用NVMain，如NVM内存的写策略、磨损均衡策略、内存控制器设计等。由于需要模拟NVM硬件级的特征，包括时序、能耗、写耐久性等，在NVMain模拟器的运行负载的速度远小于在真实DRAM系统上运行的速度。

然而系统软件方面的研究者主要关注系统软件在NVM系统中的性能（延时/吞吐量）并不需要对NVM的硬件机制做更改。NVMain这类体系结构级模拟器中大部分功能，系统软件方面的研究都用不上，而且由于运行速度问题也不能运行大规模的负载。因此，惠普（Hewlett Packard）公司为系统软件方面的研究者开发了一款轻量级的基于DRAM的NVM模拟器，[Quartz](https://github.com/HewlettPackard/quartz)。在Quartz模拟器上的运行负载的速度可实现接近于在真实DRAM系统上运行的速度。Quartz只支持三种CPU架构包括Sandy Bridge, Ivy Bridge, 和Haswell（注意其它架构类型的CPU使用不了Quartz）。下面介绍Quartz的用法：



> #### 1 下载和安装Quartz

Quartz的代码已开源在GitHub上，可以直接下载：

    git clone https://github.com/HewlettPackard/quartz.git
	
Quartz的安装需要一些依赖库，可以运行其提供的`install.sh`文件自动安装所有的依赖库：

    sudo scripts/install.sh
	
使用以下命令编译Quartz源代码：

    mkdir build
    cd build
    cmake ..
    make clean all

编译好后，可以看到在`./build/lib/`路径下生成了一个动态库文件`libnvmemul.so`。	

> #### 2 运行Quartz

首先load模拟器核心模块，在Quartz根目录运行如下命令：
    
    sudo scripts/setupdev.sh load
	
设置CPU运行在最大频率：

    echo performance | sudo tee /sys/devices/system/cpu/cpu*/cpufreq/scaling_governor
	
如果机器的Linux内核版本号大于或等于4.0需要运行如下命令：

    echo 2 | sudo tee /sys/devices/cpu/rdpmc
	
运行自己的程序：

    scripts/runenv.sh <your_app>
    
> #### 2 模拟NVM延迟

Quartz目前的版本不能同时模拟NVM的延迟和带宽。只能让带宽不变模拟不同的延迟，或让延迟不变模拟不同的带宽。模拟带宽我们一般用不到，这里主要介绍怎样模拟NVM延迟。

模拟读延迟：NVM的读延迟可以直接在根目录下的`./nvmemul.ini`文件中配置（里面的写延时配置好像并没有用）：

    read = 200;

模拟写延迟：Quartz目前的版本不能支持对写延迟的模拟，所以我们需要自己实现写延迟模拟。由于NVM一般作为持久化内存（Persistent Memory），所以CPU对NVM的写都需要使用CLFLUSH指令（cache line flush）把CPU cache中的脏数据刷回NVM中，并使用MFENCE指令（memory fence）保证cache line flush的顺序性。为了模拟NVM写延迟，我们在每个CLFLUSH指令后面植入额外的延迟。

MFENCE和CLFLUSH指令后植入延迟的实现代码可参照`./quartz-master/src/lib/`路径下的`pflush.c`文件。

> #### 3 编写基于Persistent Memory的程序	

基于Persistent Memory的程序中，内存的分配和回收一定要用Quartz中对于的函数`pmalloc`和`pfree`。所以程序中需要引用头文件`./quartz-master/src/lib/pmalloc.h`，并且编译时需要链接`libnvmemul.so`动态库。

对Persistent Memory的写需要使用CLFLUSH指令刷回NVM中，并且使用MFENCE指令保证多个CLFLUSH指令执行的顺序性。

对于大于原子写（一般是8 bytes）的数据需要进一步使用logging或copy-on-write(CoW)来保证一致性。


	