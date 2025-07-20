---
layout: post
title: Configure and Run PARSEC-2.1 Benchmark in Gem5
tags: GEM5 Benchmark Simulator

---

上一篇讲了怎样在linux系统里单独运行PARSEC Benchmark，本篇介绍如何在GEM5模拟器中配置和运行PARSEC Benchmark （以ARPHA架构方式为例）。PARSEC Benchmark需要在GEM5中的全系统（full system）模式下运行，其配置方法和上上篇中2.4节比较相似。相关教程可参考：[http://www.m5sim.org/PARSEC_benchmarks](http://www.m5sim.org/PARSEC_benchmarks) .

1. 首先新建一个文件夹用于存储PARSEC Benchmark的disk image

        mkdir full_system_images
        cd full_system_images

2. 下载初始的系统文件，并解压，再重命名文件夹（重命名可选）

        wget http://www.m5sim.org/dist/current/m5_system_2.0b3.tar.bz2
		tar jxvf m5_system_2.0b3.tar.bz2
	    mv m5_system_2.0b3 system
	
	解压后，文件的目录结构如下：
	    
		system/
            binaries/
                 console
                 ts_osfpal
                 vmlinux
            disks/
                 linux-bigswap2.img
                 linux-latest.img
				 
3. 下载PARSEC Benchmark相关文件，并替换掉system文件夹中的相应文件

    下载PARSEC对应的linux kernel文件，并替换掉 'system/binaries/vmlinux'
	    
		cd ./system/binaries/
	    wget http://www.cs.utexas.edu/~parsec_m5/vmlinux_2.6.27-gcc_4.3.4
	    rm vmlinux
		mv vmlinux_2.6.27-gcc_4.3.4 vmlinux
		
	下载PARSEC对应的PAL code文件， 并替换掉 'system/binaries/ts_osfpal'
	
	    wget http://www.cs.utexas.edu/~parsec_m5/tsb_osfpal
		rm ts_osfpal
		mv tsb_osfpal ts_osfpal
		
	下载PARSEC-2.1 Disk Image并解压
	
	    cd ../disks/
		wget http://www.cs.utexas.edu/~parsec_m5/linux-parsec-2-1-m5-with-test-inputs.img.bz2
		bzip2 -b linux-parsec-2-1-m5-with-test-inputs.img.bz2
		
4. 进入gem5文件夹，修改两个文件（SysPaths.py 和 Benckmarks.py）配置parsec的路径和文件名

     打开SysPaths.py配置parsec disk image的完整路径：
	
	    vim ./configs/common/SysPaths.py
	
	修改前：
	
        path = [ ’/dist/m5/system’, ’/n/poolfs/z/dist/m5/system’ ]
	
	修改后：
	
        path = [ ’/dist/m5/system’, ’/home/full_system_images/system’ ]
	
	打开Benchmarks.py，修改image文件名：
	
	    vim ./configs/common/Benchmarks.py
	
	修改前：
	
        elif buildEnv['TARGET_ISA'] == 'alpha':
            return env.get('LINUX_IMAGE', disk('linux-latest.img'))
			
	修改后：
	
        elif buildEnv['TARGET_ISA'] == 'alpha':
            return env.get('LINUX_IMAGE', disk('linux-parsec-2-1-m5-with-test-inputs.img'))
			
5. 生成benchmark的script文件，用于运行benchmark

    下载PARSEC script生成包，并解压：
	
	    wget http://www.cs.utexas.edu/~parsec_m5/TR-09-32-parsec-2.1-alpha-files.tar.gz
		tar zxvf TR-09-32-parsec-2.1-alpha-files.tar.gz
		
    生成script命令：
	
	    ./writescripts.pl <benchmark> <nthreads>
		
	有以下13种benchmark：
	
	    blackscholes
	    bodytrack
	    canneal
	    dedup
	    facesim
	    ferret
	    fluidanimate
	    freqmine
	    streamcluster
	    swaptions
	    vips
	    x264
	    rtview
		
6. 根据生成的script文件运行gem5：

        ./build/ALPHA/gem5.opt ./configs/example/fs.py -n <number> --script=./path/to/runScript.rcS --caches --l2cache -F 5000000000

7. 新开一个窗口，使用telnet与gem5模拟系统进行交互

        telnet localhost 3456  
        
