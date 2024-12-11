# Profile Kernels using NVIDIA Nsight Compute

This tutorial provides instructions on profiling CUDA kernels written in Julia using NVIDIA Nsight Compute. The instructions are based on a local Windows system (and similarly apply to Linux and macOS, including both remote and local systems) and use the VS Code platform.

## Prerequisite

Make sure to download the version of NVIDIA Nsight Compute that is compatible with your current NVIDIA driver.

- [NVIDIA Nsight Compute - Get Started](https://developer.nvidia.com/tools-overview/nsight-compute/get-started) 

## Connect Externel Julia REPL

First, we start by launching a Julia session under the Nsight Compute CLI using the following command:
```bash
> ncu --mode=launch julia
```

Then, we will enter a Julia REPL showing that it is waiting for a profiler to attach. To better support kernel optimization, we recommend connecting this REPL to your current development IDE. Please note that this Julia REPL (i.e., the terminal, which is commonly referred to as such in IDE platforms) is considered an external REPL with respect to the IDE.

We are now taking the VS Code as our example. 

In the command palette, search for `Julia: Connect external REPL` and select it. This will automatically copy some lines of code to your clipboard. Execute these lines in the external REPL we have already launched, and the connection to the external REPL will be successful.

## Attach Profiler to Julia Process

Now we are ready to attach the externel profiler (i.e., Nsight Compute) to the existing Julia process.

In the Nsight Compute GUI, select `Connection > Start Activity` and a new small windows will show up. Select


## Start GPU Kernel Profiling

Assume you have a example.jl file that contains CUDA kerenls you may would like to profliing.


## References

Profiling GPU code in CUDA.jl.
https://cuda.juliagpu.org/stable/development/profiling/

NVIDIA Nsight Systems user guide.
https://docs.nvidia.com/nsight-systems/UserGuide/index.html

