# Comparison of `rhs!` Performance: CPU vs. GPU

> This documentation serves as a supplementary material for JuliaCon 2025. \

See the benchmarking file at [benchmark.ipynb](https://github.com/trixi-gpu/TrixiCUDA.jl/blob/v0.1.0-rc.3/benchmark/benchmark.ipynb), and all results are compared between [TrixiCUDA.jl v0.1.0-rc.3](https://github.com/trixi-gpu/TrixiCUDA.jl/tree/v0.1.0-rc.3) and [Trixi.jl v0.11.17](https://github.com/trixi-framework/Trixi.jl/tree/v0.11.17). All the benchmark examples can be found in the [benchmark](https://github.com/trixi-gpu/TrixiCUDA.jl/tree/v0.1.0-rc.3/examples) directory.

We mainly show the mean and median times on CPU and GPU for each example, and include the degrees of freedom (DOFs) per field (i.e., per independent solution variable) in each plot, since DOFs are a dominant factor (though not the only factor) affecting computational time.

We provide the link to each example in Trixi.jl as it is a more mature and stable package compared to TrixiCUDA.jl. Note that performance varies with different inputs; these benchmark results are provided for reference only.

## Approaches

We adopt two approaches here: 
- First, we maintain a consistent solution resolution per space dimension by fixing both the degree of polynomial basis (i.e., `polydeg`) and mesh refinement level (i.e., `initial_refinement_level`), while varying the problem dimension from 1D to 2D to 3D. In this way, we observe a linear increase in log DOFs with problem dimension.
- Second, for each problem type, we keep the number of DOFs roughly constant across 1D, 2D, and 3D by changing the polynomial degree (i.e., `polydeg`) and mesh refinement level (i.e., `initial_refinement_level`). This way produces a roughly flat log DOFs curve across all dimensions.

We will present benchmark results for two approaches.

## Results

### Linear Advection Equation
Left: Basic linear advection equation ([1D](https://github.com/trixi-framework/Trixi.jl/blob/v0.11.17/examples/tree_1d_dgsem/elixir_advection_basic.jl), [2D](https://github.com/trixi-framework/Trixi.jl/blob/v0.11.17/examples/tree_2d_dgsem/elixir_advection_basic.jl), [3D](https://github.com/trixi-framework/Trixi.jl/blob/v0.11.17/examples/tree_3d_dgsem/elixir_advection_basic.jl))  \
Right: Linear advection equation with mortar method ([2D](https://github.com/trixi-framework/Trixi.jl/blob/v0.11.17/examples/tree_2d_dgsem/elixir_advection_mortar.jl), [3D](https://github.com/trixi-framework/Trixi.jl/blob/v0.11.17/examples/tree_3d_dgsem/elixir_advection_mortar.jl))

- First approach
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

- Second approach
~~~
<table style="background: transparent; border: none;">
  <tr>
    <td style="background: transparent; border: none;">
      <img src="/assets/benchmark/bench1_.png" style="width: 300px;">
    </td>
    <td style="background: transparent; border: none;">
      <img src="/assets/benchmark/bench2_.png" style="width: 300px;">
    </td>
  </tr>
</table>
~~~

### Compressible Euler Equations
Left: Compressible Euler equations with entropy-conservative flux ([1D](https://github.com/trixi-framework/Trixi.jl/blob/v0.11.17/examples/tree_1d_dgsem/elixir_euler_ec.jl), [2D](https://github.com/trixi-framework/Trixi.jl/blob/v0.11.17/examples/tree_2d_dgsem/elixir_euler_ec.jl), [3D](https://github.com/trixi-framework/Trixi.jl/blob/v0.11.17/examples/tree_3d_dgsem/elixir_euler_ec.jl))  
Right: Compressible Euler equations with shock capturing ([1D](https://github.com/trixi-framework/Trixi.jl/blob/v0.11.17/examples/tree_1d_dgsem/elixir_euler_shockcapturing.jl), [2D](https://github.com/trixi-framework/Trixi.jl/blob/v0.11.17/examples/tree_2d_dgsem/elixir_euler_shockcapturing.jl), [3D](https://github.com/trixi-framework/Trixi.jl/blob/v0.11.17/examples/tree_3d_dgsem/elixir_euler_shockcapturing.jl))

- Fisrt approach
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

- Second approach 
~~~
<table style="background: transparent; border: none;">
  <tr>
    <td style="background: transparent; border: none;">
      <img src="/assets/benchmark/bench3_.png" style="width: 300px;">
    </td>
    <td style="background: transparent; border: none;">
      <img src="/assets/benchmark/bench4_.png" style="width: 300px;">
    </td>
  </tr>
</table>
~~~

### Hyperbolic Diffusion Equations
Hyperbolic diffusion equations with non-periodic boundary conditions 
([1D](https://github.com/trixi-framework/Trixi.jl/blob/v0.11.17/examples/tree_1d_dgsem/elixir_hypdiff_nonperiodic.jl), [2D](https://github.com/trixi-framework/Trixi.jl/blob/v0.11.17/examples/tree_2d_dgsem/elixir_hypdiff_nonperiodic.jl), [3D](https://github.com/trixi-framework/Trixi.jl/blob/v0.11.17/examples/tree_3d_dgsem/elixir_hypdiff_nonperiodic.jl))

- First approach
~~~
<div align="center">
  <img src="/assets/benchmark/bench8.png" style="width: 300px;">
</div>
~~~

- Second approach
~~~
<div align="center">
  <img src="/assets/benchmark/bench8_.png" style="width: 300px;">
</div>
~~~

### Ideal GLM-MHD Equations
Upper: Ideal GLM-MHD equations with entropy-conservative flux  
([1D](https://github.com/trixi-framework/Trixi.jl/blob/v0.11.17/examples/tree_1d_dgsem/elixir_mhd_ec.jl), [2D](https://github.com/trixi-framework/Trixi.jl/blob/v0.11.17/examples/tree_2d_dgsem/elixir_mhd_ec.jl), [3D](https://github.com/trixi-framework/Trixi.jl/blob/v0.11.17/examples/tree_3d_dgsem/elixir_mhd_ec.jl)) \
Lower left: Ideal GLM-MHD Alfven wave
([1D](https://github.com/trixi-framework/Trixi.jl/blob/v0.11.17/examples/tree_1d_dgsem/elixir_mhd_alfven_wave.jl), [2D](https://github.com/trixi-framework/Trixi.jl/blob/v0.11.17/examples/tree_2d_dgsem/elixir_mhd_alfven_wave.jl), [3D](https://github.com/trixi-framework/Trixi.jl/blob/v0.11.17/examples/tree_3d_dgsem/elixir_mhd_alfven_wave.jl)) \
Lower right: Ideal GLM-MHD Alfven wave with mortar method
([2D](https://github.com/trixi-framework/Trixi.jl/blob/v0.11.17/examples/tree_2d_dgsem/elixir_mhd_alfven_wave_mortar.jl), [3D](https://github.com/trixi-framework/Trixi.jl/blob/v0.11.17/examples/tree_3d_dgsem/elixir_mhd_alfven_wave_mortar.jl))

- First approach
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

- Second approach
~~~
<div align="center">
  <img src="/assets/benchmark/bench5_.png" style="width: 300px;">
</div>
~~~
~~~
<table style="background: transparent; border: none;">
  <tr>
    <td style="background: transparent; border: none;">
      <img src="/assets/benchmark/bench6_.png" style="width: 300px;">
    </td>
    <td style="background: transparent; border: none;">
      <img src="/assets/benchmark/bench7_.png" style="width: 300px;">
    </td>
  </tr>
</table>
~~~

### Shallow Water Equations
Left: Shallow water equations with entropy conservative flux ([1D](https://github.com/trixi-framework/Trixi.jl/blob/v0.11.17/examples/tree_1d_dgsem/elixir_shallowwater_ec.jl), [2D](https://github.com/trixi-framework/Trixi.jl/blob/v0.11.17/examples/tree_2d_dgsem/elixir_shallowwater_ec.jl)) \
Right: Shallow water equations with source terms ([1D](https://github.com/trixi-framework/Trixi.jl/blob/v0.11.17/examples/tree_1d_dgsem/elixir_shallowwater_source_terms.jl), [2D](https://github.com/trixi-framework/Trixi.jl/blob/v0.11.17/examples/tree_2d_dgsem/elixir_shallowwater_source_terms.jl))

- First approach
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

- Second approach
~~~
<table style="background: transparent; border: none;">
  <tr>
    <td style="background: transparent; border: none;">
      <img src="/assets/benchmark/bench9_.png" style="width: 300px;">
    </td>
    <td style="background: transparent; border: none;">
      <img src="/assets/benchmark/bench10_.png" style="width: 300px;">
    </td>
  </tr>
</table>
~~~

## Takeaway
In the first approach, CPU and GPU runtimes both rise as DOFs increase, simply because more unknowns must be solved; while in the second approach, even when the total DOFs are held roughly constant, CPU and GPU runtimes still increase with problem size, since the cost of solving each unknown also grows with the spatial dimension of the problem. 

However, in both approaches, we observe that the slope of the runtime on the GPU is smaller than that on the CPU, so the GPU is less sensitive to increases in data size and thus robust in handling large-scale problems. So, we can conclude that the speedup increases with the problem size (including both the number of spatial dimensions and the level of solution resolution).