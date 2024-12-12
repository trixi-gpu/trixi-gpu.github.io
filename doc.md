+++
title = "Trixi-GPU Documentation"
hascode = false
rss_pubdate = Date(2024, 10, 29)
tags = ["trixi-gpu", "doc"]
description = "Archived documentation for Trixi-GPU"
+++

# Archived Documentation

\toc

## Recent Announcements

#### *Aug 5, 2024*

The original project repository has been refactored into a dependent package named [TrixiCUDA.jl](https://github.com/trixi-gpu/TrixiCUDA.jl), primarily aimed at providing CUDA support for Trixi.jl. GPU-related tests are now conducted locally due to constrained resources, and it will enable remote GPU CI testing using [JuliaGPU Buildkite](https://github.com/JuliaGPU/buildkite). The package is currently under active development and testing. 

Update: Development on Julia v1.11 is currently on hold due to an [incompatibility issue](https://github.com/trixi-framework/Trixi.jl/issues/2108) between the new CUDA.jl and Trixi.jl. The fix is in progress.

#### *May 15, 2024*

Based on the discussion, the original naive GPU implementation is planned to be optimized in the following general ways:
- Memory coalescing through shared memory 
- Sparse matrix computation through CSC and CSR
- Compensated summation algorithm

The primary challenge of optimization is about precision and performance (i.e., speed). Further research is required to determine how to achieve high precision and high performance at the same time.

#### *Apr 28, 2024*

GPU support requires type stability of `Float32` to achieve better performance. However, type stability for `Float32` is not supported in the upstream (i.e., Trixi.jl), which causes errors in some GPU kernels during compilation. We are now beginning to enhance `Float32` support in the upstream:
- Support for the solvers (focused on `Trixi.rhs!`) has been completed. See [PR#1909](https://github.com/trixi-framework/Trixi.jl/pull/1909) for all the related PRs.
- Support for mesh initialization (such as `TreeMesh` and `StructuredMesh`) and callbacks is in progress. See [PR#2042](https://github.com/trixi-framework/Trixi.jl/pull/2042) for all the discussion.


## Google Summer of Code

**Rounding Error Analysis in Weak Form Kernel for 1D Equation on GPU** \
*April 9, 2024* \
[PDF - Rounding Error Analysis](/assets/files/round_error.pdf) \
[PDF - Supplementary Proofs](/assets/files/proof_supply.pdf)

**GPU Programming Optimization: Flow Divergence, Memory Coalescing, and Sparse Matrix Computation** \
*December 19, 2023*  \
[Slides - Optimization Presentation](/assets/files/gsoc_present.pdf) \


**GPU Acceleration for PDE Discretization in Trixi.jl Using CUDA.jl (GSoC Report)**  \
*August 31, 2023*  \
[Web - Project on GSoC](https://summerofcode.withgoogle.com/programs/2023/projects/upstR7K2)  \
[Web - Report on Trixi](https://trixi-framework.github.io/outreach/gsoc/2023/gpu-acceleration-in-trixi-jl-using-cuda-jl/)  \
[GitHub Repository - TrixiCUDA.jl](https://github.com/huiyuxie/trixi_cuda)

**GPU Acceleration for PDE Discretization in Trixi.jl Using CUDA.jl (GSoC Proposal)**  \
*April 3, 2023* \
[PDF - GSoC Proposal](/assets/files/proposal.pdf)

**Matrix-Vector Representation of Discretization in 1D Linear Advection Equation**  \
*April 2, 2023* \
[PDF - Matrix-Vector Representation](/assets/files/vector_matrix.pdf)  \
[GitHub Repository - Linear Advection CUDA](https://github.com/huiyuxie/linear_advection_cuda)
