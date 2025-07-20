---
layout: post
title: Install and Run GPGPU-Sim
tags: GPU Machine-Learning Simulator

---

[GPGPU-Sim](http://www.gpgpu-sim.org/) is a cycle-level simulator for modeling contemporary GPUs running CUDA and OpenCL workloads. The current GPGPU-Sim supports the GPU simulation with four kinds of architectures, i.e., GTX480, QuadroFX5600, QuadroFX5800, and TeslaC2050 architectures. 
This blog introduces the detailed steps to install and run GPGPU-Sim.

> #### 1 Download and Install NVDIA CUDA 4.0

GPGPU-Sim has to be run with NVDIA CUDA and does not support the CUDA versions larger than 4.0. Hence, we should first install NVDIA CUDA 4.0. The linux OS in my computer is Ubuntu 18.04, and the gcc version is 7.3.0. To install NVDIA CUDA 4.0, please do the following setps.

**1)** Download the [CUDA Toolkit for Ubuntu Linux 10.10](https://developer.nvidia.com/cuda-toolkit-40) and [GPU Computing SDK code samples](https://developer.nvidia.com/cuda-toolkit-40) from the NVDIA website.

**2)** Install CUDA Toolkit for Ubuntu Linux 10.10 first:    
  
    chmod +x cudatoolkit_4.0.17_linux_64_ubuntu10.10.run
    sudo ./cudatoolkit_4.0.17_linux_64_ubuntu10.10.run

The CUDA Toolkit has been installed in the path of `/usr/local/cuda` in default.

3) Add the path of CUDA Toolkit into the `~/.bashrc` file:

    echo 'export PATH=$PATH:/usr/local/cuda/bin' >> ~/.bashrc
	echo 'export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/lib:/usr/local/cuda/lib64' >> ~/.bashrc
	source ~/.bashrc
	
4) Install GPU Computing SDK code samples:

    chmod +x gpucomputingsdk_4.0.17_linux.run
    sudo ./gpucomputingsdk_4.0.17_linux.run

The GPU Computing SDK has been installed in the path of `~/NVIDIA_GPU_Computing_SDK` in default.	

5) Install gcc-4.4 and g++-4.4 (since CUDA 4.0 supports the gcc version until 4.4):

     apt-get install gcc-4.4 g++-4.4

If the error `package gcc-4.4 is not available, but is referred to by another package` occurs, do the following steps to address it:
    
    vim /etc/apt/sources.list
	
Add the two-line codes into the opened file:

    deb http://dk.archive.ubuntu.com/ubuntu/ trusty main universe    
    deb http://dk.archive.ubuntu.com/ubuntu/ trusty-updates main universe 
	
Then, update the apt source:

    apt-get update
	
By now, the gcc-4.4 and g++-4.4 have been installed.

6) Change the gcc/g++ in the system to gcc-4.4/g++4.4:

    sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-7 150
    sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.4 100
    sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-7 150
    sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-4.4 100
	
Select the 4.4 version by using `update-alternatives`:
    
	sudo update-alternatives --config gcc
	sudo update-alternatives --config g++

> #### 2 Download and Install GPGPU-Sim

1) Download GPGPU-Sim from GitHub

    git clone https://github.com/gpgpu-sim/gpgpu-sim_distribution.git

2) Install dependencies

    sudo apt-get install build-essential xutils-dev bison zlib1g-dev flex libglu1-mesa-dev
	sudo apt-get install doxygen graphviz
	sudo apt-get install python-pmw python-ply python-numpy libpng12-dev python-matplotlib
	sudo apt-get install libxi-dev libxmu-dev freeglut3-dev

3) Add the CUDA_INSTALL_PATH into the `~/.bashrc` file:

    echo 'export CUDA_INSTALL_PATH=/usr/local/cuda' >> ~/.bashrc
	source ~/.bashrc

4) Build GPGPU-Sim:

    make
	
During the building, if there is an error `cuobjdump.l:110: error: unterminated comment cuobjdump.l:108: error: expected declaration or statement at end of input`, remove the comments in cuobjdump.l:108-109.

5) Run GPGPU-Sim:

Copy the contents of a GPU config, e.g., `configs/GTX480/*`, to your application's working directory, and then run a CUDA application.

    mkdir test
	cd test/
	cp ../configs/GTX480/* ./
	
	