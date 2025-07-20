---
layout: post
title: Install and Run ISPASS2009-benchmarks on GPGPU-Sim
tags: GPU Machine-Learning Benchmark

---

[ISPASS2009-Benchmarks](https://github.com/gpgpu-sim/ispass2009-benchmarks) are used in the ISPASS 2009 paper on GPGPU-Sim for evaluation. The benchmark suite includes 11 benchmarks, i.e., AES, BFS, CP, LPS, LIB, MUM, NN, NQU, RAY, STO, and WP. Please do the following steps to install and run ISPASS2009 Benchmarks.



> #### 1 Build the NVIDIA CUDA SDK benchmarks

1) Install NVIDIA driver if have no one:

    apt-get install nvidia-340
	
There may be some errors during the installing. That is all right.

2) We have installed the NVIDIA CUDA SDK benchmarks (i.e., GPU Computing SDK code samples) when installing GPGPU-Sim. We now build it:

    cd ~/NVIDIA_GPU_Computing_SDK
	make
	
During the building, if the error `/usr/bin/ld: cannot find -lOpenCL collect2: ld returned 1 exit status ../../common/common_opencl.mk:254: recipe for target '../../..//OpenCL//bin//linux/release/oclPostprocessGL' failed` occurs, make the following modifications:

&nbsp;&nbsp;&nbsp;&nbsp; (a) Edit `./C/common/common.mk`, lines like `LIB += … ${OPENGLLIB} …. $(RENDERCHECKGLLIB) …` should have `$(RENDERCHECKGLLIB)` moved before `${OPENGLLIB}`. There are 3 lines like this.
    
	LIB += $(RENDERCHECKGLLIB) ${OPENGLLIB} $(PARAMGLLIB) $(CUDPPLIB) ${LIB} -ldl -rdynamic
	LIB += -lcuda   $(RENDERCHECKGLLIB) ${OPENGLLIB} $(PARAMGLLIB) $(CUDPPLIB) ${LIB}
	LIB += $(RENDERCHECKGLLIB) ${OPENGLLIB} $(PARAMGLLIB) $(CUDPPLIB) ${LIB}


&nbsp;&nbsp;&nbsp;&nbsp; (b) Similarly, edit `./CUDALibraries/common/common.mk`

&nbsp;&nbsp;&nbsp;&nbsp; (c) `cd ~/NVIDIA_GPU_Computing_SDK`

&nbsp;&nbsp;&nbsp;&nbsp; (d) Edit `Makefile`. Comment all lines with `CUDALibraries` and `OpenCL` as we only want the application binaries. You comment by placing `#` in the front of the line.
    
	# GPU Computing SDK Version 4.0.8
    all:
        @$(MAKE) -C ./shared
        @$(MAKE) -C ./C
        #@$(MAKE) -C ./CUDALibraries
        #@$(MAKE) -C ./OpenCL

    clean:
        @$(MAKE) -C ./shared clean
        @$(MAKE) -C ./C clean
        #@$(MAKE) -C ./CUDALibraries clean
        #@$(MAKE) -C ./OpenCL clean

    clobber:
        @$(MAKE) -C ./shared clobber
        @$(MAKE) -C ./C clobber
        #@$(MAKE) -C ./CUDALibraries clobber
        #@$(MAKE) -C ./OpenCL clobber

    

&nbsp;&nbsp;&nbsp;&nbsp; (e) `make`

The NVIDIA CUDA SDK benchmarks have been installed by now. All executed files are listed in the fold `~/NVIDIA_GPU_Computing_SDK/C/bin/linux/release/`.

3) Test GPGPU-Sim using one of NVIDIA CUDA SDK benchmarks

    cd /home/gpgpu-sim_distribution/test
	~/NVIDIA_GPU_Computing_SDK/C/bin/linux/release/

> #### 2 Build the ISPASS2009-Benchmarks
	
1) Download ISPASS2009-Benchmarks

    cd /home/gpgpu-sim_distribution
	git clone https://github.com/gpgpu-sim/ispass2009-benchmarks.git
    cd ispass2009-benchmarks/
	
2) Define the following environment variables at the top of `Makefile.ispass-2009`:

    export CUDA_INSTALL_PATH=/usr/local/cuda
	NVIDIA_COMPUTE_SDK_LOCATION=/root/NVIDIA_GPU_Computing_SDK

3) Comment some benchmarks that fail to be built, e.g., AES, DG, and WP, in  `Makefile.ispass-2009`:

    #$(SETENV) make noinline=$(noinline) -C AES
	#$(SETENV) make noinline=$(noinline) -C DG/3rdParty/ParMetis-3.1
	#$(SETENV) make noinline=$(noinline) -C DG
	#$(SETENV) make noinline=$(noinline) -C WP

4) Build the benchmarks

    "make -f Makefile.ispass-2009
	
The binaries generated are in the `./bin/release/` fold.

5) Source setup_environment and Place a link to the GPU configuration files:

    cd /home/gpgpu-sim_distribution
	source setup_environment 
	cd ispass2009-benchmarks/
    ./setup_config.sh GTX480

You can also change the GPU type (e.g., to `TeslaC2050`) by the following instructions:

    ./setup_config.sh --cleanup
	./setup_config.sh TeslaC2050
	
6) Run a benchmark such as `NN`:

    cd NN/
	sh README.GPGPU-Sim
	

	