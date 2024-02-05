---
title: Hello World
category: [default, cxl]
---

# Hello World!

Welcome to my first blog post! In this post, I will be sharing a simple C program that prints "Hello, World!".

## The Program

```c
#include <stdio.h>

int main() {
    printf("Hello, World!\n");
    return 0;
}

```

## CUDA exmaple

```c
#include <stdio.h>

__global__ void matrixAdd(int *a, int *b, int *c, int size) {
    int tid = blockIdx.x * blockDim.x + threadIdx.x;
    if (tid < size) {
        c[tid] = a[tid] + b[tid];
    }
}

int main() {
    int size = 100;
    int a[size], b[size], c[size];
    int *dev_a, *dev_b, *dev_c;

    // Allocate memory on the GPU
    cudaMalloc((void**)&dev_a, size * sizeof(int));
    cudaMalloc((void**)&dev_b, size * sizeof(int));
    cudaMalloc((void**)&dev_c, size * sizeof(int));

    // Initialize input matrices
    for (int i = 0; i < size; i++) {
        a[i] = i;
        b[i] = i;
    }

    // Copy input matrices from host to device
    cudaMemcpy(dev_a, a, size * sizeof(int), cudaMemcpyHostToDevice);
    cudaMemcpy(dev_b, b, size * sizeof(int), cudaMemcpyHostToDevice);

    // Launch kernel
    int threadsPerBlock = 256;
    int blocksPerGrid = (size + threadsPerBlock - 1) / threadsPerBlock;
    matrixAdd<<<blocksPerGrid, threadsPerBlock>>>(dev_a, dev_b, dev_c, size);

    // Copy result matrix from device to host
    cudaMemcpy(c, dev_c, size * sizeof(int), cudaMemcpyDeviceToHost);

    // Print result matrix
    for (int i = 0; i < size; i++) {
        printf("%d ", c[i]);
    }
    printf("\n");

    // Free memory on the GPU
    cudaFree(dev_a);
    cudaFree(dev_b);
    cudaFree(dev_c);

    return 0;
}
```


