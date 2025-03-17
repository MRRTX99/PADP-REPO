# README - OpenACC Jacobi Solver

## Installation & Compilation

### **Compiling with OpenACC Support**

```sh
nvhpc/bin/nvc -fast -acc -Minfo=accel jacobi_openacc.c -o jacobi_acc
```

### **Compiling without OpenACC (for CPU Execution)**

```sh
gcc jacobi_openacc.c -o jacobi_cpu -lm
```

## Running the Program

```sh
./jacobi_acc
```

# README - OpenACC Parallel Jacobi Solver

## Introduction

This program implements a **Jacobi iterative method** for solving a 2D Poisson equation using OpenACC for parallelization. It solves a system of equations iteratively until convergence, which is determined by a tolerance (`TOL`). The solution is computed on a **1000x1000** grid.

## Problem Description

The Jacobi iterative method is used to solve the following equation:

```
u_new[i][j] = 0.25 * (u[i-1][j] + u[i+1][j] + u[i][j-1] + u[i][j+1] - f[i][j])
```

- **`u`** represents the solution matrix.
- **`f`** represents the right-hand side of the equation (set to `1.0` in this implementation).
- The grid updates each element based on the average of its neighbors, iterating until the difference between new and old values is below `TOL = 1e-6` or the number of iterations reaches `MAX_ITER = 1000`.

## Features

- **Parallelization with OpenACC** for optimized performance on GPUs.
- Uses **dynamic memory allocation** to handle large grid sizes efficiently.
- Implements **error checking** for convergence and memory allocation failures.

## Installation

Ensure you have an OpenACC-enabled compiler (such as PGI/NVIDIA HPC SDK) installed.

### Prerequisites

- OpenACC-enabled compiler (e.g., `pgcc`, `nvc`)
- Standard C development tools (GCC, Make, etc.)

## Compilation

To compile the program, use the following command:

```sh
nvc -acc -Minfo=accel jacobi_solver.c -o jacobi_solver
```

## Execution

Run the program using:

```sh
./jacobi_solver
```

## Code Explanation

### 1. **Memory Allocation**

```c
double (*u)[M] = malloc(N * sizeof(*u));
double (*f)[M] = malloc(N * sizeof(*f));
```

This dynamically allocates the 2D arrays to store the solution and the right-hand side matrix.

### 2. **Initialization**

```c
void initialize(double u[N][M], double f[N][M]) {
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < M; j++) {
            u[i][j] = 0.0; // Initial guess
            f[i][j] = 1.0; // Right-hand side
        }
    }
}
```

All elements of `u` are initialized to 0, and `f` is set to 1.

### 3. **Jacobi Iteration (Parallelized with OpenACC)**

```c
#pragma acc parallel loop reduction(max:max_diff) collapse(2)
```

This directive parallelizes the loop over `i` and `j`, computing the new `u` values and tracking the maximum difference between the new and old values.

```c
#pragma acc parallel loop collapse(2)
```

Copies the computed values from `u_new` to `u` for the next iteration.

### 4. **Stopping Condition**

```c
while (max_diff > TOL && iter < MAX_ITER);
```

The program stops iterating when:

1. The maximum difference between successive iterations is less than `TOL`.
2. The maximum number of iterations (`MAX_ITER`) is reached.

### 5. **Timing Execution**

```c
struct timeval time;
gettimeofday(&time, NULL);
double t_start = time.tv_sec + time.tv_usec / 1000000.0;
```

This records the execution time for performance measurement.

## Performance Optimization

- Using `#pragma acc parallel loop` ensures efficient parallel execution on GPUs.
- The `collapse(2)` clause optimizes nested loops.
- `reduction(max:max_diff)` ensures proper convergence calculation in parallel execution.

## Expected Output

```sh
Final maximum difference: 9.876543e-07
Elapsed time: 0.245 seconds
```

## Troubleshooting

1. **Memory Allocation Errors**
   - Ensure sufficient memory is available.
2. **Compilation Issues**
   - Check if the OpenACC compiler is installed.
3. **Performance Bottlenecks**
   - Adjust the `collapse` directive or change iteration limits to optimize performance.

## Conclusion

This OpenACC-based Jacobi solver efficiently solves large-scale PDEs by leveraging GPU acceleration. It demonstrates the power of OpenACC for scientific computing applications.
