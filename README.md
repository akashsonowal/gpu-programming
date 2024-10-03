# gpu-programming

# NVIDIA vs ATI

# Graphics: DirectX vs OpenGL

# Only Processing: CUDA vs OpenCL vs Microsoft AMP (for windows only)

GPU has an array of SMs. Each SM has cores a.k.a. (cuda cores / shader units / streming processors)

Each SM have SP. and in each SM there are memory registers used by SP. Registers are local to each SMs however it can't be used by all cores/SP. A SM can have many registers. Shared memory is used for i/o by all SP in a SM. There are also other memories like constant memory and texture memory from which SP can read from.

Note: There is device memory which can be used by all SMs.

Compute Capibility tells a lots of paramters. But If you are looking for only prcessing then look at peak FLOPS.

Install Nvidia Nsight in vscode for debugging and profiling

PTX (Parallel Thread Execution) is assembly of CUDA
