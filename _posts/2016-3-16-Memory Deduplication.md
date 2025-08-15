---
layout: post
title: Memory Deduplication
tags: Deduplication
date: 2016-03-16

---

> #### 1 Memory Deduplication

Memory deduplication aims to save memory space in RAM by identifying and merging the identical memory pages. Red Hat proposed the KSM (Kernel Shared Memory or Kernel Same-page Merging)[^KSM] technique to implement memory deduplication in Linux kernel. KSM has merged into Linux kernel since the version 2.6.32 in 2009[^Linux2632]. VMware also proposed a technique called TPS (Transparent Page Sharing)[^TPS] in its product ESXi for memory deduplication. Some literatures claims that KSM may be more efficient than TPS. However, I have not found any work comparing them in real experiments.


#### 1.1 KSM 

KSM leverages two red-black trees[^rb-tree] to manage the memory pages, i.e., a stable tree and an unstable tree. There are three page states for each page in the host, i.e., frequently modified, sharing candidate yet not frequently modified, and shared. The pages frequently modified are not recorded in KSM until their modification
frequency decreases. The unstable tree maintains pages that are sharing candidate and not frequently modified. The stable tree records the pages which have been shared and marked copy-on-write (CoW).

#### 1.2 TPS 

TPS uses the hash value of memory page's content to identify the same page. TPS maintains a global hash table, in which each entry records the hash value of a page's content and the reference number of a shared page. For each new page, its hash value is calculated and used as a key to search the global hash table. If the hash value of the new page matches that of an existing page, a full comparison of their page contents is performed to exclude a false match. If their contents are confirmed to be identical, the new page is reclaimed and pointed to the existing page. The copy-on-write (CoW) technique is used to handle writes to the shared pages.

> #### 2 Analysis of Memory Deduplication

#### 2.1 Redundancy Quantity

Virtual Machine (VM) is a primary application scenario of memory deduplication. When the same/similar operating systems or applications are running in different VMs,
lots of duplicated memory pages will be generated on the host/hypervisor system[^KSM]. Many works[^BARKER],[^chang],[^GUPTA],[^Miller] perform the empirical study on memory sharing of VMs. Chang et al.[^chang] found that the amount of redundant pages can be as low as 11% but also as high as 86% depending on the operating system and workload. Gupta et al.[^GUPTA] measured the amount of duplicated memory across three VMs and found that about 50% of the allocated memory could be saved through memory deduplication. Miller et al.[^Miller] found 110 MB of redundant memory in typical desktop workloads (LibreOffice, Firefox), and measured 400 MB (39%) of redundant data in their benchmarks.

#### 2.2 Time Overhead

To keep KSM enabled with parameters like sleep = 5000, pages_to_scan = 60, so that around 12000 virtual pages are scanned each second, allowing a maximum memory merging rate of 46.87MB/s in the original KSM[^KSM]. The memory scanner in the original KSM needs a considerable amount of time to detect new sharing opportunities (e.g., 5 mins) which hence misses the short-lived sharing opportunities (i.e., < 5 mins). However, the benchmarks[^Miller] show 80% of all sharing opportunities live between 30s and 5 mins. Thus, the original scanner is ineffective in the scenario. To address this problem, Miller et al.[^Miller] leverage the page hints in the host’s virtual file system (VFS) layer to speed up the memory scanner and observe more sharing opportunities.

> #### 3 My Comments

1. In order to ensure the access efficiency of memory, memory deduplication has to perform off-line deduplication due to the slow speed of the memory scanner. Specifically, the new pages are first stored in memory and then performed memory deduplication.
2. TPS needs to perform a full comparison of page contents when the hash matching occurs. I guess that TPS uses a general hash algorithm. If a secure hash algorithm, i.e., SHA-1 and MD5, is used to calculate the hash value of a page, the full comparison of page contents could be avoided.  Which method is more efficient?
3. Docker container has become more and more popular in recent years which is considered as an alternative to VM. A host may maintain hundreds of containers at the same time in which the memory situation is more complex.  Exploring the redundancy quantity and memory sharing in docker container may be an important problem.

**To be continued ......**

----

### References:

[^KSM]: Arcangeli A, Eidus I, Wright C. *Increasing memory density by using KSM*. In proceedings of the Linux ymposium. 2009.
[^Linux2632]: *Linux kernel 2.6.32, Section 1.3. Kernel Samepage Merging (memory deduplication)*. [kernelnewbies.org][kernel]. 2009.
[^TPS]: Guo F. *Understanding memory resource management in vmware vsphere 5.0*. VMware Inc, 2011.
[^rb-tree]: Thomas H. Cormen, Charles E. Leiserson, Ronald L. Rivest, and Clifford Stein. *Chapter 13: Red-Black Trees Introduction to Algorithms*, Second Edition. The MIT Press, September, 2001.
[^BARKER]: BARKER, S., ET AL. An empirical study of memory sharing in virtual machines. USENIX ATC 2012.
[^chang]: CHANG, C.-R., ET AL. *An empirical study on memory sharing of virtual machines for server consolidation*. Proc. of ISPA 2011.
[^GUPTA]: GUPTA, D., LEE, S., VRABLE, M., SAVAGE, S., ET AL. *Difference engine: harnessing memory redundancy in virtual machines*. Communications of the ACM, 2010, Volume 53.
[^Miller]: Miller K, Franz F, Rittinghaus M, et al. *XLH: More Effective Memory Deduplication Scanners Through Cross-layer Hints*. USENIX ATC 2013.

[kernel]: http:\\kernelnewbies.org\