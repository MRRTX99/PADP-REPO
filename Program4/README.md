Write program to convert color image to black and white image.  
a) Demonstrate performance of different scheduling techniques for varying chunk sizes.  
b) Analyse scheduling patterns by assigning a single color value for an image for each thread.

---

gcc ex4.c -fopenmp -lgd
./a.out rvce.png output2.png

---

## README: OpenMP Image Processing Program

### Overview

This program applies **parallelized image processing** using OpenMP and the **GD graphics library**. It converts an image into a **greyscale or colored channel** representation, where different threads process different pixel modifications. The parallelization technique improves efficiency when handling large images.

### Dependencies

Ensure the following dependencies are installed before running the program:

- **GD graphics library** (`libgd-dev` for Linux, `gd` for Windows)
- **OpenMP** (enabled via `-fopenmp` when compiling)
- **C compiler** (such as `gcc`)

### Compilation

Compile the program using `gcc` with OpenMP and GD library support:

```sh
gcc -o image_process image_process.c -lgd -fopenmp
```

### Usage

Run the program with an **input PNG image** and specify an **output file**:

```sh
./image_process input.png output.png
```

### How It Works

1. **Reads the input PNG file** using the GD library.
2. **Retrieves the image dimensions** (width and height).
3. **Applies parallelized pixel processing** using OpenMP with guided scheduling:
   - Threads process different pixel sections.
   - Converts the pixel values to greyscale or separate RGB color channels.
4. **Writes the modified image** back to a new output file.

### Parallelization Details

- **OpenMP Parallel For Loop:**

  ```c
  #pragma omp parallel for schedule(guided,100) private(x,y,red,blue,green,temp,color)
  ```

  - `schedule(guided,100)`: Assigns iterations dynamically based on workload.
  - **Alternative schedules:** `static`, `dynamic` for different performance behaviors.

- **Thread-Based Processing:**
  Each thread processes a portion of the image and assigns color transformations based on thread ID:
  ```c
  if(tid==0)
      color = gdImageColorAllocate(img, temp, 0, 0); // Red scale
  else if(tid==1)
      color = gdImageColorAllocate(img, 0, temp, 0); // Green scale
  else if(tid==2)
      color = gdImageColorAllocate(img, 0, 0, temp); // Blue scale
  else
      color = gdImageColorAllocate(img, temp, temp, temp); // Greyscale
  ```

### Performance Timing

The program measures execution time using OpenMP's **`omp_get_wtime()`**:

```c
 double t = omp_get_wtime();
 // Image processing loop
 t = omp_get_wtime() - t;
 printf("Time Taken: %.4f\n", t);
```

### Expected Output

- The processed image will be saved as `output.png`.
- The execution time will be printed to the terminal.

### Example Output

```sh
Width: 800, Height: 600
Time Taken: 0.3456
```

### Notes

- If **GD library is missing**, install it using:
  ```sh
  sudo apt-get install libgd-dev  # Linux
  brew install gd                 # macOS
  ```
- Ensure input images are **PNG format**.
- Modify `omp_set_num_threads(4);` to change the number of threads.

### Conclusion

This OpenMP-based image processing program demonstrates **parallelization in C** for efficient grayscale and color channel transformations on images.
