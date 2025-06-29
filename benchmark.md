# Comparison of `rhs!` Performance: CPU vs. GPU

> This documentation serves as a supplementary material for JuliaCon 2025. \

See the benchmarking file at [benchmark.ipynb](https://github.com/trixi-gpu/TrixiCUDA.jl/blob/v0.1.0-rc.2/benchmark/benchmark.ipynb), and all results are compared between [TrixiCUDA.jl v0.1.0-rc.2](https://github.com/trixi-gpu/TrixiCUDA.jl/tree/v0.1.0-rc.2) and [Trixi.jl v0.11.17](https://github.com/trixi-framework/Trixi.jl/tree/v0.11.17).

We provide the link to each example in Trixi.jl as it is a more mature and stable package compared to TrixiCUDA.jl. Note that performance varies with different inputs; these benchmark results are provided for reference only.

## Linear Advection Equation
Left: Basic linear advection equation ([1D](https://github.com/trixi-framework/Trixi.jl/blob/v0.11.17/examples/tree_1d_dgsem/elixir_advection_basic.jl), [2D](https://github.com/trixi-framework/Trixi.jl/blob/v0.11.17/examples/tree_2d_dgsem/elixir_advection_basic.jl), [3D](https://github.com/trixi-framework/Trixi.jl/blob/v0.11.17/examples/tree_3d_dgsem/elixir_advection_basic.jl))  \
Right: Linear advection equation with mortar method ([2D](https://github.com/trixi-framework/Trixi.jl/blob/v0.11.17/examples/tree_2d_dgsem/elixir_advection_mortar.jl), [3D](https://github.com/trixi-framework/Trixi.jl/blob/v0.11.17/examples/tree_3d_dgsem/elixir_advection_mortar.jl))

~~~
<table style="background: transparent; border: none;">
  <tr>
    <td style="background: transparent; border: none;">
      <img src="/assets/benchmark/bench1.png" style="width: 300px;">
    </td>
    <td style="background: transparent; border: none;">
      <img src="/assets/benchmark/bench2.png" style="width: 300px;">
    </td>
  </tr>
</table>
~~~

## Compressible Euler Equations
Left: Compressible Euler equations with entropy-conservative flux ([1D](https://github.com/trixi-framework/Trixi.jl/blob/v0.11.17/examples/tree_1d_dgsem/elixir_euler_ec.jl), [2D](https://github.com/trixi-framework/Trixi.jl/blob/v0.11.17/examples/tree_2d_dgsem/elixir_euler_ec.jl), [3D](https://github.com/trixi-framework/Trixi.jl/blob/v0.11.17/examples/tree_3d_dgsem/elixir_euler_ec.jl))  
Right: Compressible Euler equations with shock capturing ([1D](https://github.com/trixi-framework/Trixi.jl/blob/v0.11.17/examples/tree_1d_dgsem/elixir_euler_shockcapturing.jl), [2D](https://github.com/trixi-framework/Trixi.jl/blob/v0.11.17/examples/tree_2d_dgsem/elixir_euler_shockcapturing.jl), [3D](https://github.com/trixi-framework/Trixi.jl/blob/v0.11.17/examples/tree_3d_dgsem/elixir_euler_shockcapturing.jl))

~~~
<table style="background: transparent; border: none;">
  <tr>
    <td style="background: transparent; border: none;">
      <img src="/assets/benchmark/bench3.png" style="width: 300px;">
    </td>
    <td style="background: transparent; border: none;">
      <img src="/assets/benchmark/bench4.png" style="width: 300px;">
    </td>
  </tr>
</table>
~~~

## Hyperbolic Diffusion Equations
Hyperbolic diffusion equations with non-periodic boundary conditions 
([1D](https://github.com/trixi-framework/Trixi.jl/blob/v0.11.17/examples/tree_1d_dgsem/elixir_hypdiff_nonperiodic.jl), [2D](https://github.com/trixi-framework/Trixi.jl/blob/v0.11.17/examples/tree_2d_dgsem/elixir_hypdiff_nonperiodic.jl), [3D](https://github.com/trixi-framework/Trixi.jl/blob/v0.11.17/examples/tree_3d_dgsem/elixir_hypdiff_nonperiodic.jl))

~~~
<div align="center">
  <img src="/assets/benchmark/bench8.png" style="width: 300px;">
</div>
~~~

## Ideal GLM-MHD Equations
Upper: Ideal GLM-MHD equations with entropy-conservative flux  
([1D](https://github.com/trixi-framework/Trixi.jl/blob/v0.11.17/examples/tree_1d_dgsem/elixir_mhd_ec.jl), [2D](https://github.com/trixi-framework/Trixi.jl/blob/v0.11.17/examples/tree_2d_dgsem/elixir_mhd_ec.jl), [3D](https://github.com/trixi-framework/Trixi.jl/blob/v0.11.17/examples/tree_3d_dgsem/elixir_mhd_ec.jl)) \
Lower left: Ideal GLM-MHD Alfven wave
([1D](https://github.com/trixi-framework/Trixi.jl/blob/v0.11.17/examples/tree_1d_dgsem/elixir_mhd_alfven_wave.jl), [2D](https://github.com/trixi-framework/Trixi.jl/blob/v0.11.17/examples/tree_2d_dgsem/elixir_mhd_alfven_wave.jl), [3D](https://github.com/trixi-framework/Trixi.jl/blob/v0.11.17/examples/tree_3d_dgsem/elixir_mhd_alfven_wave.jl)) \
Lower right: Ideal GLM-MHD Alfven wave with mortar method
([2D](https://github.com/trixi-framework/Trixi.jl/blob/v0.11.17/examples/tree_2d_dgsem/elixir_mhd_alfven_wave_mortar.jl), [3D](https://github.com/trixi-framework/Trixi.jl/blob/v0.11.17/examples/tree_3d_dgsem/elixir_mhd_alfven_wave_mortar.jl))

~~~
<div align="center">
  <img src="/assets/benchmark/bench5.png" style="width: 300px;">
</div>
~~~
~~~
<table style="background: transparent; border: none;">
  <tr>
    <td style="background: transparent; border: none;">
      <img src="/assets/benchmark/bench6.png" style="width: 300px;">
    </td>
    <td style="background: transparent; border: none;">
      <img src="/assets/benchmark/bench7.png" style="width: 300px;">
    </td>
  </tr>
</table>
~~~

## Shallow Water Equations
Left: Shallow water equations with entropy conservative flux ([1D](https://github.com/trixi-framework/Trixi.jl/blob/v0.11.17/examples/tree_1d_dgsem/elixir_shallowwater_ec.jl), [2D](https://github.com/trixi-framework/Trixi.jl/blob/v0.11.17/examples/tree_2d_dgsem/elixir_shallowwater_ec.jl)) \
Right: Shallow water equations with source terms ([1D](https://github.com/trixi-framework/Trixi.jl/blob/v0.11.17/examples/tree_1d_dgsem/elixir_shallowwater_source_terms.jl), [2D](https://github.com/trixi-framework/Trixi.jl/blob/v0.11.17/examples/tree_2d_dgsem/elixir_shallowwater_source_terms.jl))

~~~
<table style="background: transparent; border: none;">
  <tr>
    <td style="background: transparent; border: none;">
      <img src="/assets/benchmark/bench9.png" style="width: 300px;">
    </td>
    <td style="background: transparent; border: none;">
      <img src="/assets/benchmark/bench10.png" style="width: 300px;">
    </td>
  </tr>
</table>
~~~

## Takeaway
For simple cases (for example, if the CPU performance is less than 100 μs), it is not advantageous to run on the GPU, since the overhead of using the GPU outweighs any performance gain. However, for more complex cases (such as when execution time on the CPU exceeds 1,000 μs), running on the GPU can provide significant benefits.