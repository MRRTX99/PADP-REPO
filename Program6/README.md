### PADP Programs

````
- [ ] 6. Write an OpenMP program for Word search in a file and illustrate the perfomanace using different sizes of file.

---------------------------------

gcc -fopenmp 6.c
./a.out
```----------------------

---

````

# README - OpenMP Parallel Word Count Program

## Overview

This program counts the occurrences of predefined words in a text file using OpenMP for parallelization. It reads words from a file (`words.txt`), converts them to lowercase, and compares them with a predefined list of words.

## Features

- Uses OpenMP for parallel execution
- Reads words from a file and performs case-insensitive matching
- Displays execution time and word frequency count

## Prerequisites

- A C compiler with OpenMP support (e.g., GCC)
- A text file named `words.txt` containing sample words

## Compilation

To compile the program with OpenMP:

```bash
gcc -fopenmp word_count.c -o word_count
```

## Execution

Run the program with the desired number of threads:

```bash
./word_count <num_threads>
```

For example:

```bash
./word_count 4
```

where `4` is the number of threads to use.

## How It Works

1. **Predefined Words**: The program defines an array `words[]` containing words to search for.
2. **Parallel Processing**: Each word search is performed in parallel using OpenMP.
3. **Case-Insensitive Matching**: Both the input text and predefined words are converted to lowercase for accurate matching.
4. **Performance Timing**: Execution time is measured using `omp_get_wtime()`.
5. **Results Display**: The program prints the frequency of each word along with execution time.

## Code Explanation

- `to_lower(char *str)`: Converts a string to lowercase.
- `get_count(const char *file_name, const char *key)`: Reads `words.txt` and counts occurrences of `key`.
- `main()`: Parses command-line arguments, sets the number of threads, and runs word counting in parallel.

## Example Output

```
Time: 0.002345 seconds
lorem 10
ipsum 8
dolo 5
sit 12
amet 7
saksham 3
```

## Notes

- Ensure `words.txt` is present in the same directory as the executable.
- The number of threads should not exceed the number of logical cores on your machine.
