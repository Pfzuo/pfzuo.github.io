---
layout: page
title: Projects
permalink: /projects/
description: 
nav: true
nav_order: 3
display_categories: []
horizontal: false
---



## 1. LLM Serving Systems

---


<div style="display:flex;justify-content:center;">
  <svg width="500" height="414" viewBox="0 0 500 414" xmlns="http://www.w3.org/2000/svg" font-family="Arial, Helvetica, sans-serif">
    <rect x="0" y="0" width="500" height="414" fill="#fff"/>

    <!-- Distributed Request Router -->
    <rect x="2" y="4" width="496" height="62" fill="#b9eeff" stroke="#111" stroke-width="1.5"/>
    <text x="250" y="21" text-anchor="middle" font-size="14" font-weight="800" letter-spacing="0.2" fill="#111">Distributed Request Router</text>
    <rect x="9" y="27" width="482" height="33" fill="#fff" stroke="#111" stroke-width="1.5"/>
    <text x="250" y="40" text-anchor="middle" font-size="12" font-weight="700" fill="#111">DualMap: Achieving Both Cache Afinity and Load Balance</text>
    <text x="250" y="54" text-anchor="middle" font-size="12" font-weight="800" fill="#ff008a">(ICLR'26)</text>

    <!-- Router <-> Serving connectors -->
    <line x1="118.75" y1="66" x2="118.75" y2="98" stroke="#111" stroke-width="1.5"/>
    <polygon points="114,73 122,73 118,66" fill="#111"/>
    <polygon points="114,91 122,91 118,98" fill="#111"/>
    <line x1="350.75" y1="66" x2="350.75" y2="98" stroke="#111" stroke-width="1.5"/>
    <polygon points="346,73 354,73 350,66" fill="#111"/>
    <polygon points="346,91 354,91 350,98" fill="#111"/>

    <!-- Disaggregated LLM Serving -->
    <rect x="2" y="98" width="496" height="232" fill="#c8eaa7" stroke="#111" stroke-width="1.5"/>
    <text x="250" y="116" text-anchor="middle" font-size="14" font-weight="800" fill="#111">Disaggregated LLM Serving</text>

    <!-- Prefill Instance stack -->
    <polygon points="24.02,142 209.02,142 200.98,172 15.98,172" fill="#8cd24d" stroke="#2f5e23" stroke-width="1.5"/>
    <polygon points="28.02,138 213.02,138 204.98,168 19.98,168" fill="#95d956" stroke="#2f5e23" stroke-width="1.5"/>
    <polygon points="32.02,134 217.02,134 208.98,164 23.98,164" fill="#9ddf5d" stroke="#2f5e23" stroke-width="1.5"/>
    <polygon points="36.02,130 221.02,130 212.98,160 27.98,160" fill="#a6e666" stroke="#2f5e23" stroke-width="1.5"/>
    <text x="72" y="154" font-size="11" font-weight="700" fill="#111">Prefill Instance</text>

    <!-- Decode Instance stack -->
    <polygon points="284.02,142 469.02,142 460.98,172 275.98,172" fill="#8cd24d" stroke="#2f5e23" stroke-width="1.5"/>
    <polygon points="288.02,138 473.02,138 464.98,168 279.98,168" fill="#95d956" stroke="#2f5e23" stroke-width="1.5"/>
    <polygon points="292.02,134 477.02,134 468.98,164 283.98,164" fill="#9ddf5d" stroke="#2f5e23" stroke-width="1.5"/>
    <polygon points="296.02,130 481.02,130 472.98,160 287.98,160" fill="#a6e666" stroke="#2f5e23" stroke-width="1.5"/>
    <text x="332" y="154" font-size="11" font-weight="700" fill="#111">Decode Instance</text>

    <!-- Serving technique cards -->
    <rect x="9" y="186" width="238" height="42" fill="#fff" stroke="#111" stroke-width="1.5"/>
    <text x="128" y="201" text-anchor="middle" font-size="12" font-weight="700" fill="#111">Adrenaline: Attention Disaggregation</text>
    <text x="128" y="215" text-anchor="middle" font-size="12" font-weight="800" fill="#ff008a">(ArXiv'25)</text>

    <rect x="253" y="186" width="238" height="42" fill="#fff" stroke="#111" stroke-width="1.5"/>
    <text x="372" y="201" text-anchor="middle" font-size="12" font-weight="700" fill="#111">SparseServe: Serving with DSA</text>
    <text x="372" y="215" text-anchor="middle" font-size="12" font-weight="800" fill="#ff008a">(ICS'26)</text>

    <rect x="9" y="235" width="238" height="42" fill="#fff" stroke="#111" stroke-width="1.5"/>
    <text x="128" y="250" text-anchor="middle" font-size="12" font-weight="700" fill="#111">TaiJi: Unifying PD Aggregation &amp; Disag.</text>
    <text x="128" y="264" text-anchor="middle" font-size="12" font-weight="800" fill="#ff008a">(SC'26)</text>

    <rect x="253" y="235" width="238" height="42" fill="#fff" stroke="#111" stroke-width="1.5"/>
    <text x="372" y="250" text-anchor="middle" font-size="12" font-weight="700" fill="#111">Progressive Sparse Attention</text>
    <text x="372" y="264" text-anchor="middle" font-size="12" font-weight="800" fill="#ff008a">(ArXiv'25)</text>

    <rect x="9" y="284" width="238" height="42" fill="#fff" stroke="#111" stroke-width="1.5"/>
    <text x="128" y="299" text-anchor="middle" font-size="12" font-weight="700" fill="#111">CloudMatrix-Infer</text>
    <text x="128" y="313" text-anchor="middle" font-size="12" font-weight="800" fill="#ff008a">(Technical Report'25)</text>

    <rect x="253" y="284" width="238" height="42" fill="#fff" stroke="#111" stroke-width="1.5"/>
    <text x="372" y="299" text-anchor="middle" font-size="12" font-weight="700" fill="#111">AdaSkip: Adaptive Sublayer Skipping</text>
    <text x="372" y="313" text-anchor="middle" font-size="12" font-weight="800" fill="#ff008a">(AAAI'25)</text>

    <!-- Serving <-> Caching connectors -->
    <line x1="114.75" y1="330" x2="114.75" y2="339" stroke="#111" stroke-width="1.5"/>
    <polygon points="110,337 118,337 114,330" fill="#111"/>
    <polygon points="110,334 118,334 114,341" fill="#111"/>
    <line x1="362.75" y1="330" x2="362.75" y2="339" stroke="#111" stroke-width="1.5"/>
    <polygon points="358,337 366,337 362,330" fill="#111"/>
    <polygon points="358,334 366,334 362,341" fill="#111"/>

    <!-- Context Caching -->
    <rect x="2" y="339" width="496" height="72" fill="#fff1bf" stroke="#111" stroke-width="1.5"/>
    <text x="250" y="357" text-anchor="middle" font-size="14" font-weight="800" fill="#111">Context Caching</text>
    <rect x="9" y="367" width="482" height="38" fill="#fff" stroke="#111" stroke-width="1.5"/>
    <text x="250" y="380" text-anchor="middle" font-size="12" font-weight="700" fill="#111">CachedAttention: The First Context Caching System with Hierarchical Storage</text>
    <text x="250" y="395" text-anchor="middle" font-size="12" font-weight="800" fill="#ff008a">(USENIX ATC'24)</text>
  </svg>
</div>
<br>

This project targets the fundamental challenges of building highly efficient, scalable, and cost-effective LLM serving systems. As illustrated in the figure, we introduce key innovations across every layer of the serving stack.

**Distributed Request Router:** At the top of the stack, our intelligent router manages incoming traffic. Going beyond simple load balancing, our work, [DualMap (ICLR'26)](https://openreview.net/pdf?id=zCadrJ32Xn) achieves both cache affinity and load balance for distributed LLM serving. It ensures that requests are routed not only to available instances but preferentially to those that may already have the required context cached, significantly reducing redundant prefill computation.

**Disaggregated LLM Serving:** At the core of the system, we decouple the computationally distinct phases of LLM inference—prompt processing (Prefill Instance) and token generation (Decode Instance). This fundamental separation is orchestrated by system-wide optimizations such as [Adrenaline (ArXiv'25)](https://arxiv.org/abs/2406.10198), which disaggregates and offloads memory-bound decode-phase attention to compute-bound prefill instances, and [TaiJi (SC'26)](https://arxiv.org/abs/2508.01989), which unifies PD aggregation and disaggregation under a new serving architecture. To further accelerate the memory-bound decode phase, we propose a new dynamic sparse attention algorithm ([PSA@ArXiv'25](https://arxiv.org/abs/2406.10731)), [SparseServe (ICS'26)](https://arxiv.org/abs/2509.24626v1), and TileSparse (ICML'26) for compute-bound sparse-attention decoding.

**Context Caching:** Underpinning the stack is a robust caching layer. Our foundational work, [CachedAttention (USENIX ATC'24)](https://www.usenix.org/conference/atc24/presentation/gao-bin-cost), is the first context caching system to leverage hierarchical storage (e.g., DRAM and SSDs). This enables efficient management of massive KV caches for long-context handling and high-throughput serving.

Together, these layers form a comprehensive, principled solution that addresses the primary bottlenecks in modern LLM serving, paving the way for more powerful and accessible AI services.


<br>


## 2. The CloudMatrix384 Supernode System


---


<div style="display:flex;justify-content:center;">
  <svg width="500" height="372" viewBox="0 0 500 372" xmlns="http://www.w3.org/2000/svg" font-family="Arial, Helvetica, sans-serif">
    <rect x="0" y="0" width="500" height="372" fill="#fff"/>

    <!-- Supernode: one integrated hardware-software co-design -->
    <rect x="2" y="6" width="496" height="360" rx="16" fill="#f2f8ff" stroke="#111" stroke-width="1.5"/>
    <text x="250" y="30" text-anchor="middle" font-size="15" font-weight="800" fill="#111">CloudMatrix384 Supernode</text>
    <text x="250" y="47" text-anchor="middle" font-size="10" font-weight="700" fill="#444">Hardware–Software Co-Design</text>

    <!-- Software: CloudMatrix-Infer -->
    <rect x="18" y="60" width="464" height="66" fill="#d7e3ff" stroke="#111" stroke-width="1.5"/>
    <text x="250" y="78" text-anchor="middle" font-size="12" font-weight="800" fill="#111">CloudMatrix-Infer  (Serving Software)</text>
    <text x="250" y="93" text-anchor="middle" font-size="9" font-weight="600" fill="#555">Peer-to-Peer Serving · EP320 Expert Parallelism · INT8 Quantization</text>
    <rect x="40" y="101" width="126" height="18" fill="#a6e666" stroke="#111" stroke-width="1"/>
    <text x="103" y="114" text-anchor="middle" font-size="10" font-weight="700" fill="#111">Prefill</text>
    <rect x="187" y="101" width="126" height="18" fill="#9cd2ff" stroke="#111" stroke-width="1"/>
    <text x="250" y="114" text-anchor="middle" font-size="10" font-weight="700" fill="#111">Decode</text>
    <rect x="334" y="101" width="126" height="18" fill="#ffe08a" stroke="#111" stroke-width="1"/>
    <text x="397" y="114" text-anchor="middle" font-size="10" font-weight="700" fill="#111">Caching (KV)</text>

    <!-- Co-design: software roles mapped onto pooled fabric -->
    <text x="250" y="140" text-anchor="middle" font-size="9" font-style="italic" fill="#555">serving roles co-designed &amp; mapped onto the pooled UB fabric</text>
    <line x1="60" y1="126" x2="60" y2="150" stroke="#111" stroke-width="1.5"/>
    <polygon points="56,144 64,144 60,151" fill="#111"/>
    <line x1="440" y1="126" x2="440" y2="150" stroke="#111" stroke-width="1.5"/>
    <polygon points="436,144 444,144 440,151" fill="#111"/>

    <!-- Hardware fabric: all devices on one UB (any-to-any pooling) -->
    <rect x="18" y="150" width="464" height="204" fill="#eafae0" stroke="#111" stroke-width="1.5"/>
    <text x="250" y="169" text-anchor="middle" font-size="10" font-weight="800" fill="#111">Unified Bus (UB) Network — Non-Blocking All-to-All &amp; Resource Pooling</text>

    <!-- NPU tiles, colored by the serving role assigned by the software -->
    <g stroke="#111" stroke-width="1">
      <rect x="34" y="182" width="36" height="34" fill="#a6e666"/><rect x="78" y="182" width="36" height="34" fill="#a6e666"/><rect x="122" y="182" width="36" height="34" fill="#a6e666"/><rect x="166" y="182" width="36" height="34" fill="#a6e666"/>
      <rect x="210" y="182" width="36" height="34" fill="#9cd2ff"/><rect x="254" y="182" width="36" height="34" fill="#9cd2ff"/><rect x="298" y="182" width="36" height="34" fill="#9cd2ff"/>
      <rect x="342" y="182" width="36" height="34" fill="#ffe08a"/><rect x="386" y="182" width="36" height="34" fill="#ffe08a"/><rect x="430" y="182" width="36" height="34" fill="#ffe08a"/>
    </g>
    <g font-size="8" font-weight="700" fill="#111" text-anchor="middle">
      <text x="52" y="203">NPU</text><text x="96" y="203">NPU</text><text x="140" y="203">NPU</text><text x="184" y="203">NPU</text><text x="228" y="203">NPU</text><text x="272" y="203">NPU</text><text x="316" y="203">NPU</text><text x="360" y="203">NPU</text><text x="404" y="203">NPU</text><text x="448" y="203">NPU</text>
    </g>
    <g stroke="#111" stroke-width="1">
      <line x1="52" y1="216" x2="52" y2="248"/><line x1="96" y1="216" x2="96" y2="248"/><line x1="140" y1="216" x2="140" y2="248"/><line x1="184" y1="216" x2="184" y2="248"/><line x1="228" y1="216" x2="228" y2="248"/><line x1="272" y1="216" x2="272" y2="248"/><line x1="316" y1="216" x2="316" y2="248"/><line x1="360" y1="216" x2="360" y2="248"/><line x1="404" y1="216" x2="404" y2="248"/><line x1="448" y1="216" x2="448" y2="248"/>
    </g>

    <!-- UB spine -->
    <rect x="30" y="248" width="440" height="16" rx="8" fill="#ffd76a" stroke="#111" stroke-width="1.5"/>
    <text x="250" y="260" text-anchor="middle" font-size="9" font-weight="800" fill="#111">UB Fabric · any-to-any</text>

    <!-- CPU tiles -->
    <g stroke="#111" stroke-width="1">
      <line x1="64" y1="264" x2="64" y2="286"/><line x1="138" y1="264" x2="138" y2="286"/><line x1="212" y1="264" x2="212" y2="286"/><line x1="286" y1="264" x2="286" y2="286"/><line x1="360" y1="264" x2="360" y2="286"/><line x1="434" y1="264" x2="434" y2="286"/>
    </g>
    <g stroke="#111" stroke-width="1" fill="#ffc4c4">
      <rect x="44" y="286" width="40" height="30"/><rect x="118" y="286" width="40" height="30"/><rect x="192" y="286" width="40" height="30"/><rect x="266" y="286" width="40" height="30"/><rect x="340" y="286" width="40" height="30"/><rect x="414" y="286" width="40" height="30"/>
    </g>
    <g font-size="8" font-weight="700" fill="#111" text-anchor="middle">
      <text x="64" y="305">CPU</text><text x="138" y="305">CPU</text><text x="212" y="305">CPU</text><text x="286" y="305">CPU</text><text x="360" y="305">CPU</text><text x="434" y="305">CPU</text>
    </g>

    <!-- Legend: NPU tile color = serving role -->
    <text x="70" y="338" text-anchor="end" font-size="8" font-weight="700" fill="#555">NPU role:</text>
    <rect x="78" y="329" width="12" height="10" fill="#a6e666" stroke="#111" stroke-width="1"/>
    <text x="93" y="338" font-size="8" fill="#333">Prefill</text>
    <rect x="150" y="329" width="12" height="10" fill="#9cd2ff" stroke="#111" stroke-width="1"/>
    <text x="165" y="338" font-size="8" fill="#333">Decode</text>
    <rect x="228" y="329" width="12" height="10" fill="#ffe08a" stroke="#111" stroke-width="1"/>
    <text x="243" y="338" font-size="8" fill="#333">Caching</text>
    <text x="470" y="338" text-anchor="end" font-size="8" fill="#555">384 &#215; Ascend 910C NPU · 192 &#215; Kunpeng CPU</text>

    <!-- Paper citation (whole system) -->
    <a href="https://arxiv.org/abs/2506.12708" target="_blank">
      <text x="250" y="362" text-anchor="middle" font-size="10" font-weight="800" fill="#ff008a">Serving Large Language Models on Huawei CloudMatrix384 (Technical Report'25)</text>
    </a>
  </svg>
</div>
<br>

This project builds a next-generation AI datacenter architecture for LLMs, realized in Huawei's production-grade **CloudMatrix384** supernode—an end-to-end hardware–software co-design presented in our [technical report](https://arxiv.org/abs/2506.12708). On the hardware side, the supernode tightly integrates **384 Ascend 910C NPUs** and **192 Kunpeng CPUs** over an ultra-high-bandwidth **Unified Bus (UB) network** that enables direct all-to-all communication and dynamic pooling of compute, memory, and cache resources—well suited to communication-intensive workloads such as large-scale MoE expert parallelism and distributed KV-cache access. Co-designed with this fabric, **CloudMatrix-Infer** is the accompanying LLM serving software built on three core innovations: (i) a **peer-to-peer serving architecture** that independently scales prefill, decode, and caching; (ii) a **large-scale expert-parallelism** strategy supporting **EP320** via efficient UB-based token dispatch; and (iii) **hardware-aware optimizations** including specialized operators, microbatch-based pipelining, and INT8 quantization. On DeepSeek-R1, the co-designed system achieves state-of-the-art efficiency—6,688 tokens/s per NPU for prefill and 1,943 tokens/s per NPU for decode (<50 ms TPOT)—while sustaining 538 tokens/s even under a stringent 15 ms latency constraint, with INT8 preserving accuracy across benchmarks.


<br>


## 3. Agents


---


<div style="display:flex;justify-content:center;">
  <svg width="500" height="348" viewBox="0 0 500 348" xmlns="http://www.w3.org/2000/svg" font-family="Arial, Helvetica, sans-serif">
    <rect x="0" y="0" width="500" height="348" fill="#fff"/>

    <!-- Agent outer box -->
    <rect x="2" y="2" width="496" height="248" rx="16" fill="#fff" stroke="#111" stroke-width="1.5"/>
    <text x="14" y="31" font-size="16" font-weight="800" fill="#111">Agent</text>

    <!-- Agent Brain -->
    <rect x="108" y="10" width="286" height="227" fill="#fff" stroke="#111" stroke-width="1.5"/>
    <text x="251" y="33" text-anchor="middle" font-size="16" font-weight="800" fill="#111">Agent Brain</text>

    <!-- Memory -->
    <rect x="117" y="40" width="268" height="65" fill="#cfe9b4" stroke="#111" stroke-width="1.5"/>
    <text x="251" y="58" text-anchor="middle" font-size="12" font-weight="800" fill="#111">Memory</text>
    <rect x="138" y="67" width="226" height="28" fill="#fff" stroke="#111" stroke-width="1.5"/>
    <text x="251" y="81" text-anchor="middle" font-size="10" font-weight="700" fill="#111">Efficient Agent Memory System</text>
    <text x="251" y="91" text-anchor="middle" font-size="10" font-weight="800" fill="#ff008a">(Under Review)</text>

    <!-- Memory -> Planning connector -->
    <line x1="250" y1="106" x2="250" y2="117" stroke="#111" stroke-width="1.5"/>
    <polygon points="246,111 254,111 250,118" fill="#111"/>

    <!-- Planning -->
    <rect x="117" y="117" width="268" height="110" fill="#ffc4c4" stroke="#111" stroke-width="1.5"/>
    <text x="251" y="133" text-anchor="middle" font-size="12" font-weight="800" fill="#111">Planning (LLM)</text>
    <a href="https://arxiv.org/abs/2605.10195" target="_blank">
      <rect x="138" y="143" width="226" height="34" fill="#fff" stroke="#111" stroke-width="1.5"/>
      <text x="251" y="156" text-anchor="middle" font-size="10" font-weight="700" fill="#111">Accelerating ToT Reasoning</text>
      <text x="251" y="169" text-anchor="middle" font-size="10" font-weight="800" fill="#ff008a">SPEX (OSDI'26)</text>
    </a>
    <a href="https://arxiv.org/abs/2602.06527" target="_blank">
      <rect x="138" y="185" width="226" height="34" fill="#fff" stroke="#111" stroke-width="1.5"/>
      <text x="251" y="198" text-anchor="middle" font-size="10" font-weight="700" fill="#111">Scaling Multi-Path CoT Reasoning</text>
      <text x="251" y="211" text-anchor="middle" font-size="10" font-weight="800" fill="#ff008a">HyPER (ICML'26)</text>
    </a>

    <!-- Perception / Action -->
    <rect x="8" y="177" width="72" height="35" fill="#b9eeff" stroke="#111" stroke-width="1.5"/>
    <text x="44" y="198" text-anchor="middle" font-size="12" font-weight="800" fill="#111">Perception</text>
    <rect x="414" y="177" width="72" height="35" fill="#b9eeff" stroke="#111" stroke-width="1.5"/>
    <text x="450" y="198" text-anchor="middle" font-size="12" font-weight="800" fill="#111">Action</text>

    <line x1="80" y1="194" x2="117" y2="194" stroke="#111" stroke-width="1.5"/>
    <polygon points="113,191 113,199 120,195" fill="#111"/>
    <line x1="385" y1="194" x2="414" y2="194" stroke="#111" stroke-width="1.5"/>
    <polygon points="410,191 410,199 417,195" fill="#111"/>

    <!-- Observation (Perception <-> Environment) -->
    <line x1="43" y1="212" x2="43" y2="280" stroke="#111" stroke-width="1.5"/>
    <polygon points="39,219 47,219 43,212" fill="#111"/>
    <polygon points="39,273 47,273 43,280" fill="#111"/>
    <text x="55" y="263" font-size="10" font-weight="500" fill="#111">Observation</text>

    <!-- Action -> Environment -->
    <line x1="450" y1="212" x2="450" y2="280" stroke="#111" stroke-width="1.5"/>
    <polygon points="446,273 454,273 450,280" fill="#111"/>

    <!-- Environment -->
    <rect x="2" y="283" width="496" height="60" rx="12" fill="#fff" stroke="#111" stroke-width="1.5"/>
    <text x="10" y="313" font-size="16" font-weight="800" fill="#111">Environment</text>

    <rect x="108" y="293" width="116" height="34" fill="#fff" stroke="#111" stroke-width="1.5"/>
    <text x="166" y="314" text-anchor="middle" font-size="12" font-weight="800" fill="#111">Reward</text>
    <rect x="239" y="293" width="116" height="34" fill="#fff" stroke="#111" stroke-width="1.5"/>
    <text x="297" y="314" text-anchor="middle" font-size="12" font-weight="800" fill="#111">Feedback</text>
    <rect x="370" y="293" width="116" height="34" fill="#fff" stroke="#111" stroke-width="1.5"/>
    <text x="428" y="314" text-anchor="middle" font-size="12" font-weight="800" fill="#111">Tool</text>
  </svg>
</div>
<br>

This project tackles the central challenges in building advanced autonomous LLM agents. As shown in the figure, the core architecture is organized around an Agent Brain, which serves as the cognitive hub for decision-making. The agent functions in a continuous loop: the Perception module processes observations from the Environment, the Planning module formulates an Action, and the action in turn alters the environment, producing new observations, reward signals, feedback, and opportunities to invoke external tools. This creates an adaptive learning cycle. By integrating advances in reasoning and memory, our project aims to develop agents that are more capable, efficient, and intelligent. We currently focus on two key components of the Agent Brain:

**Planning (LLM):** At the core of reasoning is a large language model dedicated to planning. Our recent works, [SPEX (OSDI'26)](https://arxiv.org/abs/2605.10195) and [HyPER (ICML'26)](https://arxiv.org/abs/2602.06527), improve inference-time scaling from two complementary angles. **SPEX** accelerates **Tree-of-Thought (ToT) reasoning** by breaking the *reward dependency barrier*—the synchronization bottleneck that serializes reward-guided search. It speculatively expands high-potential branches (intra-query speculative selection), balances speculative compute across concurrent queries (inter-query budget allocation), and prunes redundant deep branches (adaptive early termination), delivering up to 3× speedups (and up to 4.1× when combined with speculative decoding) without sacrificing accuracy. **HyPER** targets **multi-path Chain-of-Thought (CoT) reasoning**, reformulating test-time scaling as a training-free *expand–reduce* control problem that dynamically shifts from exploration to exploitation over a pool of hypotheses, improving accuracy by 8–10% while cutting token usage by 25–40%.

**Memory:** To provide long-term learning and context retention, the agent includes a dedicated Memory module. We have designed **an Efficient Agent Memory System**, also under review, that supports accurate, low-latency storage and retrieval of relevant information, ensuring continuity and coherence across extended interactions.

<br>


## 4. Disaggregated Memory Infrastructure

---

<div style="text-align: center;">
  <img src="https://pfzuo.github.io/assets/img/project-dm.jpg" alt="Disaggregated Memory Infrastructure" width="500">
</div>

<br>

This project aims to build a robust and high-performance infrastructure for disaggregated memory, enabling applications to efficiently access large, distributed memory pools as a unified resource. By decoupling memory from compute, our architecture offers significant improvements in resource utilization, scalability, and cost-efficiency for data-intensive services. The infrastructure is designed as a three-layer stack, with foundational research contributions at each level.

**Memory Pooling Layer (Foundation):** At the bottom layer, we address the core challenges of creating a scalable and reliable memory pool from distributed machines. Our work in this area includes foundational techniques for distributed transactions ([FORD@FAST'22](https://www.usenix.org/system/files/fast22-zhang-ming.pdf)), efficient memory management ([FUSEE@FAST'23](https://www.usenix.org/system/files/fast23-shen.pdf)), robust failure tolerance ([Aceso@SOSP'24](https://dl.acm.org/doi/10.1145/3694715.3695951)), and scalable cluster membership management ([uKaron@USENIX ATC'22](https://www.usenix.org/system/files/atc22-guerraoui.pdf)). These components provide the fundamental building blocks for a scalable disaggregated memory pool.

**Indexing Layer (Data Access):** Built on top of the memory pool, the indexing layer provides scalable and high-performance mechanisms for organizing and accessing data. We have explored a diverse range of indexing strategies to suit different data structures and access patterns, including hashing ([RACE@USENIX ATC'21](https://www.usenix.org/system/files/atc21-zuo.pdf)), tree-based ([SMART@OSDI'23](https://www.usenix.org/conference/osdi23/presentation/luo)), learned ([ROLEX, Best Paper@FAST '23](https://www.usenix.org/conference/fast23/presentation/li-pengfei)), and hybrid ([CHIME@SOSP'24](https://arxiv.org/abs/2405.20831)) indexes. This layer ensures that applications can retrieve data from the vast memory pool with low latency.

**System Service Layer (Application):** The top layer exposes the capabilities of the disaggregated memory infrastructure to applications. Our key service is [Ditto (SOSP'23)](https://dl.acm.org/doi/10.1145/3600006.3613144), a disaggregated memory caching system that provides a powerful caching solution for applications. This layer also directly supports demanding workloads such as OLTP, HTAP, and vector databases, allowing them to leverage the full benefits of a large, fast, and disaggregated memory pool.

Together, these layers form a complete and principled solution for building next-generation disaggregated datacenter infrastructure, enabling more efficient and powerful data-intensive applications.


<br>


## 5. Persistent Memory Systems and Architectures

---

<div style="text-align: center;">
  <img src="https://pfzuo.github.io/assets/img/project-nvm.jpg" alt="Persistent Memory System and Architecture" width="600">
</div>
<br>

With the increasing number of processor cores and the emergence of data-intensive applications, the demand for large-capacity main memory is growing. While DRAM is the primary main memory, its scalability and energy efficiency limit further capacity expansion. Non-volatile memory (NVM), with high scalability and energy efficiency, is a promising next-generation main memory. However, modern computer systems are optimized for DRAM, so adopting NVM introduces challenges in write endurance, data persistence, and security. NVM cells have limited write endurance, data must be persisted to guarantee crash consistency, and retaining data after power-off raises security concerns for edge devices. This dissertation addresses these challenges and proposes efficient solutions for both general and encrypted NVMs.

For general NVM, this dissertation proposes two hash-based structures. 1) [Path Hashing (MSST'17)](https://csyhua.github.io/csyhua/hua-MSST2017-NVM.pdf): A write-optimized hash index that leverages position sharing, double-path hashing, and path shortening to eliminate extra writes while achieving high space utilization (up to 95%) and low latency. 2) [Level Hashing (OSDI'18)](https://www.usenix.org/conference/osdi18/presentation/zuo): A persistent hash index that guarantees crash consistency with log-free schemes and efficient in-place resizing, achieving 1.4–3× speedup in insertions, 1.2–2.1× in updates, and over 4.3× in resizing compared to state-of-the-art methods.

For encrypted NVM, this dissertation proposes two architectures. 1) [DeWrite (MICRO'18)](https://ieeexplore.ieee.org/document/8595424): A write-optimized memory system that combines lightweight cache-line deduplication with opportunistic parallel encryption, reducing writes by 54%, accelerating reads/writes by 3.1–4.2×, and lowering energy consumption by 40%. 2) [SuperMem (MICRO'19)](https://dl.acm.org/doi/10.1145/3352460.3358290): A persistent secure NVM architecture using a write-through counter cache, locality-aware counter write coalescing (CWC), and cross-bank counter storage (XBank) to guarantee consistency while improving performance; CWC reduces up to 50% of writes, and XBank achieves up to 2× speedup.

These contributions collectively enhance the endurance, performance, crash consistency, and security of both un-encrypted and encrypted NVMs.

<br><br>



{% if site.enable_project_categories and page.display_categories %}
  <!-- Display categorized projects -->
  {% for category in page.display_categories %}
  <a id="{{ category }}" href=".#{{ category }}">
    <h2 class="category">{{ category }}</h2>
  </a>
  {% assign categorized_projects = site.projects | where: "category", category %}
  {% assign sorted_projects = categorized_projects | sort: "importance" %}
  <!-- Generate cards for each project -->
  {% if page.horizontal %}
  <div class="container">
    <div class="row row-cols-1 row-cols-md-2">
    {% for project in sorted_projects %}
      {% include projects_horizontal.liquid %}
    {% endfor %}
    </div>
  </div>
  {% else %}
  <div class="row row-cols-1 row-cols-md-3">
    {% for project in sorted_projects %}
      {% include projects.liquid %}
    {% endfor %}
  </div>
  {% endif %}
  {% endfor %}

{% else %}

<!-- Display projects without categories -->

{% assign sorted_projects = site.projects | sort: "importance" %}

  <!-- Generate cards for each project -->

{% if page.horizontal %}

  <div class="container">
    <div class="row row-cols-1 row-cols-md-2">
    {% for project in sorted_projects %}
      {% include projects_horizontal.liquid %}
    {% endfor %}
    </div>
  </div>
  {% else %}
  <div class="row row-cols-1 row-cols-md-3">
    {% for project in sorted_projects %}
      {% include projects.liquid %}
    {% endfor %}
  </div>
  {% endif %}
{% endif %}
