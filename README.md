[![Hits](https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https%3A%2F%2Fgithub.com%2Fpjyi2147%2FGPU_Computing_project&count_bg=%23FFBC93&title_bg=%238FC2FF&icon=&icon_color=%23E7E7E7&title=visits&edge_flat=false)](https://hits.seeyoufarm.com)

### CSED 490C Heterogeneous Computing - Final Project
### Fall 2023, POSTECH

---

### Details

This project is to parallelize Quick Hull algorithm for Convex Hull problem using CUDA and compare the performance between the serial (CPU) version of the algorithm.

### How to run

The project is built using Nvidia GPU teaching kit.

CUDA-enabled GPU, CUDA Toolkit and CMake (CCMake) must be installed to run the project.

1. Build libgputk 
The following procedure will build `libgputk` (the support library) that will be linked with your template file for processing command-line arguments, logging time, and checking the correctness of your solution. 

Create the target build directory

~~~
mkdir build-dir
cd build-dir
~~~

We will use `ccmake`

~~~
ccmake ..
~~~

You will see the following screen

![ccmake](https://s3.amazonaws.com/gpuedx/resources/screenshots/Screenshot+2015-10-23+11.58.27.png)

Pressing `c` would configure the build to your system (in the process detecting
  the compiler, the CUDA Toolkit location, etc...).

![ccmake-config](https://s3.amazonaws.com/gpuedx/resources/screenshots/Screenshot+2015-10-23+12.03.26.png)

~~~
BUILD_LIBgpuTK_LIBRARY          *ON
BUILD_LOGTIME                   *ON
~~~

If you have modified the above, then you should type `g` to regenerate the Makefile and then `q` to quit out of `ccmake`.
You can then use the `make` command to build the labs.

![make](https://s3.amazonaws.com/gpuedx/resources/screenshots/Screenshot+2015-10-23+12.11.15.png)


2. Build the data generator and template 

The following will compile the template file, and the data generator that will generate input files. 

~~~
cd sources 
make template 
make daataset_generator 
~~~

You can generate input data with

~~
./dataset_generator
~~

This will create a directory that contains multiple pairs of input data. You can modify the file to generate input data of different sizes.

Change the file name in `Makefile` to change the template file version to the version that you want to build.

---

### Version changelogs

v1:

* initial version

v2:

* changed pt_idx structure
* Does not use pt_idx pointer vectors anymore (free from deep copy!!)

v3:

* Apply threshold to apply CUDA kernel
* Best perf at 32 * BLOCKSIZE

v4:

* Apply parallel reduction on the max dist calculation
* Best perf at 32 * BLOCKSIZE (85ms on 2M points)

v5:

* Apply Unified memory
* Does not work well

v6:

* Sort using thrust
* Works really well

---

### Benchmark results

Optimization flag includes `-O3 -Xptxas -O3`.

![image](https://github.com/pjyi2147/CSED490C-project/assets/21299683/a58db0ae-fdec-4b19-83a5-a7bcabcca897)
![image](https://github.com/pjyi2147/CSED490C-project/assets/21299683/9d338e86-ffa5-455c-80a0-19462294f7aa)

---

### References

[Computing the convex hull on GPU by Timur Iskhakov](https://timiskhakov.github.io/posts/computing-the-convex-hull-on-gpu)
