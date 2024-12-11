+++
title = "Trixi-GPU Tutorial"
hascode = true
rss_pubdate = Date(2024, 10, 29)
tags = ["trixi-gpu", "tutorial"]
description = "Hands-on tutorials for Trixi-GPU"
+++

# Hands-on Tutorials

\toc

## Prepare GPUs on Cloud

Not everyone has access to a personal or privately owned GPU. This tutorial is designed to help you set up a GPU in the cloud. It is perfect for those without access to a physical GPU or anyone interested in easily trying different types of GPUs. There are many cloud platforms to choose from, such as AWS, GCP, and Azure, each of which is worth trying. AWS Cloud is used as an example in this tutorial.

[Setup a Cloud GPU for Running CUDA.jl](./cloud_gpu/)

## About Profiling

Both Nsight Systems and Nsight Compute are powerful tools for profiling. Nsight Systems excels at providing a high-level overview of system-wide performance, helping developers analyze application behavior and detect bottlenecks across CPU, GPU, and I/O. On the other hand, Nsight Compute is more focused on in-depth kernel analysis, offering detailed metrics like cache utilization, memory bandwidth, and warp execution efficiency. 

[System-wide Profiling using NVIDIA Nsight Systems](./nsys_profiling/) - *Currently unavailable due to the [NVTX issue on Windows](https://github.com/NVIDIA/NVTX/issues/107#issuecomment-2520453798), please wait for an update*\\

[Profiling kernels using NVIDIA Nsight Compute](./ncu_profiling/)

