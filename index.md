@def title = "Trixi-GPU Home"
@def tags = ["Trixi-GPU", "home"]

# Trixi-GPU

\toc

## About Trixi-GPU

Trixi-GPU offers GPU acceleration for solving hyperbolic PDEs. The core solvers are based on the [Trixi-Framework](https://trixi-framework.github.io/), with its acceleration powered by [JuliaGPU](https://juliagpu.org/). Currently, NVIDIA CUDA serves as our primary and experimental GPU acceleration support, and other types of GPU support will be implemented in the future.

## TrixiCUDA.jl

TrixiCUDA.jl offers CUDA acceleration for solving hyperbolic PDEs on GPUs. It is our top-priority solution for achieving high acceleration in solving PDEs on GPUs.

### Recent Update

*Update on Dec 31, 2024*:
- The initial round of kernel optimization starts with the volume integral kernels (see [TrixiCUDA.jl PR #102](https://github.com/trixi-gpu/TrixiCUDA.jl/pull/102)) and will later extend to all existing kernels used in the semidiscretization process. The primary approach includes improving global memory access patterns, using shared memory, and selecting appropriate launch sizes to reduce warp stalls and achieve better occupancy.

*Update on Nov 21, 2024*: 
- Due to the [issue](https://github.com/trixi-framework/Trixi.jl/issues/2108) from upstream with Trixi.jl and CUDA.jl in Julia v1.11, this package now supports only Julia v1.10. Using or developing this package with Julia v1.11 will result in precompilation errors. To fix this, downgrade to Julia v1.10. If you have any other problems, please file issues [here](https://github.com/trixi-gpu/TrixiCUDA.jl/issues).

*Update on Oct 30, 2024*: 
- The general documentation is now available at [https://trixi-gpu.github.io](https://trixi-gpu.github.io) (in development).  
- Documentation specific to this package can be found at [https://trixi-gpu.github.io/TrixiCUDA.jl/dev](https://trixi-gpu.github.io/TrixiCUDA.jl/dev) (in development).

[*Archived Update*](/update)

## Acceleration Overview

### CPU and GPU Data Flow

~~~
<div class="row">
  <div class="container">
    <img class="left" src="/assets/index1.png">
    <div style="clear: both"></div>
  </div>
</div>
~~~

Minimizing large and frequent data transfers between the CPU and GPU is crucial for accelerating large programs. To reduce transfer overhead, initial values and large parameters are initialized and kept on the GPU throughout the solving process. Additionally, GPU-specific interfaces and custom kernels are implemented to speed up data initialization and processing.

### ODE and PDE Acceleration

~~~
<div class="row">
  <div class="container">
    <img class="left" src="/assets/index2.png">
    <div style="clear: both"></div>      
  </div>
</div>
~~~

The overall GPU acceleration relies on two parts: (1) ODE acceleration using standard kernels from the package, and (2) PDE-specific acceleration, focusing on semidiscretization, implemented with custom kernels. With custom kernels, specialized optimizations focused on memory access and algorithms can be applied to achieve further speedup.

### Smediscretization on GPU

~~~
<div class="row">
  <div class="container">
    <img class="left" src="/assets/index3.png">
    <div style="clear: both"></div>      
  </div>
</div>
~~~

Semidiscretization is a key part of acceleration due to its potential for full parallelization and the weak data dependencies between some functionalities. Thus, running it on the GPU with pipelined streams is an effective approach to achieving high speedup. But some data dependencies force certain functionalities to remain sequential, making it hard to achieve more intensive pipelining.

## News

There is a new project that probably involves the parallelization of mesh initialization process in solving PDEs using CUDA.jl (or other available GPU packages in Julia) for the upcoming [Google Summer of Code 2025](https://summerofcode.withgoogle.com/).

## Acknowledgments

Thanks to our developers, maintainers, and outside contributors for their contributions to our community. Also, special thanks to Prof. Hendrik Ranocha, Prof. Jesse Chan, and Prof. Michael Schlottke-Lakemper for advising this project.