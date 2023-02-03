---
layout: page
title: Projects
comments: true
permalink: /project/
---

* content
{:toc}

# My Projects
---

>## 1. Disaggregated Memory
   
### Overview

Memory disaggregation, which has attracted extensive attentions from both industry, e.g., HP’s The Machine and Intel RSD and academia, decouples the traditional monolithic compute and memory resources in datacenters and forms independent compute and memory resource pools. Due to resource pooling and independent hardware deployments, disaggregated memory enjoys the benefits of improvements on resource utilization, failure isolation, and elasticity. In the disaggregated memory architecture, compute blades run applications with only a small amount of memory as cache. In contrast, the memory pool stores application data with weak computing power. Due to not involving the compute resources in the memory pool, fast one-sided RDMA networks generally serve for data accesses from the compute blades to the memory pool.

### Publications

* Jiacheng Shen, **Pengfei Zuo**, Xuchuan Luo, Tianyi Yang, Yuxin Su, Yangfan Zhou, Michael Lyu, "[FUSEE: A Fully Memory-Disaggregated Key-Value Store](https://pfzuo.github.io/images/FUSEE-fast23.pdf)", accepted and to appear in the 21st USENIX Conference on File and Storage Technologies (**FAST**), 2023. 

* Pengfei Li, Yu Hua, **Pengfei Zuo**, Zhangyu Chen, Jiajie Sheng, "[ROLEX: A Scalable RDMA-oriented Learned Key-Value Store for Disaggregated Memory Systems](https://csyhua.github.io/csyhua/HUA-FAST23-ROLEX.pdf)", accepted and to appear in the 21st USENIX Conference on File and Storage Technologies (**FAST**), 2023. 

* Ming Zhang, Yu Hua, **Pengfei Zuo**, Lurong Liu, "[Localized Validation Accelerates Distributed Transactions on Disaggregated Persistent Memory]()", Accepted and to appear in ACM Transactions on Storage (**TOS**), 2023.

* **Pengfei Zuo\***, Qihui Zhou\*, Jiazhao Sun, Liu Yang, Shuangwu Zhang, Yu Hua, James Cheng, Rongfeng He, Huabing Yan, "[RACE: One-Sided RDMA-Conscious Extendible Hashing](https://csyhua.github.io/csyhua/hua-tos2022.pdf)", ACM Transactions on Storage (**TOS**) 18.2 (2022): 1-29. (*co-first authors) **[Invited Paper]**

* Ming Zhang, Yu Hua, **Pengfei Zuo**, Lurong Liu, "[FORD: Fast One-sided RDMA-based Distributed Transactions for Disaggregated Persistent Memory](https://www.usenix.org/system/files/fast22-zhang-ming.pdf)", Proceedings of the 20th USENIX Conference on File and Storage Technologies (**FAST**), 2022.

* **Pengfei Zuo**, Jiazhao Sun, Liu Yang, Shuangwu Zhang, Yu Hua, "[One-sided RDMA-Conscious Extendible Hashing for Disaggregated Memory](https://www.usenix.org/conference/atc21/presentation/zuo)", Proceedings of the USENIX Annual Technical Conference (**USENIX ATC**), 2021.

>## 2. Index Structures for NVM
   
### Overview
   
   Non-volatile memory (NVM) as persistent memory is expected to substitute or complement DRAM as the next-generation main memory, due to the strengths of non-volatility, high density, and near-zero standby power. In main memory systems, hashing index structures are fundamental building block to provide fast query response. However, hashing index structures originally designed for DRAM become inefficient for NVM due to new challenges such as hardware limitations of NVM and the requirement of data consistency. To address these problems, we propose a series of efficient hashing index schemes for NVM:

* In Path Hashing [MSST'2017], we propose a cost-efficient write-friendly hashing scheme that can significantly reduce extra writes for NVM. The basic idea of path hashing is to leverage a novel hash-collision resolution method, i.e., position sharing, which meets the needs of insertion and deletion requests without extra writes to NVMs. By further exploiting double-path hashing and path shortening techniques, path hashing delivers high performance of hash tables in terms of space utilization and request latency.

* In Cache-optimized Path Hashing [TPDS'2018], we enable path hashing to be cache-optimized by packing multiple cells in the same path
together and storing them into one cache line, and thus improve the cache line utilization in path hashing to obtain higher performance.

* In Level Hashing [OSDI'2018], we propose a write-optimized and high-performance hashing index scheme with low-overhead consistency guarantee and cost-efficient resizing for persistent memory. Level hashing provides a sharing-based two-level hash table, which achieves a constant-scale search/insertion/deletion/update time complexity in the worst case and rarely incurs extra NVM writes. To guarantee the consistency with low overhead, level hashing leverages log-free consistency schemes for insertion, deletion, and resizing operations, and an opportunistic log-free scheme for update operation. To cost-efficiently resize this hash table, level hashing leverages an in-place resizing scheme that only needs to rehash 1/3 of buckets instead of the entire table, thus significantly reducing the number of rehashed buckets and improving the resizing performance.

### Publications

* Zhangyu Chen, Yu Hua, Bo Ding, **Pengfei Zuo**, "[Lock-free Concurrent Level Hashing for Persistent Memory](https://csyhua.github.io/csyhua/hua-atc2020.pdf)", Proceedings of the USENIX Annual Technical Conference (**USENIX ATC**), 2020.

* **Pengfei Zuo**, Yu Hua, Jie Wu, "[Write-Optimized and High-Performance Hashing Index Scheme for Persistent Memory](http://nvmw.ucsd.edu/nvmw2019-program/unzip/current/nvmw2019-final16.pdf)", in the 10-th Non-Volatile Memories Workshop (**NVMW**), 2019. <span style="color:red">(Memorable Paper Award Finalist)</span>

* **Pengfei Zuo**, Yu Hua, Jie Wu, "[Write-Optimized and High-Performance Hashing Index Scheme for Persistent Memory](https://csyhua.github.io/csyhua/hua-OSDI2018.pdf)", in Proceedings of the 13th USENIX Symposium on Operating Systems Design and Implementation (**OSDI**), 2018.

* **Pengfei Zuo** and Yu Hua, "[A Write-friendly and Cache-optimized Hashing Scheme for Non-volatile Memory Systems](https://csyhua.github.io/csyhua/hua-tpds2018-nvm.pdf)", IEEE Transactions on Parallel and Distributed Systems (**TPDS**), Vol.29, No.5, May 2018, pages: 985-998.

* **Pengfei Zuo** and Yu Hua, "[A Write-friendly Hashing Scheme for Non-volatile Memory Systems](https://csyhua.github.io/csyhua/hua-MSST2017-NVM.pdf)", in Proceedings of the 33rd International Conference on Massive Storage Systems and Technology (**MSST**), 2017. 

---
>## 3. Secure NVM


### Overview
	
Non-volatile memory (NVM) technologies are considered as promising candidates of the next-generation main memory. However, the non-volatility of NVMs leads to new security vulnerabilities. For example, it is not difficult to access sensitive data stored on stolen NVMs. Memory encryption can be employed to mitigate the security vulnerabilities, but it increases the number of bits written to NVMs due to the diffusion property and thereby aggravates the NVM wear-out induced by writes. Moreover, in the non-volatile memory, ensuring the security and correctness of persistent data is fundamental. However, the security and persistence issues are usually studied independently in existing work. To achieve both data security and persistence, simply combining existing persistence schemes with memory encryption is inefficient due to crash inconsistency and significant performance degradation. 

* In DeWrite[MICRO'2018], we propose a secure and deduplication-aware scheme to enhance the performance and endurance of encrypted NVMs based on a new in-line deduplication technique and the synergistic integrations of deduplication and encryption. Specifically, it performs low-latency in-line deduplication to exploit the abundant cache-line-level duplications leveraging the intrinsic read/write asymmetry of NVMs and light-weight hashing. It also opportunistically parallelizes the operations of deduplication and encryption and allows them to co-locate the metadata for high time and space efficiency. 
* In SecPM [HotStorage'2018], we propose a secure and persistent memory system. SecPM leverages the CWT scheme to guarantee the crash consistency via ensuring both the data and its counter are durable before the data flush completes, and leverages the CWR scheme to improve the performance via exploiting the spatial locality of counter storage, log and data writes. 

### Publications

* **Pengfei Zuo**, Yu Hua, Yuan Xie, "[SuperMem: Enabling Application-transparent Secure Persistent Memory with Low Overheads](https://csyhua.github.io/csyhua/hua-micro2019.pdf)", Proceedings of the 52nd IEEE/ACM International Symposium on Microarchitecture (**MICRO**), 2019.    

* **Pengfei Zuo**, Yu Hua, Ming Zhao, Wen Zhou, Yuncheng Guo, "[Improving the Performance and Endurance of Encrypted Non-volatile Main Memory through Deduplicating Writes](http://nvmw.ucsd.edu/nvmw2019-program/unzip/current/nvmw2019-final25.pdf)", in the 10-th Non-Volatile Memories Workshop (**NVMW**), 2019.

* **Pengfei Zuo**, Yu Hua, Ming Zhao, Wen Zhou, Yuncheng Guo, "[Write Deduplication and Hash Mode Encryption for Secure Non-volatile Main Memory](https://csyhua.github.io/csyhua/hua-IEEE-micro.pdf)", Accepted and to appear in **IEEE Micro**, 2019.

* **Pengfei Zuo**, Yu Hua, Ming Zhao, Wen Zhou, Yuncheng Guo, "[Improving the Performance and Endurance of Encrypted Non-volatile Main Memory through Deduplicating Writes](https://csyhua.github.io/csyhua/hua-MICRO2018.pdf)", in Proceedings of the 51st IEEE/ACM International Symposium on Microarchitecture (**MICRO**), 2018.

* **Pengfei Zuo** and Yu Hua, "[SecPM: a Secure and Persistent Memory System for Non-volatile Memory](https://csyhua.github.io/csyhua/hua-hotstorage2018.pdf)", in Proceedings of 10th USENIX Workshop on Hot Topics in Storage and File Systems (**HotStorage**), 2018.

---
>## 4. Data Deduplication

### Overview

Data deduplication is able to effectively identify and eliminate redundant data and only maintain a single copy of data. Hence, it is widely used in backup and archival storage systems to save storage space. Nevertheless, redundant data also widely exist in other application situations such as network, cloud storage, and devices. How to efficienlt deploying or improving deduplicaiton techqiues in these applicaitons is challenging.   
* In BEES [ICDCS'2017], we propose a bandwidth and energy efficient image sharing system to provide efficient image sharing in disasters by leveraging deduplication. The salient feature behind BEES is to propose the concept of Approximate Image Sharing (AIS), which explores and exploits approximate feature extraction, redundancy detection, and image uploading to trade the slightly low quality of computation results in content-based redundancy elimination for higher bandwidth and energy efficiency.

* In RRCS [IPDPS'2018], we propose a simple yet effective scheme to significantly mitigate the risk of the LRI attack while maintaining the high bandwidth efficiency of deduplication in cloud storage systems, by adding randomized redundant chunks to mix up the real deduplication states of files used for the LRI attack.

* In DeWrite [MICRO'2018], we propose a secure and deduplication-aware scheme to enhance the performance and endurance of encrypted NVM devices based on a new in-line deduplication technique and the synergistic integrations of deduplication and encryption.  


### Publications

*  **Pengfei Zuo**, Yu Hua, Yuanyuan Sun, Xue Liu, Jie Wu, Yuncheng Guo, Wen Xia, Shunde Cao, Dan Feng, "[Bandwidth and Energy Efficient Image Sharing for Situation Awareness in Disasters](https://csyhua.github.io/csyhua/hua-tpds2018-bandwidth.pdf)", in IEEE Transactions on Parallel and Distributed Systems (**TPDS**), vol. 30, no. 1, pp. 15-28, 1 Jan. 2019.

* **Pengfei Zuo**, Yu Hua, Ming Zhao, Wen Zhou, Yuncheng Guo, "[Improving the Performance and Endurance of Encrypted Non-volatile Main Memory through Deduplicating Writes](https://csyhua.github.io/csyhua/hua-MICRO2018.pdf)", in Proceedings of the 51st IEEE/ACM International Symposium on Microarchitecture (**MICRO**), 2018.

* **Pengfei Zuo**, Yu Hua, Cong Wang, Wen Xia, Shunde Cao, Yukun Zhou, Yuanyuan Sun, "[Mitigating Traffic-based Side Channel Attacks in Bandwidth-efficient Cloud Storage](https://csyhua.github.io/csyhua/hua-ipdps2018.pdf)", in Proceedings of the 32nd IEEE International Parallel and Distributed Processing Symposium (**IPDPS**), 2018.

* **Pengfei Zuo**, Yu Hua, Xue Liu, Dan Feng, Wen Xia, Shunde Cao, Jie Wu, Yuanyuan Sun, Yuncheng Guo, "[BEES: Bandwidth- and Energy- Efficient Image Sharing for Real-time Situation Awareness](https://csyhua.github.io/csyhua/hua-ICDCS2017.pdf)", in Proceedings of the 37th International Conference on Distributed Computing Systems (**ICDCS**), 2017.