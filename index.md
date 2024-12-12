@def title = "Trixi-GPU Home"
@def tags = ["Trixi-GPU", "home"]

# Trixi-GPU

\toc

## About Trixi-GPU

Trixi-GPU offers GPU acceleration for solving hyperbolic PDEs. The core solvers are based on the [Trixi-Framework](https://trixi-framework.github.io/), with its acceleration powered by [JuliaGPU](https://juliagpu.org/). Currently, NVIDIA CUDA serves as our primary but experimental GPU acceleration support, and other types of GPU support will be implemented in the future.

[Trixi-GPU on GitHub](https://github.com/trixi-gpu)

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

There is a new project that likely involves the parallelization of mesh initialization for solving PDEs using CUDA.jl (or other available GPU packages in Julia) for the upcoming [Google Summer of Code 2025](https://summerofcode.withgoogle.com/).

## Acknowledgments

Thanks to our developers, maintainers, and outside contributors for their contributions to our community.