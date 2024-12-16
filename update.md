### Archived Update

*Update on Sep 16, 2024*:
- GPU-related tests are run now locally rather than on CI. Once the package is ready to publish, we will set up JuliaGPU CI infrastructure to run tests on a system with a GPU using [JuliaGPU Buildkite](https://github.com/JuliaGPU/buildkite).

*Update on Aug 5, 2024*:

- The original project repository has been refactored into a package named [TrixiCUDA.jl](https://github.com/trixi-gpu/TrixiCUDA.jl), primarily aimed at providing CUDA support for Trixi.jl. The package is currently under active development and testing. 

*Update on May 15, 2024*:

- Based on the discussion, the original naive GPU implementation is planned to be optimized in the following general ways:
    - Memory coalescing through shared memory 
    - Sparse matrix computation through CSC and CSR
    - Compensated summation algorithm
    The primary challenge of optimization is about precision and performance (i.e., speed). Further research is required to determine how to achieve high precision and high performance at the same time.

*Update on Apr 28, 2024*:

- GPU support requires type stability of `Float32` to achieve better performance. However, type stability for `Float32` is not supported in the upstream (i.e., Trixi.jl), which causes errors in some GPU kernels during compilation. We are now beginning to enhance `Float32` support in the upstream:
    - Support for the solvers (focused on `Trixi.rhs!`) has been completed. See [Trixi.jl PR #1909](https://github.com/trixi-framework/Trixi.jl/pull/1909) for all the related PRs.
    - Support for mesh initialization (such as `TreeMesh` and `StructuredMesh`) and callbacks is in progress. See [Trixi.jl PR #2042](https://github.com/trixi-framework/Trixi.jl/pull/2042) for all the discussion.





