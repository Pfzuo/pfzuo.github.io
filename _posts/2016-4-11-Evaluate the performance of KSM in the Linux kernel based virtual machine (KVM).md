---
layout: post
title: Evaluate the Performance of KSM in the Linux Kernel-based Virtual Machine (KVM)
tags: Deduplication 

---

### 安装KVM
---




1. 首先查看主机CPU的虚拟化支持:
        
    `$ egrep -o '(vmx|svm)' /proc/cpuinfo`

    如果显示如下,则表示该主机CPU支持虚拟化

        zuo@zuo:~$ egrep -o '(vmx|svm)' /proc/cpuinfo   
        vmx   
        vmx   
        vmx   
        vmx   
        zuo@zuo:~$   

2. 安装KVM软件包：virt-manager为GUI管理窗口，bridge-utils:用于网络桥接

    `$ apt-get install qemu-kvm libvirt-bin virt-manager bridge-utils`

3. 检查KVM是否安装成功

    方法1：
    
    `$ lsmod | grep kvm`
    
    如果显示如下信息，则表示KVM安装成功
    
        zuo@zuo:~$ lsmod | grep kvm   
        kvm_intel             143630  0    
        kvm                   452096  1 kvm_intel   
        zuo@zuo:~$    
    
    方法2：
    
    `$ virsh -c qemu:///system list`
    
    如果显示如下信息，则表示KVM安装成功
    
        zuo@zuo:~$ virsh -c qemu:///system list   
        Id    Name                           State   
        ----------------------------------------------------   
        zuo@zuo:~$    

4. 比较容易被忽视的一点是：开机前，进入BIOS中，开启CPU虚拟化支持

        Intel(R) Virtualization Technology (Enabled)
 
### 运行KVM
---

1. 终端中输入如下指令，打开virtual machine manager

    `$ sudo virt-manager`

   这时会弹出virtual machine manager的界面
     
2. 创建虚拟机前，需要下载一个操作系统的镜像文件（.iso）,用于安装虚拟机的操作系统;   
   点击virtual machine manager界面上的“create a new virtual machine”按钮，就可以开始创建虚拟机了（如下图所示）:
   
   ![image](https://pfzuo.github.io/images/createVM.png)


### 运行KSM
---

1. KSM需要在root权限下运行，所以首先获取root权限：

    `# su root`
    
        zuo@zuo:~$ su root   
        Password:   
        root@zuo:/home/zuo#    

2. KSM进程由'/sys/kernel/mm/ksm/'路径中的文件控制，我们可以查看KSM的运行状态：
    
    `# grep -H '' /sys/kernel/mm/ksm/*`
    
    结果如下：
    
        root@zuo:/home/zuo# grep -H '' /sys/kernel/mm/ksm/*
        /sys/kernel/mm/ksm/full_scans:0
        /sys/kernel/mm/ksm/merge_across_nodes:1
        /sys/kernel/mm/ksm/pages_shared:0
        /sys/kernel/mm/ksm/pages_sharing:0
        /sys/kernel/mm/ksm/pages_to_scan:100
        /sys/kernel/mm/ksm/pages_unshared:0
        /sys/kernel/mm/ksm/pages_volatile:0
        /sys/kernel/mm/ksm/run:0
        /sys/kernel/mm/ksm/sleep_millisecs:200
        root@zuo:/home/zuo# 
     
     其中每个参数的含义可参照 [https://www.kernel.org/doc/Documentation/vm/ksm.txt](https://www.kernel.org/doc/Documentation/vm/ksm.txt)

3. 开启KSM进程：
    
    `# echo 1 > /sys/kernel/mm/ksm/run`
    

### 虚拟机内存去重测试全过程
---

1. 首先用KVM创建了3个相同的Linux虚拟机(系统：Ubuntu-12.04 32位, 内存：1GB，硬盘空间：8GB);

2. 只开启一个虚拟机，查看内存去重情况

    ![image](https://pfzuo.github.io/images/oneVM.png)
    
     KSM开始合并相同内存页，3次full scan后（约10分钟），内存去重结果如下：
     
        root@zuo:/home/zuo# grep -H '' /sys/kernel/mm/ksm/*
        /sys/kernel/mm/ksm/full_scans:4
        sys/kernel/mm/ksm/merge_across_nodes:1
        /sys/kernel/mm/ksm/pages_shared:3633
        /sys/kernel/mm/ksm/pages_sharing:26033
        /sys/kernel/mm/ksm/pages_to_scan:100
        /sys/kernel/mm/ksm/pages_unshared:109842
        /sys/kernel/mm/ksm/pages_volatile:25486
        /sys/kernel/mm/ksm/run:1
        /sys/kernel/mm/ksm/sleep_millisecs:200
        
    第4次full scan后（约6分钟），内存相对稳定，内存去重结果如下：
    
        root@zuo:/home/zuo# grep -H '' /sys/kernel/mm/ksm/*
        /sys/kernel/mm/ksm/full_scans:5
        /sys/kernel/mm/ksm/merge_across_nodes:1
        /sys/kernel/mm/ksm/pages_shared:10446
        /sys/kernel/mm/ksm/pages_sharing:41652
        /sys/kernel/mm/ksm/pages_to_scan:100
        /sys/kernel/mm/ksm/pages_unshared:112580
        /sys/kernel/mm/ksm/pages_volatile:5436
        /sys/kernel/mm/ksm/run:1
        /sys/kernel/mm/ksm/sleep_millisecs:200
  


3. 开启第二个虚拟机（此时两个虚拟机同时运行），查看内存去重情况

    ![image](https://pfzuo.github.io/images/twoVMs.png)
    
    查看此时的内存去重结果：
    
        root@zuo:/home/zuo# grep -H '' /sys/kernel/mm/ksm/*
        /sys/kernel/mm/ksm/full_scans:5
        /sys/kernel/mm/ksm/merge_across_nodes:1
        /sys/kernel/mm/ksm/pages_shared:11512
        /sys/kernel/mm/ksm/pages_sharing:42692
        /sys/kernel/mm/ksm/pages_to_scan:100
        /sys/kernel/mm/ksm/pages_unshared:112405
        /sys/kernel/mm/ksm/pages_volatile:3505
        /sys/kernel/mm/ksm/run:1
        /sys/kernel/mm/ksm/sleep_millisecs:200
    
    可见新开启的虚拟机的内存页还没计入KSM，在下一次full scan时，才会计入;
    
    一次full scan后（约10分钟），内存去重结果：
    
        root@zuo:/home/zuo# grep -H '' /sys/kernel/mm/ksm/*
        /sys/kernel/mm/ksm/full_scans:7
        /sys/kernel/mm/ksm/merge_across_nodes:1
        /sys/kernel/mm/ksm/pages_shared:12135
        /sys/kernel/mm/ksm/pages_sharing:84749
        /sys/kernel/mm/ksm/pages_to_scan:100
        /sys/kernel/mm/ksm/pages_unshared:122351
        /sys/kernel/mm/ksm/pages_volatile:136353
        /sys/kernel/mm/ksm/run:1
        /sys/kernel/mm/ksm/sleep_millisecs:200

    第二次full scan后（约10分钟），内存去重结果：
    
        root@zuo:/home/zuo# grep -H '' /sys/kernel/mm/ksm/*
        /sys/kernel/mm/ksm/full_scans:8
        /sys/kernel/mm/ksm/merge_across_nodes:1
        /sys/kernel/mm/ksm/pages_shared:57047
        /sys/kernel/mm/ksm/pages_sharing:133770
        /sys/kernel/mm/ksm/pages_to_scan:100
        /sys/kernel/mm/ksm/pages_unshared:155843
        /sys/kernel/mm/ksm/pages_volatile:8928
        /sys/kernel/mm/ksm/run:1
        /sys/kernel/mm/ksm/sleep_millisecs:200

    第三次full scan后（约13分钟），内存相对稳定，内存去重结果：
    
        root@zuo:/home/zuo# grep -H '' /sys/kernel/mm/ksm/*
        /sys/kernel/mm/ksm/full_scans:9
        /sys/kernel/mm/ksm/merge_across_nodes:1
        /sys/kernel/mm/ksm/pages_shared:80047
        /sys/kernel/mm/ksm/pages_sharing:159071
        /sys/kernel/mm/ksm/pages_to_scan:100
        /sys/kernel/mm/ksm/pages_unshared:113814
        /sys/kernel/mm/ksm/pages_volatile:3680
        /sys/kernel/mm/ksm/run:1
        /sys/kernel/mm/ksm/sleep_millisecs:200
    

    
4. 开启第三个虚拟机（此时三个虚拟机同时运行），查看内存去重情况

    ![image](https://pfzuo.github.io/images/threeVMs.png)

    第一次full scan过程中，前6分钟pages_sharing和pages_volatile数目在增加，pages_shared和pages_unshared数目几乎没变
    
    第六分钟：
    
        root@zuo:/home/zuo# grep -H '' /sys/kernel/mm/ksm/*
        /sys/kernel/mm/ksm/full_scans:10
        /sys/kernel/mm/ksm/merge_across_nodes:1
        /sys/kernel/mm/ksm/pages_shared:81335
        /sys/kernel/mm/ksm/pages_sharing:263226
        /sys/kernel/mm/ksm/pages_to_scan:100
        /sys/kernel/mm/ksm/pages_unshared:111860
        /sys/kernel/mm/ksm/pages_volatile:72891
        /sys/kernel/mm/ksm/run:1
        /sys/kernel/mm/ksm/sleep_millisecs:200

    第一次full scan完成后（约17分钟），内存去重结果：
    
        root@zuo:/home/zuo# grep -H '' /sys/kernel/mm/ksm/*
        /sys/kernel/mm/ksm/full_scans:11
        /sys/kernel/mm/ksm/merge_across_nodes:1
        /sys/kernel/mm/ksm/pages_shared:81414
        /sys/kernel/mm/ksm/pages_sharing:269549
        /sys/kernel/mm/ksm/pages_to_scan:100
        /sys/kernel/mm/ksm/pages_unshared:111442
        /sys/kernel/mm/ksm/pages_volatile:77609
        /sys/kernel/mm/ksm/run:1
        /sys/kernel/mm/ksm/sleep_millisecs:200

    第二次full scan过程中，刚开始page_volatitle增加了约4万，然后开始减少：
    
        root@zuo:/home/zuo# grep -H '' /sys/kernel/mm/ksm/*
        /sys/kernel/mm/ksm/full_scans:11
        /sys/kernel/mm/ksm/merge_across_nodes:1
        /sys/kernel/mm/ksm/pages_shared:81413
        /sys/kernel/mm/ksm/pages_sharing:278134
        /sys/kernel/mm/ksm/pages_to_scan:100
        /sys/kernel/mm/ksm/pages_unshared:111442
        /sys/kernel/mm/ksm/pages_volatile:118125
        /sys/kernel/mm/ksm/run:1
        /sys/kernel/mm/ksm/sleep_millisecs:200

    
    第二次full scan完成后（约20分钟），内存相对稳定，内存去重结果：
    
        root@zuo:/home/zuo# grep -H '' /sys/kernel/mm/ksm/*
        /sys/kernel/mm/ksm/full_scans:12
        /sys/kernel/mm/ksm/merge_across_nodes:1
        /sys/kernel/mm/ksm/pages_shared:85499
        /sys/kernel/mm/ksm/pages_sharing:278616
        /sys/kernel/mm/ksm/pages_to_scan:100
        /sys/kernel/mm/ksm/pages_unshared:171862
        /sys/kernel/mm/ksm/pages_volatile:53213
        /sys/kernel/mm/ksm/run:1
        /sys/kernel/mm/ksm/sleep_millisecs:200
        
    第三次full scan完成后（约20分钟），内存稳定，内存去重结果：
    
        root@zuo:/home/zuo# grep -H '' /sys/kernel/mm/ksm/*
        /sys/kernel/mm/ksm/full_scans:13
        /sys/kernel/mm/ksm/merge_across_nodes:1
        /sys/kernel/mm/ksm/pages_shared:100562
        /sys/kernel/mm/ksm/pages_sharing:293995
        /sys/kernel/mm/ksm/pages_to_scan:100
        /sys/kernel/mm/ksm/pages_unshared:189267
        /sys/kernel/mm/ksm/pages_volatile:5366
        /sys/kernel/mm/ksm/run:1
        /sys/kernel/mm/ksm/sleep_millisecs:200

5. 关闭第三个虚拟机后：

        root@zuo:/home/zuo# grep -H '' /sys/kernel/mm/ksm/*
        /sys/kernel/mm/ksm/full_scans:15
        /sys/kernel/mm/ksm/merge_across_nodes:1
        /sys/kernel/mm/ksm/pages_shared:100155
        /sys/kernel/mm/ksm/pages_sharing:159629
        /sys/kernel/mm/ksm/pages_to_scan:100
        /sys/kernel/mm/ksm/pages_unshared:79381
        /sys/kernel/mm/ksm/pages_volatile:17447
        /sys/kernel/mm/ksm/run:1
        /sys/kernel/mm/ksm/sleep_millisecs:200

6. 关闭第二个虚拟机后：

        root@zuo:/home/zuo# grep -H '' /sys/kernel/mm/ksm/*
        /sys/kernel/mm/ksm/full_scans:16
        /sys/kernel/mm/ksm/merge_across_nodes:1
        /sys/kernel/mm/ksm/pages_shared:77934
        /sys/kernel/mm/ksm/pages_sharing:43155
        /sys/kernel/mm/ksm/pages_to_scan:100
        /sys/kernel/mm/ksm/pages_unshared:48300
        /sys/kernel/mm/ksm/pages_volatile:1237
        /sys/kernel/mm/ksm/run:1
        /sys/kernel/mm/ksm/sleep_millisecs:200

7. 关闭第一个虚拟机后：

        root@zuo:/home/zuo# grep -H '' /sys/kernel/mm/ksm/*
        /sys/kernel/mm/ksm/full_scans:17
        /sys/kernel/mm/ksm/merge_across_nodes:1
        /sys/kernel/mm/ksm/pages_shared:0
        /sys/kernel/mm/ksm/pages_sharing:0
        /sys/kernel/mm/ksm/pages_to_scan:100
        /sys/kernel/mm/ksm/pages_unshared:0
        /sys/kernel/mm/ksm/pages_volatile:0
        /sys/kernel/mm/ksm/run:1
        /sys/kernel/mm/ksm/sleep_millisecs:200


### 虚拟机内存去重结果分析
---

1. 内存去重率

    * 一个虚拟机单独运行的情况：   
    
        | pages_shared | pages_sharing | pages_unshared | pages_volatile |
        | :-----------:|:-------------:| :-------------:| :-------------:|
        | 10446        | 41652         | 112580         | 5436           |
    
        总内存页数： 10446 + 41652 + 112580 + 5436 = 170114    
        去重率： 41652/170114 × 100% = 24.5%    
        （可见单个虚拟机的内存冗余也是蛮多的）
    
    * 两个虚拟机同时运行的情况：   
    
         | pages_shared | pages_sharing | pages_unshared | pages_volatile |
         | :-----------:|:-------------:| :-------------:| :-------------:|
         | 80047        | 159071        | 113814         | 3680           |   
    
         总内存页数： 80047 + 159071 + 113814 + 3680 = 356612   
         总去重率： 159071/356612 × 100% = 44.6%     
         单个虚拟机内重复的页数约为： 41652 × 2 = 83304    
         两个虚拟机间重复的页数约为： 159071 - 83304 = 75747   
         两个虚拟机间的去重率约为： 75747/356612 × 100% = 21.2%   
    
    * 三个虚拟机同时运行的情况：   
    
         | pages_shared | pages_sharing | pages_unshared | pages_volatile |
         | :-----------:|:-------------:| :-------------:| :-------------:|
         | 100562       | 293995        | 189267         | 5366           |  
     
         总内存页数： 100562 + 293995 + 189267 + 5366 = 589190   
         总去重率： 293995/589190 × 100% = 49.9%    
         单个虚拟机内重复的页数约为： 41652 × 3 = 124956    
         三个虚拟机间重复的页数约为： 293995 - 124956 = 169039   
         三个虚拟机间的去重率约为： 169039/589190 × 100% = 28.7%   
 
2. CPU占用

   测试过程中，观测到KSM进程的CPU占用一直处于0.3%～0.7%间;
    
3. 一些发现

    * 前几次full scan中，每次full scan后pages_sharing数会大幅度增加，一个主要原因是： 内存逐渐趋于稳定，pages_volatile的页慢慢变少，有些merge到了stable tree中;    
    * 新开启的虚拟机产生的内存页，在下一轮full scan时，才被KSMD处理;   
    * 关闭一个虚拟机后，stable tree中的内存页，有些会成为unshared，但不会从stable tree中删掉（上一章第6步）;   
    * 测试过程中，同一轮full scan内可以观测到，某段时间pages_sharing数一直在增加，某段时间pages_sharing数一直趋于稳定，可见重复内存页具有一定的局部性;   











