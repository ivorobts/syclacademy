# SYCL Academy

## Exercise 1: Compiling with SYCL

---

For this first exercise you simply need to install ComputeCpp and the SYCL
Academy dependencies and then verify your installation by comping a source file
for SYCL.

### 1.) Installing ComputeCpp

To install ComputeCpp follow the instructions in the README.md of the SYCL
Academy repository for installing ComputeCpp and the necessary OpenCL drivers.

### 2.) Verifying your environment

ComputeCpp includes a tool called `computecpp_info` which lists all the
devices available on your machine and displays which are setup with the correct
drivers.

Open a console and run the executable located in the 'bin' directory of the
ComputeCpp release package:

```
./computecpp_info
```

Look for the lines that say:
```
  Device is supported                     : YES - Tested internally by Codeplay
  Software Ltd.
```

You can also add the option --verbose to display further information about the
devices.

From this output you can confirm your environment is setup correctly.

### 3.) Configuring the exercise project

Once you have confirmed your environment is setup and available you are ready to
compile your first SYCL application from source code.

First fetch the tutorial samples from GitHub.

Clone this repository ensuring that you include sub-modules.

```
git clone --branch iwocl21 --recursive https://github.com/codeplaysoftware/syclacademy.git
mkdir build
cd build
```

### 4.) Include the SYCL header file

Then open the source file for this exercise and include the SYCL header file
`"SYCL/sycl.hpp"`.

Make sure before you do this you define `SYCL_LANGUAGE_VERSION` to `2020`, to
enable support for the SYCL 2020 interface.

Once that is done build your source file with your chosen build system.

### 5.) Compile and run

Once you've done that simply build the exercise with your chosen build system
and invoke the executable.


#### Build And Execution Hints

For For DPC++ (using the Intel DevCloud):
```sh
dpcpp -o sycl-ex-1 -I../External/Catch2/single_include ../Code_Exercises/Exercise_01_compiling_with_SYCL/source.cpp
```
In Intel DevCloud, to run computational applications, you will submit jobs to a queue for execution on compute nodes,
especially some features like longer walltime and multi-node computation is only abvailable through the job queue.
Please refer to the [guide][devcloud-job-submission].

So wrap the binary into a script `job_submission` and run:
```sh
qsub job_submission
```

For ComputeCpp:
```sh
cmake -DSYCL_ACADEMY_USE_COMPUTECPP=ON -DSYCL_ACADEMY_INSTALL_ROOT=/insert/path/to/computecpp ..
make exercise_01_compiling_with_sycl_source
./Code_Exercises/Exercise_01_compiling_with_SYCL/exercise_01_compiling_with_sycl_source
```


For hipSYCL:
```sh
# Add -DHIPSYCL_GPU_ARCH=<arch> to the cmake arguments when compiling for GPUs.
# <arch> is e.g. sm_60 for NVIDIA Pascal GPUs, gfx900 for AMD Vega 56/64, and gfx906 for Radeon VII.
cmake -DSYCL_ACADEMY_USE_HIPSYCL=ON -DSYCL_ACADEMY_INSTALL_ROOT=/insert/path/to/hipsycl -DHIPSYCL_PLATFORM=<cpu|cuda|rocm> ..
make exercise_01_compiling_with_sycl_source
./Code_Exercises/Exercise_01_compiling_with_SYCL/exercise_01_compiling_with_sycl_source
```
alternatively, without cmake:
```sh
cd Code_Exercises/Exercise_01_compiling_with_SYCL
HIPSYCL_PLATFORM=<cpu|cuda|rocm> HIPSYCL_GPU_ARCH=<arch-when-compiling-for-gpu> /path/to/hipsycl/bin/syclcc -o sycl-ex-1 -I../../External/Catch2/single_include source.cpp
./sycl-ex-1
```


[devcloud-job-submission]: https://devcloud.intel.com/oneapi/documentation/job-submission/