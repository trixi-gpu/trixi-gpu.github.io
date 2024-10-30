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

### ODE and PDE GPU acceleration

~~~
<div class="row">
  <div class="container">
    <img class="left" src="/assets/index2.png">
    <div style="clear: both"></div>      
  </div>
</div>
~~~

### Smediscretization on GPU

~~~
<div class="row">
  <div class="container">
    <img class="left" src="/assets/index3.png">
    <div style="clear: both"></div>      
  </div>
</div>
~~~

## New section
