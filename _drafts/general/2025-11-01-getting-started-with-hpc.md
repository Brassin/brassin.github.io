---
layout: post
title: "Getting Started with High-Performance Computing"
date: 2025-11-01
category: hpc
author: BrassinAI
excerpt: "An introduction to High-Performance Computing - from parallelism basics to GPU programming and distributed workloads."
---

This article covers the basics of **High-Performance Computing (HPC)**. From understanding parallelism to using GPUs efficiently, HPC remains the foundation of large-scale simulation and AI workloads.

{% include toc.html %}

## Why HPC Matters

Modern scientific computing, weather simulation, molecular dynamics, and deep learning all demand computational power far beyond what a single CPU core can provide. HPC is the discipline of harnessing thousands (or millions) of processing units to solve these problems. {% include sidenote.html text="The TOP500 list ranks the world's fastest supercomputers twice a year. As of 2024, Frontier at Oak Ridge holds the #1 spot at 1.2 exaFLOPS." ref="https://www.top500.org/" ref_title="TOP500 Supercomputer List" %}

## Core Concepts

### Parallelism

There are two fundamental types:

- **Data parallelism** - the same operation applied across different data chunks
- **Task parallelism** - different operations running concurrently

### Memory Models

| Model | Description |
|-------|-------------|
| Shared memory | All processors access the same memory (OpenMP) |
| Distributed memory | Each processor has its own memory (MPI) |
| Hybrid | Combines both (MPI + OpenMP) |

OpenMP is the de facto standard for shared-memory parallelism in C/C++ and Fortran. {% include sidenote.html text="OpenMP uses compiler directives (#pragma omp) to parallelize loops and sections, making it one of the lowest-friction ways to add parallelism to existing code." ref="https://www.openmp.org/specifications/" ref_title="OpenMP Specifications" %} MPI, on the other hand, handles distributed-memory communication across nodes. {% include sidenote.html text="MPI (Message Passing Interface) has been the backbone of distributed HPC since the early 1990s. The MPI-4.0 standard introduced persistent collectives and partitioned communication." ref="https://www.mpi-forum.org/docs/mpi-4.0/mpi40-report.pdf" ref_title="MPI 4.0 Standard" %}

## GPU Computing with CUDA

GPUs excel at data-parallel workloads. A simple CUDA kernel:

```c
__global__ void vectorAdd(float *a, float *b, float *c, int n) {
    int i = blockIdx.x * blockDim.x + threadIdx.x;
    if (i < n) c[i] = a[i] + b[i];
}
```

Key CUDA concepts:
1. **Threads** are organized into **blocks**
2. Blocks are organized into a **grid**
3. Shared memory within a block enables fast communication {% include sidenote.html text="CUDA shared memory is on-chip SRAM (~100 KB per SM on modern GPUs) with ~100× lower latency than global memory. Efficient use of shared memory is often the single biggest optimization lever." ref="https://docs.nvidia.com/cuda/cuda-c-programming-guide/" ref_title="CUDA C++ Programming Guide" %}

## Profiling & Optimization

{% capture note_profiling %}**Nsight Systems** provides a timeline view of GPU and CPU activity, making it easy to spot idle gaps and kernel launch overhead.

![Nsight timeline](https://developer.nvidia.com/sites/default/files/akamai/gameworks/Nsight_Systems_workspace.png)

This second paragraph demonstrates rich sidenotes with images, **bold**, *italic*, and `inline code`.{% endcapture %}

Before optimizing, measure. {% include sidenote.html text=note_profiling %}

Essential tools:

- `nvprof` / `Nsight Systems` - GPU profiling
- `perf` - CPU-level performance counters
- `gprof` - function-level profiling

> Premature optimization is the root of all evil, but late optimization is the root of all slow code.

## What's Next

Future posts will explore:

- MPI communication patterns
- CUDA memory hierarchy deep dive
- Distributed training with NCCL
- Profiling real AI workloads end to end
