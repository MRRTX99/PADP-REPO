### PADP Programs

```
- [ ] 3. Write an OpenMP program for Cache unfriendly sieve of Erathothneses.
```

---

gcc -fopenmp 3.c -lm
./a.out

````--------------------------
### Prime Number Sieve - OpenMP Parallelization

### **1. Overview**
This program implements and compares three versions of the **Sieve of Eratosthenes** algorithm for finding prime numbers:
1. **Unfriendly Sieve** - A basic, sequential implementation.
2. **Friendly Sieve** - Optimized memory usage for better performance.
3. **Parallely Sieve** - Uses OpenMP to parallelize the process.

Each version estimates prime numbers up to a given limit `n` and measures execution time.

---

## **2. Code Explanation**
### **strike() Function**
- Marks multiples of a given prime as composite.
- Used by all three sieve implementations.

### **1. Unfriendly Sieve (`unfriendlySieve(n)`)**
- Uses a single array (`comp[]`) to mark non-prime numbers.
- Iterates through numbers and marks their multiples.
- Inefficient due to repeated memory access.
- Time complexity: **O(n log log n)**.

### **2. Friendly Sieve (`friendlySieve(n)`)**
- Uses separate **`factor[]`** and **`striker[]`** arrays for improved cache locality.
- Divides the range into chunks to reduce redundant operations.
- More memory-efficient and slightly faster than `unfriendlySieve()`.

### **3. Parallel Sieve (`parallelySieve(n)`)**
- Uses **OpenMP** directives to parallelize two steps:
  - **Marking composite numbers** using `#pragma omp parallel for`.
  - **Counting prime numbers** using `#pragma omp parallel for reduction(+:count)`.
- Improves performance significantly for large `n`.
- Uses multiple CPU cores efficiently.

---

## **3. Compilation & Execution in VS Code**
### **Compilation:**
To compile the code with OpenMP support, run:
```sh
gcc -fopenmp sieve.c -o sieve -lm
````

### **Execution:**

Run the program using:

```sh
./sieve
```

---

## **4. Expected Output**

```
Unfriendly Time: 2.345678 seconds
Unfriendly Count: 5761455

Friendly Time: 1.678432 seconds
Friendly Count: 5761455

Parallely Time: 0.756431 seconds
Parallely Count: 5761455
```

---

## **5. Comparison of Implementations**

| Sieve Type | Execution Time | Parallelism    |
| ---------- | -------------- | -------------- |
| Unfriendly | Slowest        | No Parallelism |
| Friendly   | Moderate       | No Parallelism |
| Parallely  | Fastest        | Uses OpenMP    |

---

## **6. Conclusion**

- The **Unfriendly Sieve** is simple but inefficient.
- The **Friendly Sieve** optimizes memory usage and improves performance.
- The **Parallely Sieve** is the best for large `n`, leveraging OpenMP for multi-threaded execution.
