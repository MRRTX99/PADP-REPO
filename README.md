# PADP-REPO
# Parallel and Distributed Programming (PADP) - Program Collection

## Overview
This repository contains seven programs related to **Parallel and Distributed Programming (PADP)**. Each program demonstrates different parallel computing paradigms using **OpenMP, MPI, OpenACC, and OpenCL/CUDA** for efficient parallel execution.

## Programs and Their Descriptions

### **1. Parallel Image Processing with OpenMP (Program1)**
- Uses **OpenMP** to apply color transformations (grayscale, red-scale, green-scale, blue-scale) on a PNG image.
- Implements parallel pixel manipulation using **OpenMP parallel for loops**.
- Uses the **GD graphics library** for image manipulation.

### **2. MPI-Based Message Passing (Program2)**
- Uses **MPI (Message Passing Interface)** to demonstrate inter-process communication.
- Each process (except the root) sends a predefined message to the root process.
- The root process receives and prints messages from all other processes.

### **3. Parallel Word Count using OpenMP (Program3)**
- Uses **OpenMP** for parallel word frequency counting in a text file.
- Multiple threads scan the file for predefined words and count their occurrences.
- Demonstrates parallel text processing with OpenMP **reduction**.

### **4. OpenACC-Based Jacobi Iteration (Program4)**
- Implements the **Jacobi iterative method** for solving partial differential equations.
- Uses **OpenACC** directives to accelerate computations on GPUs.
- Demonstrates data parallelism in scientific computing applications.

### **5. CUDA/OpenCL-Based Sobel Edge Detection (Program5)**
- Uses **CUDA/OpenCL** to implement the **Sobel edge detection** algorithm.
- Performs real-time image edge detection using parallel GPU execution.
- Demonstrates efficient memory access patterns in GPU programming.

### **6. OpenMP-Based Prime Number Sieve (Program6)**
- Implements different versions of **Sieve of Eratosthenes** for prime number calculation.
- Compares sequential, optimized, and parallelized versions using **OpenMP**.
- Demonstrates shared memory parallel computing for mathematical problems.

### **7. Parallel Depth Estimation using CUDA/OpenCL (Program7)**
- Uses **CUDA/OpenCL** for **real-time single-image depth estimation**.
- Implements **ResNet-50 for feature extraction** and **DenseNet for depth prediction**.
- Outputs results in `.PLY` format for 3D visualization.

## Compilation and Execution Instructions (GENERAL COMMANDs)
Each program has different dependencies and execution methods. Below are the general steps:

### **1. Compiling OpenMP Programs (Program1, Program3, Program6)**
```bash
gcc -fopenmp program.c -o program.out
./program.out
```

### **2. Compiling MPI Programs (Program2)**
```bash
mpicc program.c -o program.out
mpirun -np 4 ./program.out
```

### **3. Compiling OpenACC Programs (Program4)**
```bash
pgcc -acc -o program.out program.c
./program.out
```

### **4. Compiling CUDA Programs (Program5, Program7)**
```bash
nvcc program.cu -o program.out
./program.out
```

## Dependencies
- **OpenMP** (GCC or Clang)
- **MPI** (`mpicc`, `mpirun`)
- **OpenACC** (`pgcc` or `nvhpc`)
- **CUDA** (NVIDIA GPU, CUDA Toolkit)
- **OpenCL** (AMD/NVIDIA drivers)
- **GD Library** (for image processing)

## Conclusion
This collection of programs demonstrates key concepts in **parallel and distributed programming** using **OpenMP, MPI, OpenACC, CUDA, and OpenCL**. The examples cover **image processing, numerical computation, message passing, text analysis, and machine learning-based depth estimation**.

For more details, refer to individual program files and comments within the code.

---
**Author:** Sadiq Wahid  
**Date:** March 2025  
