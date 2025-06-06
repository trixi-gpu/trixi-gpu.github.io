### Archived Update

*Update on Dec 31, 2024*:
- The kernel optimization starts with the volume integral kernels (see [TrixiCUDA.jl PR #102](https://github.com/trixi-gpu/TrixiCUDA.jl/pull/102)) and will extend to all existing kernels used in the semidiscretization.

*Update on Nov 21, 2024*:
- Due to the [issue](https://github.com/trixi-framework/Trixi.jl/issues/2108) from upstream with Trixi.jl and CUDA.jl in Julia v1.11, this package now supports only Julia v1.10. Using or developing this package with Julia v1.11 will result in precompilation errors. To fix this, downgrade to Julia v1.10. If you have any other problems, please file issues [here](https://github.com/trixi-gpu/TrixiCUDA.jl/issues).

*Update on Oct 11, 2024*:
- Development on Julia v1.11 is currently on hold due to an [incompatibility issue](https://github.com/trixi-framework/Trixi.jl/issues/2108) between the latest version of CUDA.jl and Trixi.jl. The fix is in progress.
    - Trace the root issue in [Trixi.jl Issue #1789](https://github.com/trixi-framework/Trixi.jl/issues/1789): SciMLBase.jl has dropped support for arrays of `SVector`.
    - [Trixi.jl PR #2150](https://github.com/trixi-framework/Trixi.jl/pull/2150) is opened to replace arrays of `SVector` using RecursiveArrayTools.jl
    - It requires updating RecursiveArrayTools.jl, which is compatible with Julia >= v1.10. However, Trixi.jl has some legacy tests relying on Julia v1.8 and v1.9. See more discussions in [Trixi.jl PR #2194](https://github.com/trixi-framework/Trixi.jl/pull/2194). 

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





