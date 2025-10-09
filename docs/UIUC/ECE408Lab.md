## LAB1

```c
// LAB 1
#include <wb.h>

__global__ void vecAdd(float *in1, float *in2, float *out, int len) {
  //@@ Insert code to implement vector addition here
  int i = blockIdx.x * blockDim.x + threadIdx.x;
  if (i < len) {
    out[i] = in1[i] + in2[i];
  }
}

int main(int argc, char **argv) {
  wbArg_t args;
  int inputLength;
  float *hostInput1;
  float *hostInput2;
  float *hostOutput;
  float *deviceInput1;
  float *deviceInput2;
  float *deviceOutput;

  args = wbArg_read(argc, argv);
  //@@ Importing data and creating memory on host
  hostInput1 =
      (float *)wbImport(wbArg_getInputFile(args, 0), &inputLength);
  hostInput2 =
      (float *)wbImport(wbArg_getInputFile(args, 1), &inputLength);
  hostOutput = (float *)malloc(inputLength * sizeof(float));

  wbLog(TRACE, "The input length is ", inputLength);

  //@@ Allocate GPU memory here
  int size = inputLength * sizeof(float);
  cudaMalloc((void **)&deviceInput1, size);
  cudaMalloc((void **)&deviceInput2, size);
  cudaMalloc((void **)&deviceOutput, size);

  //@@ Copy memory to the GPU here
  cudaMemcpy(deviceInput1, hostInput1, size, cudaMemcpyHostToDevice);
  cudaMemcpy(deviceInput2, hostInput2, size, cudaMemcpyHostToDevice);

  //@@ Initialize the grid and block dimensions here
  dim3 dimBlock(256);
  dim3 dimGrid((inputLength - 1) / 256 + 1);

  //@@ Launch the GPU Kernel here to perform CUDA computation
  vecAdd<<<dimGrid, dimBlock>>>(deviceInput1, deviceInput2, deviceOutput,
                                inputLength);

  cudaDeviceSynchronize();
  //@@ Copy the GPU memory back to the CPU here
  cudaMemcpy(hostOutput, deviceOutput, size, cudaMemcpyDeviceToHost);

  //@@ Free the GPU memory here
  cudaFree(deviceInput1);
  cudaFree(deviceInput2);
  cudaFree(deviceOutput);

  wbSolution(args, hostOutput, inputLength);

  free(hostInput1);
  free(hostInput2);
  free(hostOutput);

  return 0;
}
```

## LAB2

```c
#include <wb.h>

#define wbCheck(stmt)                                                     \
  do {                                                                    \
    cudaError_t err = stmt;                                               \
    if (err != cudaSuccess) {                                             \
      wbLog(ERROR, "Failed to run stmt ", #stmt);                         \
      wbLog(ERROR, "Got CUDA error ...  ", cudaGetErrorString(err));      \
      return -1;                                                          \
    }                                                                     \
  } while (0)


// Compute C = A * B
__global__ void matrixMultiply(float *A, float *B, float *C, int numARows,
                               int numAColumns, int numBRows,
                               int numBColumns, int numCRows,
                               int numCColumns)
{
  //@@ Implement matrix multiplication kernel here
  int Row = blockIdx.y * blockDim.y + threadIdx.y;
  int Col = blockIdx.x * blockDim.x + threadIdx.x;
  if (Row < numCRows && Col < numCColumns) {
    float Cvalue = 0;
    for (int i = 0; i < numAColumns; ++i) {
      int ARow = Row;
      int ACol = i;
      int BRow = i;
      int BCol = Col;
      Cvalue += A[ARow * numAColumns + ACol] * B[BRow * numBColumns + BCol];
    }
    C[Row * numCColumns + Col] = Cvalue;
  }
}


int main(int argc, char **argv) {
  wbArg_t args;
  float *hostA; // The A matrix
  float *hostB; // The B matrix
  float *hostC; // The output C matrix
  
  int numARows;    // number of rows in the matrix A
  int numAColumns; // number of columns in the matrix A
  int numBRows;    // number of rows in the matrix B
  int numBColumns; // number of columns in the matrix B
  int numCRows;    // number of rows in the matrix C (you have to set this)
  int numCColumns; // number of columns in the matrix C (you have to set
                   // this)

  args = wbArg_read(argc, argv);

  //@@ Importing data and creating memory on host
  hostA = (float *)wbImport(wbArg_getInputFile(args, 0), &numARows,
                            &numAColumns);
  hostB = (float *)wbImport(wbArg_getInputFile(args, 1), &numBRows,
                            &numBColumns);
  wbLog(TRACE, "The dimensions of A are ", numARows, " x ", numAColumns);
  wbLog(TRACE, "The dimensions of B are ", numBRows, " x ", numBColumns);

  //@@ Set numCRows and numCColumns
  // A_{m x n} * B_{n x p} = C_{m x p}
  numCRows = numARows;
  numCColumns = numBColumns;

  //@@ Allocate the hostC matrix
  hostC = (float *)malloc(numCRows * numCColumns * sizeof(float));

  //@@ Allocate GPU memory here
  float *deviceA;
  float *deviceB;
  float *deviceC;
  cudaMalloc((void**)&deviceA, numARows * numAColumns * sizeof(float));
  cudaMalloc((void**)&deviceB, numBRows * numBColumns * sizeof(float));
  cudaMalloc((void**)&deviceC, numCRows * numCColumns * sizeof(float));

  //@@ Copy memory to the GPU here
  cudaMemcpy(deviceA, hostA, numARows * numAColumns * sizeof(float), cudaMemcpyHostToDevice);
  cudaMemcpy(deviceB, hostB, numBRows * numBColumns * sizeof(float  ), cudaMemcpyHostToDevice);

  //@@ Initialize the grid and block dimensions here
  dim3 DimGrid(ceil(numCColumns/16.0), ceil(numCRows/16.0), 1);
  dim3 DimBlock(16, 16, 1); 

  //@@ Launch the GPU Kernel here
  matrixMultiply<<<DimGrid, DimBlock>>>(deviceA, deviceB, deviceC, numARows, numAColumns, numBRows, numBColumns, numCRows, numCColumns); 

  cudaDeviceSynchronize();
  
  //@@ Copy the GPU memory back to the CPU here
  cudaMemcpy(hostC, deviceC, numCRows * numCColumns * sizeof(float), cudaMemcpyDeviceToHost);

  //@@ Free the GPU memory here
  cudaFree(deviceA);
  cudaFree(deviceB);
  cudaFree(deviceC);


  wbSolution(args, hostC, numCRows, numCColumns);

  free(hostA);
  free(hostB);
  //@@Free the hostC matrix
  free(hostC);

  return 0;
}
```

## LAB3

```c
#include <wb.h>

#define wbCheck(stmt)                                                     \
  do {                                                                    \
    cudaError_t err = stmt;                                               \
    if (err != cudaSuccess) {                                             \
      wbLog(ERROR, "Failed to run stmt ", #stmt);                         \
      wbLog(ERROR, "Got CUDA error ...  ", cudaGetErrorString(err));      \
      return -1;                                                          \
    }                                                                     \
  } while (0)

#define TILE_WIDTH 16

// Compute C = A * B
__global__ void matrixMultiplyShared(float *A, float *B, float *C,
                                     int numARows, int numAColumns,
                                     int numBRows, int numBColumns,
                                     int numCRows, int numCColumns) {
  //@@ Insert code to implement matrix multiplication here
  //@@ You have to use shared memory for this MP
  // declare arrays in shared memory
  __shared__ float A_s[TILE_WIDTH][TILE_WIDTH];
  __shared__ float B_s[TILE_WIDTH][TILE_WIDTH];
  unsigned int row = blockIdx.y * blockDim.y + threadIdx.y;
  unsigned int col = blockIdx.x * blockDim.x + threadIdx.x;
  float sum = 0.0f;
  // We need to round up for the Width
  int numTiles = (numAColumns - 1) / TILE_WIDTH + 1;                            
  
  // Loop over the tiles of the input in phases
  for (unsigned int tile = 0; tile < numTiles; ++tile) {
    // Load tile to shared memory
    if (row < numARows && tile*TILE_WIDTH+threadIdx.x < numAColumns) {
      // as before
      A_s[threadIdx.y][threadIdx.x] = A[row * numAColumns + tile*TILE_WIDTH + threadIdx.x];
    } else {
      A_s[threadIdx.y][threadIdx.x] = 0.0f;
    }

    if (tile*TILE_WIDTH+threadIdx.y < numBRows && col < numBColumns) {
      // as before
      B_s[threadIdx.y][threadIdx.x] = B[(tile*TILE_WIDTH + threadIdx.y)*numBColumns + col];
    } else {
      B_s[threadIdx.y][threadIdx.x] = 0.0f;
    }
    __syncthreads(); // Threads wait for each other to finish loading before computing
    
    // Compute with tile
    if (row < numARows && col < numBColumns) {
      for (unsigned int i = 0; i < TILE_WIDTH && (tile*TILE_WIDTH+i)<numAColumns; ++i) {
        sum += A_s[threadIdx.y][i] * B_s[i][threadIdx.x];
      }
    }
      __syncthreads(); // Threads wait for each other to finish loading before computing

  }

  if (row < numARows && col < numBColumns) {
    C[row * numCColumns + col] = sum;
  }
}

int main(int argc, char **argv) {
  wbArg_t args;
  float *hostA; // The A matrix
  float *hostB; // The B matrix
  float *hostC; // The output C matrix

  int numARows;    // number of rows in the matrix A
  int numAColumns; // number of columns in the matrix A
  int numBRows;    // number of rows in the matrix B
  int numBColumns; // number of columns in the matrix B
  int numCRows;    // number of rows in the matrix C (you have to set this)
  int numCColumns; // number of columns in the matrix C (you have to set
                   // this)

  args = wbArg_read(argc, argv);

  //@@ Importing data and creating memory on host
  hostA = (float *)wbImport(wbArg_getInputFile(args, 0), &numARows,
                            &numAColumns);
  hostB = (float *)wbImport(wbArg_getInputFile(args, 1), &numBRows,
                            &numBColumns);
  //@@ Set numCRows and numCColumns
  numCRows = numARows;
  numCColumns = numBColumns;

  //@@ Allocate the hostC matrix
  hostC = (float *)wbMalloc(numCRows * numCColumns * sizeof(float));
  //@@ Allocate GPU memory here
  float *deviceA;
  float *deviceB;
  float *deviceC;
  wbCheck(cudaMalloc((void **)&deviceA, numARows * numAColumns * sizeof(float)));
  wbCheck(cudaMalloc((void **)&deviceB, numBRows * numBColumns * sizeof(float)));
  wbCheck(cudaMalloc((void **)&deviceC, numCRows * numCColumns * sizeof(float)));

  //@@ Copy memory to the GPU here
  wbCheck(cudaMemcpy(deviceA, hostA, numARows * numAColumns * sizeof(float), cudaMemcpyHostToDevice));
  wbCheck(cudaMemcpy(deviceB, hostB, numBRows * numBColumns * sizeof(float), cudaMemcpyHostToDevice));   

  //@@ Initialize the grid and block dimensions here
  dim3 DimGrid(ceil(numCColumns / 16.0), ceil(numCRows / 16.0), 1);
  dim3 DimBlock(16, 16, 1);

  //@@ Launch the GPU Kernel here
  matrixMultiplyShared<<<DimGrid, DimBlock>>>(deviceA, deviceB, deviceC, numARows, numAColumns, numBRows, numBColumns, numCRows, numCColumns);
  cudaDeviceSynchronize();

  //@@ Copy the GPU memory back to the CPU here
  wbCheck(cudaMemcpy(hostC, deviceC, numCRows * numCColumns * sizeof(float), cudaMemcpyDeviceToHost));

  //@@ Free the GPU memory here
  cudaFree(deviceA);
  cudaFree(deviceB);
  cudaFree(deviceC);

  wbSolution(args, hostC, numCRows, numCColumns);

  free(hostA);
  free(hostB);

  //@@ Free the hostC matrix
  free(hostC);

  return 0;
}
```

## LAB4

```c
#include <wb.h>

#define wbCheck(stmt)                                                     \
  do {                                                                    \
    cudaError_t err = stmt;                                               \
    if (err != cudaSuccess) {                                             \
      wbLog(ERROR, "CUDA error: ", cudaGetErrorString(err));              \
      wbLog(ERROR, "Failed to run stmt ", #stmt);                         \
      return -1;                                                          \
    }                                                                     \
  } while (0)

//@@ Define any useful program-wide constants here
# define MASK_WIDTH 3
# define MASK_RADIUS 1
# define TILE_WIDTH 4
# define OUTPUT_TILE_WIDTH (TILE_WIDTH)
# define INPUT_TILE_WIDTH (TILE_WIDTH + MASK_WIDTH - 1)

//@@ Define constant memory for device kernel here
__constant__ float deviceKernel[MASK_WIDTH * MASK_WIDTH * MASK_WIDTH];

__global__ void conv3d(float *input, float *output, const int z_size,
                       const int y_size, const int x_size) {
  //@@ Insert kernel code here
  // Shared memory tile, correctly aliased as N_ds
  __shared__ float N_ds[INPUT_TILE_WIDTH][INPUT_TILE_WIDTH][INPUT_TILE_WIDTH];

  // Thread indices
  int tx = threadIdx.x;
  int ty = threadIdx.y;
  int tz = threadIdx.z;

  // Global coordinates of this thread's output element
  int output_x = blockIdx.x * TILE_WIDTH + tx;
  int output_y = blockIdx.y * TILE_WIDTH + ty;
  int output_z = blockIdx.z * TILE_WIDTH + tz;

  // Top-left-front corner of the input tile in global memory
  int input_start_x = blockIdx.x * TILE_WIDTH - MASK_RADIUS;
  int input_start_y = blockIdx.y * TILE_WIDTH - MASK_RADIUS;
  int input_start_z = blockIdx.z * TILE_WIDTH - MASK_RADIUS;
  
  // Flattened thread index within the block and total number of threads in the block
  int flat_thread_id = tz * TILE_WIDTH * TILE_WIDTH + ty * TILE_WIDTH + tx;
  int num_threads_in_block = TILE_WIDTH * TILE_WIDTH * TILE_WIDTH;

  // Load input tile into shared memory with boundary checks
  for (int i = flat_thread_id; i < INPUT_TILE_WIDTH * INPUT_TILE_WIDTH * INPUT_TILE_WIDTH; i += num_threads_in_block) {
    // Convert flat index 'i' back to 3D coords in shared memory
    int sz = i / (INPUT_TILE_WIDTH * INPUT_TILE_WIDTH);
    int remainder = i % (INPUT_TILE_WIDTH * INPUT_TILE_WIDTH);
    int sy = remainder / INPUT_TILE_WIDTH;
    int sx = remainder % INPUT_TILE_WIDTH;

    // Calculate corresponding global input coordinates
    int gx = input_start_x + sx;
    int gy = input_start_y + sy;
    int gz = input_start_z + sz;

    // Boundary check (zero-padding) and load from global to shared memory
    if (gx >= 0 && gx < x_size && gy >= 0 && gy < y_size && gz >= 0 && gz < z_size) {
      N_ds[sz][sy][sx] = input[gz * y_size * x_size + gy * x_size + gx];
    } else {
      N_ds[sz][sy][sx] = 0.0f;
    }
  }

  // Synchronize to ensure all data is loaded before computation
  __syncthreads();

  // Guard to make sure we don't compute for threads outside the image bounds
  if (output_x < x_size && output_y < y_size && output_z < z_size) {
    float outputValue = 0.0f;
    
    // Perform convolution using shared memory
    for (int z = 0; z < MASK_WIDTH; z++) {
      for (int y = 0; y < MASK_WIDTH; y++) {
        for (int x = 0; x < MASK_WIDTH; x++) {
          outputValue += deviceKernel[z * MASK_WIDTH * MASK_WIDTH + y * MASK_WIDTH + x] * N_ds[tz + z][ty + y][tx + x];
        }
      }
    }
    
    // Write result to global memory
    output[output_z * y_size * x_size + output_y * x_size + output_x] = outputValue;
  }
}

int main(int argc, char *argv[]) {
  wbArg_t args;
  int z_size;
  int y_size;
  int x_size;
  int inputLength, kernelLength;
  float *hostInput;
  float *hostKernel;
  float *hostOutput;
  //@@ Initial deviceInput and deviceOutput here.

  args = wbArg_read(argc, argv);

  // Import data
  hostInput = (float *)wbImport(wbArg_getInputFile(args, 0), &inputLength);
  hostKernel =
      (float *)wbImport(wbArg_getInputFile(args, 1), &kernelLength);
  hostOutput = (float *)malloc(inputLength * sizeof(float));

  // First three elements are the input dimensions
  z_size = hostInput[0];
  y_size = hostInput[1];
  x_size = hostInput[2];
  wbLog(TRACE, "The input size is ", z_size, "x", y_size, "x", x_size);
  assert(z_size * y_size * x_size == inputLength - 3);
  assert(kernelLength == 27);


  //@@ Allocate GPU memory here
  // Recall that inputLength is 3 elements longer than the input data
  // because the first three elements were the dimensions

  float *deviceInput;
  float *deviceOutput;

  wbCheck(cudaMalloc((void **)&deviceInput,
                     (inputLength - 3) * sizeof(float)));
  wbCheck(cudaMalloc((void **)&deviceOutput,
                     (inputLength - 3) * sizeof(float)));


  //@@ Copy input and kernel to GPU here
  // Recall that the first three elements of hostInput are dimensions and
  // do
  // not need to be copied to the gpu
  wbCheck(cudaMemcpy(deviceInput, hostInput + 3,
                     (inputLength - 3) * sizeof(float),
                     cudaMemcpyHostToDevice));
  wbCheck(cudaMemcpyToSymbol(deviceKernel, hostKernel,
                             kernelLength * sizeof(float)));

  //@@ Initialize grid and block dimensions here
  dim3 DimGrid(ceil(1.0 * x_size / OUTPUT_TILE_WIDTH),
               ceil(1.0 * y_size / OUTPUT_TILE_WIDTH),
               ceil(1.0 * z_size / OUTPUT_TILE_WIDTH));
  dim3 DimBlock(OUTPUT_TILE_WIDTH, OUTPUT_TILE_WIDTH, OUTPUT_TILE_WIDTH);

  //@@ Launch the GPU kernel here
  conv3d<<<DimGrid, DimBlock>>>(deviceInput, deviceOutput,
                                z_size, y_size, x_size);
  wbCheck(cudaGetLastError());

  cudaDeviceSynchronize();

  //@@ Copy the device memory back to the host here
  // Recall that the first three elements of the output are the dimensions
  // and should not be set here (they are set below)
  wbCheck(cudaMemcpy(hostOutput + 3, deviceOutput,
                     (inputLength - 3) * sizeof(float),
                     cudaMemcpyDeviceToHost));             

  // Set the output dimensions for correctness checking
  hostOutput[0] = z_size;
  hostOutput[1] = y_size;
  hostOutput[2] = x_size;
  wbSolution(args, hostOutput, inputLength);

  //@@ Free device memory
  wbCheck(cudaFree(deviceInput));
  wbCheck(cudaFree(deviceOutput));

  // Free host memory
  free(hostInput);
  free(hostOutput);
  return 0;
}
```

