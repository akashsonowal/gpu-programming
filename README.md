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

Thread blocks are scheduled to run on available SMs. This is done by scheduler.

Each SM executes one block at a time. Each block is divided into warps. Warps of a thread blocks are handled concurrently. 

Device Memory: Grid scope.....available to all threads in all blocks......cudaMalloc is dynamic memory allocation......for static memory allocation use __device__ int sum = 0; This memory is slow.

Constant and Texture Memory: __constant__ . It is fast provided all threads read from same location. Texture memory is more optimised for access (mostly used in game graphics). Constant memory is cached. so it is slightly faster.

Shared Memory: only within a thread block. It is very fast. <<<block, thread, share_mem>>>

in the kernel func: extern __shared__ int dcopy[];

dcopy[i * 2] = d[i * 2];

All the above memory is defined before kernel call

Register and Local Memory: per thread

for array use localmemory....abstraction but stored in global memory and inaccessible to others....that's why it slow than registers. Regsisters can only store single values.

Atomic operations makes sure we don't have race conditions in multiprocessing

Pinned and paged locked memory

# Events and Streams

Pinned memory is needed to use streams

## Events
Os timer (too much noise)
Profiler (times only kernel duration and other invocations)

## CPU has pageable memory (can be swapped to disk)

## But it can be pinned (pagebale locked) - stays in place: cudaHostAlloc() for pinned memory

CUDA Streams is a queue of GPU operations - Kernel lauch, memory copy

kernel<<<blocks, threads, shared_mem, streams>>>
