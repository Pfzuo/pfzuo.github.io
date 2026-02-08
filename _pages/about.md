---
layout: about
title: Home
permalink: /
subtitle: >
  <b>Email:</b> <a href="mailto:pfzuo.cs@gmail.com">pfzuo.cs@gmail.com</a>

profile:
  align: right
  image: zuo-2021.jpg
  image_circular: false # crops the image to make it circular
  # more_info: >
    # <p>555 your office number</p>
    # <p>123 your address street</p>
    # <p>Your City, State 12345</p>

selected_papers: true # includes a list of papers marked as "selected={true}"
social: true # includes social icons at the bottom of the page

announcements:
  enabled: true # includes a list of news items
  scrollable: true # adds a vertical scroll bar if there are more than 3 news items
  limit: 5 # leave blank to include all the news in the `_news` folder

latest_posts:
  enabled: true
  scrollable: true # adds a vertical scroll bar if there are more than 3 new post items
  limit: 3 # leave blank to include all the blog posts
---

I currently serve as the chief architect of AI-native storage at Huawei Cloud. I lead the EMS ([Elastic Memory Service](https://www.huaweicloud.com/product/ems.html)) team to build a disaggregated memory service layer in the cloud, upgrading Huawei Cloud's two-tier infrastructure architecture that disaggregates storage and computing into a three-tier architecture that disaggregates computing, memory, and storage. This transformation enables higher resource elasticity and utilization. EMS also serves as a foundational memory infrastructure to enhance the efficiency of LLM training and inference on Huawei Cloud. 

I received my Ph.D. degree (advised by Prof. [Yu Hua](https://csyhua.github.io/)) in Computer Science from Huazhong University of Science and Technology (HUST) in 2019. I was a visiting Ph.D. student (advised by Prof. [Yuan Xie](https://ece.hkust.edu.hk/yuanxie)) at the University of California, Santa Barbara (UCSB) during 2018-2019. I received a B.E. degree in Computer Science from HUST in 2014.  

My research focuses on AI and cloud infrastructure, with an emphasis on machine learning systems and memory systems. I have published 50+ refereed papers in top-tier computer systems and architecture conferences and journals, including SOSP, OSDI, MICRO, ASPLOS, FAST, USENIX ATC, VLDB, and DAC. I received the [2020 ACM China Doctoral Dissertation Award](https://www.acmturc.com/2021/cn/doctoral_thesis_award.html) (only two awardees among all computer disciplines across China every year) and the [Best Paper Award in FAST 2023](https://www.usenix.org/conferences/best-papers?taxonomy_vocabulary_1_tid=2023&title_1=FAST). The open-source codes for our research on AI systems and disaggregated data centers are available at [ASISys](https://github.com/ASISys) and [DMemSys](https://github.com/dmemsys), respectively.


***I am seeking motivated interns and postdocs in AI systems. If you're passionate about tackling key industry challenges and publishing impactful research, feel free to reach out!*** 

---

### Research

#### AI Systems and Algorithms  
* LLM Serving Systems: [CachedAttention (USENIX ATC'24)](https://www.usenix.org/conference/atc24/presentation/gao-bin-cost), [Adrenaline (ArXiv'25)](https://arxiv.org/abs/2406.10198), [TaiChi (ArXiv'25)](https://arxiv.org/abs/2508.01989), [SparseServe (ArXiv'25)](https://arxiv.org/pdf/2509.24626), [DualMap (ICLR'26)](https://openreview.net/pdf?id=zCadrJ32Xn)
* Generative Recommendation: [RelayGR (Technical Report'26)](https://arxiv.org/abs/2601.01712)  
* AI Algorithms: [AdaSkip (AAAI'25)](https://arxiv.org/abs/2405.19583),  [Progressive Sparse Attention (ArXiv'25)](https://arxiv.org/abs/2406.10731)  
* AI Hardware Architectures: [DeepSniffer (ASPLOS'20)](https://dl.acm.org/doi/10.1145/3373376.3378487), [SEAL (DAC'21)](https://dl.acm.org/doi/10.1109/DAC18074.2021.9586256), [Memory Trojaning (TCAD'21)](https://ieeexplore.ieee.org/document/9345491), [CloudMatrix384 (Technical Report'25)](https://arxiv.org/abs/2506.12708)  

#### Memory Systems and Architectures  
* Disaggregated Memory Systems: [FORD (FAST'22)](https://www.usenix.org/system/files/fast22-zhang-ming.pdf), [uKaron (USENIX ATC'22)](https://www.usenix.org/system/files/atc22-guerraoui.pdf), [FUSEE (FAST'23)](https://www.usenix.org/system/files/fast23-shen.pdf),  [Ditto (SOSP'23)](https://dl.acm.org/doi/10.1145/3600006.3613144), [Aceso (SOSP'24)](https://dl.acm.org/doi/10.1145/3694715.3695951)  
* Disaggregated Memory Indexes: [RACE (USENIX ATC'21)](https://www.usenix.org/system/files/atc21-zuo.pdf), [ROLEX (FAST'23, Best Paper)](https://www.usenix.org/conference/fast23/presentation/li-pengfei), [SMART (OSDI'23)](https://www.usenix.org/conference/osdi23/presentation/luo), [CHIME (SOSP'24)](https://arxiv.org/abs/2405.20831)  
* Persistent Memory Systems:  [Path Hashing (MSST'17)](https://csyhua.github.io/csyhua/hua-MSST2017-NVM.pdf), [Level Hashing (OSDI'18)](https://www.usenix.org/conference/osdi18/presentation/zuo) , [CLevel (USENIX ATC'20)](https://www.usenix.org/conference/atc20/presentation/chen)
* Persistent Memory Architectures: [DPEC (DATE'18)](https://ieeexplore.ieee.org/document/8342113), [DeWrite (MICRO'18)](https://ieeexplore.ieee.org/document/8595424), [SecPM (HotStorage'18)](https://www.usenix.org/conference/hotstorage18/presentation/zuo), [SuperMem (MICRO'19)](https://dl.acm.org/doi/10.1145/3352460.3358290), [SimCom (DAC'20)](https://ieeexplore.ieee.org/document/9218581)  

#### Storage Systems  
* Indexes: [MinCounter (MSST'15)](https://ieeexplore.ieee.org/document/7165945), [SmartCuckoo (USENIX ATC'17)](https://pfzuo.github.io/publication/), [DLSH (SoCC'17)](https://pfzuo.github.io/publication/), [FINEDex (VLDB'22)](https://pfzuo.github.io/publication/)  
* Deduplication Systems: [SMR (MSST'17)](https://ieeexplore.ieee.org/document/7965055), [BEES (ICDCS'17)](https://pfzuo.github.io/publication/), [RRCS (IPDPS'18)](https://ieeexplore.ieee.org/document/8374580)

--- 

