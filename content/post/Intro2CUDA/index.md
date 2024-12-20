---
title: Intro 2 CUDA
subtitle: 
# Summary for listings and search engines
summary: Basic Driver API
# Link this post with a project
projects: []

# Date published
date: '2023-12-12T00:00:00Z'

# Date updated
lastmod: '2023-12-12T00:00:00Z'

# Is this an unpublished draft?
draft: false

# Show this page in the Featured widget?
featured: false

# Featured image
# Place an image named `featured.jpg/png` in this page's folder and customize its options here.

authors:
  - Zi-Qi Lu

tags:
  - Academic
  - 开源

categories:
  - Tutorial
  - 教程
---
# Intro 2 CUDA

## Streams

### Page-Locked Host Memory

```cuda
cudaHostAlloc((void**)&a, N*sizeof(int), cudaHostAllocDefault);
cudaFreeHost(a);
```

page-locked / pinned host memory:
os guarantees that the memory is resident in physical memory and won't be paged out to disk.

simultaneously pinned memory opt out of the feature of virtual memory.

### Multiple Streams

```cuda
cudaStream_t stream1, stream2;
cudaStreamCreate(&stream1);
cudaStreamCreate(&stream2);
cudaMemcpyAsync(d_a, a, N*sizeof(int), cudaMemcpyHostToDevice, stream1);
cudaMemcpyAsync(d_b, b, N*sizeof(int), cudaMemcpyHostToDevice, stream2);
kernel<<<grid1, block1, 0, stream1>>>(d_a, N);
kernel<<<grid2, block2, 0, stream2>>>(d_b, N);
cudaStreamSynchronize(stream1);
cudaStreamSynchronize(stream2);
cudaStreamDestroy(stream1);
cudaStreamDestroy(stream2);
```

### GPU Work Schedule

Be aware of the GPU work schedule.
There are different execution units to execute different types of instructions, such as copy, compute, and so on.
And **the order of code dependencies is equal to the order written in the code**.

## Multi-GPU

### Zero-Copy Host Memory

```cuda
cudaHostAlloc((void**)&a, N*sizeof(int), cudaHostAllocWriteCombined | cudaHostAllocMapped);
```

cudaHostAllocWriteCombined: this flag indicates that the runtime should allocate the buffer as write-combined, which will not change functionality in application
but represents a performance enhancement for buffers that will be read only by the GPU.

Write-combined memory can be extremely inefficient in scenarios where CPU also needs to perform reads from the buffer.

cudaHostAllocMapped: the buffers can be accessed from the GPU. However, since there is a difference between the virtual address space of the CPU and the GPU,
the call to cudaHostAlloc() will return a CPU pointer, which is then mapped to a GPU pointer using cudaHostGetDevicePointer().

### Portable Pinned Memory

**This is neccesary when you use multiple GPUs.**

```cuda
cudaHostAlloc((void**)&a, N*sizeof(int), cudaHostAllocPortable);
```

When a buffer is allocated as pinned, they will only **appear** page-locked to the thread that allocated them. If another thread tries to access the buffer, they will see the buffer as  standard pageable memory.

To support portable pinned memory and zero-copy memory in multi-GPU systems, the code need two notable changes:

```c
void* function(void* arg) {
    if(arg->deviceID != 0) {
        cudaSetDevice(arg->deviceID);
        cudaSetDeviceFlags(cudaDeviceMapHost);
    }
}
```

We need a call to cudaSetDevice() to enable every thread controls  a different GPU.

In addition, as we use zero-copy in order to access these buffers directly from the GPU, we use cudaHostGetDevicePointer() to get the valid device pointers for the host memory.

```cuda
float *a, *b, *partial_c;
float *dev_a, *dev_b, *dev_partial_c;

//allocate memory on the CPU side
a = data->a;
b = data->b;
partial_c = (float *)malloc(blocksPerGrid *　sizeof(float));

cudaHostGetDevicePointer(&dev_a, a, 0);
cudaHostGetDevicePointer(&dev_b, b, 0);
cudaMalloc((void**)&dev_partial_c, blocksPerGrid * sizeof(float));

dev_a += data->offset;
dev_b += data->offset;

kernel<<<blocksPerGrid, threadsPerBlock>>>(dev_a, dev_b, dev_partial_c);
```
