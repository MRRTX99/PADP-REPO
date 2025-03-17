### PADP Programs

- [ ] 1. a) Write an OpenMP program that computes the value of PI using Monto-Carlo Algorithm
     b) Write an MPI program that computes the value of PI using Monto-Carlo Algorithm
     ### 1st Program (Monte Carlo)

```----------------------------------

1a) gcc -fopenmp 1.c
    ./a.out
    g++ for CPP files, gcc for C files
1b) mpicc 2.c
    mpirun -np 4 ./a.out

    ==========================
```

# Monte Carlo π Estimation - OpenMP & MPI Versions

## **1. Overview**

This repository contains two implementations of the Monte Carlo method for estimating the value of π:

1. **OpenMP Version:** Uses multi-threading for parallel execution.
2. **MPI Version:** Uses distributed processing with multiple processes.

Both implementations generate random points within a unit square and determine how many fall inside the unit circle to approximate π.

---

## **2. OpenMP Version (`pi_openmp.c`)**

### **How It Works**

- Uses **OpenMP** for multi-threading.
- Distributes the iterations across multiple threads.
- Uses `omp_set_num_threads()` to set the thread count.
- Uses `#pragma omp parallel` to parallelize the computation.
- Uses `#pragma omp for` to distribute loop iterations across threads.
- Uses `#pragma omp atomic` to safely update the shared `count` variable.
- Measures execution time using `omp_get_wtime()`.

### **Compilation & Execution in VS Code**

1. Open VS Code and navigate to the file directory.
2. Compile using `gcc -fopenmp pi_openmp.c -o pi_openmp`.
3. Run using `./pi_openmp` and enter the number of iterations.

### **Expected Output**

The program outputs the estimated value of π and the execution time for different thread counts:

```
Threads	 Execution Time(s)	 PI Estimation
1	0.015432	3.141592
2	0.008321	3.141592
4	0.004785	3.141593
```

---

## **3. MPI Version (`pi_mpi.c`)**

### **How It Works**

- Uses **MPI** for distributed parallel processing.
- Each process performs a portion of the computation.
- Uses `MPI_Comm_rank()` to get the process rank.
- Uses `MPI_Comm_size()` to get the total number of processes.
- Uses `MPI_Reduce()` to sum results across all processes.
- Measures execution time using `MPI_Wtime()`.

### **Compilation & Execution in VS Code**

1. Open VS Code and navigate to the file directory.
2. Compile using `mpicc pi_mpi.c -o pi_mpi`.
3. Run using `mpirun -np 4 ./pi_mpi` (where `4` is the number of processes).

### **Expected Output**

The program outputs the estimated value of π, execution time, and number of processes used:

```
Time: 0.002534 seconds
No. of threads: 4
No. of trials: 10000
Estimated value of pi: 3.141600
```

---

## **4. Comparison of OpenMP and MPI Versions**

| Feature         | OpenMP Version                  | MPI Version                           |
| --------------- | ------------------------------- | ------------------------------------- |
| Parallelism     | Multi-threading (Shared Memory) | Multi-processing (Distributed Memory) |
| Synchronization | Uses `#pragma omp atomic`       | Uses `MPI_Reduce`                     |
| Scalability     | Limited to one machine          | Can run across multiple machines      |
| Compilation     | `gcc -fopenmp`                  | `mpicc`                               |
| Execution       | `./pi_openmp`                   | `mpirun -np N ./pi_mpi`               |

---

## **5. Conclusion**

- Use **OpenMP** when working on a single machine with multiple cores.
- Use **MPI** for distributed computing across multiple machines.
- Both methods efficiently estimate π using Monte Carlo simulations.
