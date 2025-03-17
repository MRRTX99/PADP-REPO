### PADP Programs

- [ ] 5. Write a MPI Program that has a total of 4 processes. Process with rank 1, 2, and 3 should send the following messages respectives to teh process with rank 0: HELLO, CSE, RVCE.

````---------------
mpicc 5.c
mpirun -np 4 ./a.out   or mpirun --oversubscribe -np 4 a.out

``-------------------------------------------------------`

- **README: MPI Message Passing Program**

### Overview

This program demonstrates basic **MPI (Message Passing Interface) communication** between multiple processes. It involves sending and receiving messages between different ranks in an MPI environment.

### Compilation and Execution

#### **Compile the program:**

```bash
mpicc mpi_message_passing.c -o mpi_message_passing
````

#### **Run the program with 4 processes:**

```bash
mpirun -np 4 ./mpi_message_passing
```

### Code Explanation

#### **Header Files**

- `stdio.h` and `stdlib.h` for standard I/O operations.
- `string.h` for string operations (`strcpy`).
- `mpi.h` for MPI functions.

#### **Definitions**

- `SIZE 4` → The number of processes.
- `BUFSIZE 32` → Maximum size for message buffers.
- `ROOT 0` → Root process ID.
- `TAG 0` → Message tag for MPI communication.

#### **Message Array (`m[SIZE]`)**

- Contains predefined messages for each process (except rank 0).

#### **MPI Initialization**

- `MPI_Init(&argc, &argv);` initializes MPI.
- `MPI_Comm_rank(MPI_COMM_WORLD, &rank);` gets the process rank.
- `MPI_Comm_size(MPI_COMM_WORLD, &size);` gets the total number of processes.
- If the number of processes is not 4 (`SIZE`), the program exits with an error message.

#### **Message Passing**

- **Non-root processes (`rank != ROOT`)**:

  - Copy their respective messages from `m[rank]` into `msg`.
  - Send the message to the root process using `MPI_Send`.

- **Root process (`rank == ROOT`)**:
  - Receives messages from all other processes using `MPI_Recv`.
  - Prints the received messages.

#### **Finalization**

- `MPI_Finalize();` terminates MPI execution.

### Example Output

```bash
Received Hello in process 0 from process 1
Received RVCE in process 0 from process 2
Received CSE in process 0 from process 3
```

### Key MPI Concepts Used

- **Point-to-point communication:** `MPI_Send` and `MPI_Recv`.
- **Process synchronization:** Each process either sends or receives data according to its rank.
- **Distributed message passing:** Different processes communicate data to the root process.

### Improvements and Extensions

- Modify the message array dynamically based on `size`.
- Implement bidirectional communication (send and receive from all processes).
- Use `MPI_Bcast` or `MPI_Scatter/Gather` for more efficient collective communication.
