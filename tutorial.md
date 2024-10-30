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

Some people may not have direct access to a personal or privately owned GPU. This tutorial is designed to help you set up a GPU in the cloud. It's perfect for those without access to a physical GPU or anyone interested in easily trying different types of GPUs. There are many cloud platforms to choose from, such as AWS, GCP, and Azure. This tutorial focuses on using AWS Cloud for running CUDA.jl.

[Setup a Cloud GPU for Running CUDA.jl](./cloud_gpu/)

## About Kernel Profiling

Kernel profilig is the most direct way to let developer/user to know the inner issues when perforamce are not ideal, for example, the cache hit and data transfer.

[Profiling CUDA kernel using Nsight Compute](./nsys_profiling/)

