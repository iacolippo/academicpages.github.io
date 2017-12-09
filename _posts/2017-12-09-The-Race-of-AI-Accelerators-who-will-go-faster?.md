---
title: 'The race of AI accelerators: who will go faster?'
date: 2017-12-09
permalink: /posts/2017/12/the-race-of-AI-accelerators-who-will-go-faster/
tags:
  - deep learning
  - hardware
  - GPU
  - TPU
  - FPGA
  - NVIDIA
  - Google
---

> Software is eating the world and deep learning is eating software.

Realizing this is the first step to understand why all the big companies are competing in a race to build their hardware solution to accelerate training and prediction in deep neural networks.

<h2>The rules of the race</h2>

Deep learning models are very powerful, but costly. Different challenges must be addressed.

1. **Speed**: long training time limits productivity.
2. **Size**: large model size stops mobile deployment.
3. **Power**: a GPU training deep networks is enough to heat a room.

These problems will be somewhat mitigated by advances in the algorithms (i.e. in the software). 
The main hardware problem to solve is efficient memory access.
    
<h2>The contestants</h2>

1. **NVIDIA** is leading the race at the moment, they won't stop working on improving **GPUs** and their stock has skyrocketed in the past few years. The market is confident that NVIDIA will continue to have a central role in artificial intelligence hardware.
2. **Google** is working on **TPUs**, after a *v1* dedicated to inference <a href="https://www.wired.com/2017/04/building-ai-chip-saved-google-building-dozen-new-data-centers/" target="blank">saved them from building a dozen new datacenters</a>, *v2* will be able to handle both training and inference workloads.
3. **Xilinx**, **Microsoft** and **Mipsology** are working on **FPGAs**, which are a nice way to reduce power requirements, but may be lacking in flexibility.
4. **Intel** has bet on **Nervana** and **Movidius**. The Intel Nervana **Neural Network Processor** has a new memory architecture and adopts a new numeric format called flexpoint; the Movidius **Neural Compute Stick** features a dedicated Neural Compute Engine for computer vision applications.
5. **GraphCore** is building an **Intelligence Processing Unit** (IPU). They have released some <a href="https://www.graphcore.ai/posts/preliminary-ipu-benchmarks-providing-previously-unseen-performance-for-a-range-of-machine-learning-applications" target="blank">preliminary benchmarks</a> and shown <a href="https://twitter.com/jwangARK/status/937806283117281280" target="blank">some others at NIPS2017</a>.
6. **Wave Computing** proposes a **Dataflow Processing Unit** (DPU). A <a href="https://wavecomp.ai/dataflow-whitepaper" target="blank">whitepaper</a> is available with technical details.
7. **Vathys.ai** introduces a complete rethink of the processor, deisgned for deep learning.<a href="http://web.stanford.edu/class/ee380/Abstracts/171206-slides.pdf" target="blank">These slides from a presentation at Stanford</a> enter in a lot of details and make comparisons with competitors.

**Apple**, **Huawei**, **Tesla** and many others are also in this race.

<h3>Who will go faster?</h3>