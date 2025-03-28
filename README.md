# Sparse-Matrix-Vector-Multiplication
This project implements and compares three versions of sparse matrix-vector multiplication:

Serial implementation - A baseline sequential version     
OpenMP implementation - A shared-memory parallel version using OpenMP       
MPI implementation - A distributed-memory parallel version using MPI      

The project focuses on analyzing the performance (speedup and efficiency) of these parallelization techniques for different matrix sizes (1.4M, 1.6M, and 1.8M elements) and sparsity levels (0%, 10%, 50%, and 100%).

# Key Features

> Serial Implementation

The serial implementation serves as the baseline for performance comparison. It generates sparse matrices with configurable sparsity levels and performs matrix-vector multiplication sequentially. The program also computes additional metrics such as the maximum, minimum, and sum of the result vector, as well as row and column averages. This version is straightforward but lacks parallelism, making it suitable for understanding the fundamental performance characteristics of the algorithm.

> OPENMP Implementation

Openmp uses shared-memory parallelism to take less time in computations. 
It dynamically schedules work across threads to balance the load, especially important for sparse matrices where work distribution can be uneven. The implementation includes parallel reductions for statistical calculations and allows users to specify the number of threads. There are also parallel sections for independent operations.

> MPI Implementation


The MPI version is designed for distributed-memory systems, partitioning the matrix across multiple processes. It uses MPI's collective operations like broadcast and reduce to manage communication and aggregation of results. Each process handles a portion of the matrix, computing local results that are later combined in global variables.

# Requirements

To compile and run the project, you will need a C compiler (GCC recommended), OpenMP support (typically included with GCC), and an MPI implementation such as OpenMPI or MPICH. A Linux/Unix environment is recommended for ease of setup and execution.

# How to Use

> Serial

Compile using **gcc serial_sparse_matrix.c -o serial**
Run the program by this command: ./serial

> OpenMP

Compile using **gcc sparse_matrix_openmp.c -o openmp -fopenmp**
Run the program by this command: ./openmp

> MPI

Compile using **mpicc mpi_sparse_matrix.c -o mpi**
Run the program by this command for any number of processors(for example: 4 processors): **mpirun -np 4 ./mpi**

# Input Parameters
Each program prompts the user for:

Matrix size: The number of rows/columns in the square matrix.

Sparsity percentage: A value between 0 (dense) and 1 (fully sparse).

Parallel configuration: For OpenMP/MPI, the number of threads or processes to use.

# Performance Analysis
The project includes detailed performance data in Project Data Testing.xlsx, showcasing execution times, speedup, and efficiency for various configurations. Key observations include:

OpenMP excels for smaller matrices and lower sparsity but struggles with scalability at higher thread counts.

MPI shows better performance for large, sparse matrices and scales more effectively with additional processes, though communication overhead can be a bottleneck.

Both parallel versions demonstrate diminishing efficiency as concurrency increases, highlighting the challenges of load balancing and resource contention.

More detailed observations can be found in the report.
