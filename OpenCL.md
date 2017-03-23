# OpenCL.org Initiative

TODO: What is OpenCL.org initiative?

## Acknowledgements

## About [StreamComputing](https://streamcomputing.eu)

# Table Of Contents

##### NOTE FOR CONTRIBUTORS:
> [Edit this when you add/remove sections/chapters.]

1. [OpenCL Introduction](#S-introduction)
2. [Platforms and tools](#S-platforms)
   1. SDKs
   2. Debuggers
   3. Profilers
3. [Libraries](#S-libraries)
4. Specification
5. Getting Started
6. Profiling
7. Bibliography

# <a name="S-introduction"></a>OpenCL Introduction 

## What is OpenCL?

OpenCL (trademark of Apple Computers Inc.) is an open, royalty-free industry standard that makes much faster computations possible through parallel computing. The standard is controlled by non-profit standards organisation Khronos. For example, by using this technology with graphics cards and modern multi-core processors it is possible to convert a video in 20 minutes instead of 2 hours, or analyze spectra of hundreds of thousands of stars in minutes instead of several hours.

## How does it work?

OpenCL is an extension to existing languages. It makes it possible to specify a piece of code that is executed multiple times independently from each other. This code can run on various processors – not only the main CPU. Also, OpenCL has built-in support for vector types (float2, short4, int8, long16, etc), and operations on those types can be mapped to vector extensions of modern CPUs (SSE, AVX).

>For example, you need to calculate `sin(x)` of a large array `A` of one million numbers. Based on the information provided by the OpenCL framework you can pick the best device, or even several devices, and send the data to the device(s). Normally you would loop over the million numbers, one number after another, but with OpenCL you can just say: "For each `x` in array `A` give me `sin(x)`", and each `x` is processed in parallel. When finished, you can take the data back from the device(s) or proceed with other computations.

OpenCL framework is great at exposing parallel nature of various compute-devices: x86 CPUs, GPUs, FPGAs, DSPs. This can significantly lower the total execution time compared to conventional sequential methods.

## 5 questions on OpenCL

**Q: Why is it so fast?**

>OpenCL framework gives programmers tools and features which enable them to implement efficient parallel algorithms. It does it by providing direct access to the cores of multi-core CPUs, and to the hundreds of little processors on graphics cards. 

**Q: Does it work on any type of hardware?**

>As it is an open standard, it can work on any type of hardware that targets parallel execution. This can be a CPU, GPU, DSP or FPGA. You can read more in [Platforms and tools](#S-platforms) chapter.

**Q: How does it compare to OpenMP/MPI?**

>Where OpenMP and MPI try to split loops over threads/servers and is CPU-oriented, OpenCL focuses on getting threads being data-position aware and making use of processor-capabilities.

**Q: Does it replace C or C++?**

>No, it is a framework which integrates well with C, C++, Python, Java and more.

**Q: How stable/mature is OpenCL?**

>First version of OpenCL was released in 2009. The latest version is OpenCL 2.1 from November 2015. The standard is being actively developed. Next version (2.2), which currently has provisional status, will include OpenCL C++ kernel language based C++14 standard.

# <a name="S-platforms"></a>Platforms and tools

# <a name="S-libraries"></a>Libraries

The crucial part of every technology and programming language are libraries. They extend the language, simplify it, add new features, and help you build you applications faster. The same goes for OpenCL. This chapter presents a few selected libraries which at the time seemed popular, useful and reliable.

## Wrappers 

### [OpenCL-CLHPP](https://github.com/KhronosGroup/OpenCL-CLHPP)

OpenCL Host API C++ bindings. 

> For many large applications C++ is the language of choice and so it seems reasonable to define C++ bindings for OpenCL.

> The interface is contained with a single C++ header file cl2.hpp and all definitions are contained within the namespace cl. There is no additional requirement to include cl.h and to use either the C++ or original C bindings; it is enough to simply include cl2.hpp.

> The bindings themselves are lightweight and correspond closely to the underlying C API. Using the C++ bindings introduces no additional execution overhead.

* Homepage: https://github.com/KhronosGroup/OpenCL-CLHPP
* Documentation: http://github.khronos.org/OpenCL-CLHPP

### [Boost.Compute](https://github.com/boostorg/compute/)

Boost.Compute is an official Boost library, added to the Boost C++ Libraries package since 1.61 version. It is a comprehensive wrapper for OpenCL 1.0 - 2.0. It provides STL-like algorithms and various helper features (functions, classes) which make developing in C++/OpenCL environment much faster.

> Boost.Compute is a GPU/parallel-computing library for C++ based on OpenCL.

> The core library is a thin C++ wrapper over the OpenCL API and provides access to compute devices, contexts, command queues and memory buffers.

> On top of the core library is a generic, STL-like interface providing common algorithms (e.g. `transform()`, `accumulate()`, `sort()`) along with common containers (e.g. `vector<T>`, `flat_set<T>`). It also features a number of extensions including parallel-computing algorithms (e.g. `exclusive_scan()`, `scatter()`, `reduce()`) and a number of fancy iterators (e.g. `transform_iterator<>`, `permutation_iterator<>`, `zip_iterator<>`).

* Homepage: https://github.com/boostorg/compute/
* Documentation: http://www.boost.org/doc/libs/1_63_0/libs/compute/doc/html/index.html
* Talks:
    * [Talk about Boost.Compute @ IWOCL 2016](http://www.iwocl.org/wp-content/uploads/iwocl-2016-boost-compute.pdf) by Jakub Szuppe
    * [Boost.Compute @ C++Now 2015](https://github.com/boostcon/cppnow_presentations_2015/blob/master/files/Boost.ComputeCxxNow2015.pdf) by Kyle Lutz ([Video](https://www.youtube.com/watch?v=q7oCblCtTT8))
* Other resources:
    * [Differences between VexCL, Thrust, and Boost.Compute](http://stackoverflow.com/questions/20154179/differences-between-vexcl-thrust-and-boost-compute)  

### [AMD Aparapi](https://github.com/aparapi/aparapi)

Aparapi enables Java developers to define OpenCL kernels and executed them on GPU and APU devices.

>Aparapi allows Java developers to take advantage of the compute power of GPU and APU devices by executing data parallel code fragments on the GPU rather than being confined to the local CPU. It does this by converting Java bytecode to OpenCL at runtime and executing on the GPU, if for any reason Aparapi can't execute on the GPU it will execute in a Java thread pool.

> We like to think that for the appropriate workload this extends Java's 'Write Once Run Anywhere' to include GPU devices.

* Homepage: https://github.com/aparapi/aparapi
* Documentation:
    * https://github.com/aparapi/aparapi/blob/master/doc/README.md
    * https://code.google.com/archive/p/aparapi/


##### Note
> You find more OpenCL wrappers/bindings in blog post [StreamComputing: OpenCL Wrappers](https://streamcomputing.eu/knowledge/for-developers/opencl-wrappers/).

## Specialized libraries

### [VexCL](https://github.com/ddemidov/vexcl)

VexCL was developed with scientific computing in mind. It provides custom DSL to simplify using various accelerators for vector arithmetic, reduction, sparse matrix-vector product etc. It has some features of a wrapper library, but not all of them. However, it is possible to define generic C++ algorithms with its DSL and write custom kernels using VexCL. It supports both OpenCL and CUDA.

>VexCL is a vector expression template library for OpenCL/CUDA. It has been created for ease of GPGPU development with C++. VexCL strives to reduce amount of boilerplate code needed to develop GPGPU applications. The library provides convenient and intuitive notation for vector arithmetic, reduction, sparse matrix-vectork products, etc. Multi-device and even multi-platform computations are supported. The source code of the library is distributed under very permissive MIT license.

* Homepage: https://github.com/boostorg/compute/
* Documentation: http://www.boost.org/doc/libs/1_63_0/libs/compute/doc/html/index.html
* Talks: http://vexcl.readthedocs.io/en/latest/talks.html
* Other resources:
    * [Differences between VexCL, Thrust, and Boost.Compute](http://stackoverflow.com/questions/20154179/differences-between-vexcl-thrust-and-boost-compute)

### [ArrayFire](https://arrayfire.com/)

>ArrayFire is a general-purpose library that simplifies the process of developing software that targets parallel and massively-parallel architectures including CPUs, GPUs, and other hardware acceleration devices.

* Homepages:
    * https://arrayfire.com/
    * https://github.com/arrayfire/arrayfire 
* Documentation: http://arrayfire.org/docs/

### [ViennaCL](http://viennacl.sourceforge.net/)

>ViennaCL is a free open-source linear algebra library for computations on many-core architectures (GPUs, MIC) and multi-core CPUs. The library is written in C++ and supports CUDA, OpenCL, and OpenMP (including switches at runtime).

* Homepage: http://viennacl.sourceforge.net/
* Documentation: http://viennacl.sourceforge.net/viennacl-documentation.html

### [clMathLibraries](https://github.com/clMathLibraries)

clMathLibraries is a name for a group of math libraries with OpenCL backend. Also see [StreamComputing: OpenCL alternatives for CUDA Linear Algebra Libraries](https://streamcomputing.eu/blog/2014-01-16/opencl-alternatives-for-cuda-linear-algebra-libraries/).

* [clFFT](https://github.com/clMathLibraries/clFFT) - a software library containing FFT functions written in OpenCL
* [clBLAS](https://github.com/clMathLibraries/clBLAS) - a software library containing BLAS functions written in OpenCL
* [clSPARSE](https://github.com/clMathLibraries/clSPARSE) - a software library containing Sparse functions written in OpenCL.
* [clRNG](https://github.com/clMathLibraries/clRNG) - an OpenCL based software library containing random number generation functions

##### Note
> Full list of libraries using OpenCL can be found at [khronos.org/opencl/resources](https://www.khronos.org/opencl/resources).

# <a name="S-specification"></a>Specification

The OpenCL specification documents can be found on [the Khronos OpenCL Registry](https://www.khronos.org/registry/OpenCL/). They are a must-read for everyone who wants to dive into OpenCL programming and a great reference for the experienced OpenCL developer. 

* OpenCL 2.2 (Provisional)
    * [The OpenCL 2.2 Specification (API)](https://www.khronos.org/registry/OpenCL/specs/opencl-2.2.pdf)
    * [The OpenCL C++ Language Specification](https://www.khronos.org/registry/OpenCL/specs/opencl-2.2-cplusplus.pdf)
* OpenCL 2.1
    * [The OpenCL 2.1 Specification (API)](https://www.khronos.org/registry/OpenCL/specs/opencl-2.1.pdf)
    * [The OpenCL 2.0 C Language Specification](https://www.khronos.org/registry/OpenCL/specs/opencl-2.0-openclc.pdf)
        * Note: OpenCL 2.1 uses OpenCL 2.0 C Language for OpenCL programs
    * [Online Reference Pages](http://www.khronos.org/registry/cl/sdk/2.1/docs/man/xhtml/)
* OpenCL 2.0 
    * [The OpenCL 2.0 Specification (API)](https://www.khronos.org/registry/OpenCL/specs/opencl-2.0.pdf)
    * [The OpenCL 2.0 C Language Specification](https://www.khronos.org/registry/OpenCL/specs/opencl-2.0-openclc.pdf)
    * [Online Reference Pages](http://www.khronos.org/registry/cl/sdk/2.0/docs/man/xhtml/)
* OpenCL 1.2
    * [The OpenCL 1.2 Specification (API)](https://www.khronos.org/registry/OpenCL/specs/opencl-1.2.pdf)
    * [The OpenCL 1.2 C Language Specification](https://www.khronos.org/registry/OpenCL/specs/opencl-1.2.pdf#page=197)
    * [Online Reference Pages](http://www.khronos.org/registry/cl/sdk/1.2/docs/man/xhtml/)
* All specifications and other documents regarding OpenCL standard, including including environment specifications, extensions specifications, and specifications for OpenCL 1.0 and 1.1, are available at https://www.khronos.org/registry/OpenCL.

## The OpenCL Architecture

The crucial part of The OpenCL Specification is the chapter about the OpenCL architecture. It is very important to understand at least its basic principles. Without this knowledge it is not possible neither to efficiently program using OpenCL nor to use it to its full capabilities. 

The architecture is described by four models:

* Platform Model
* Memory Model
* Programming Model
* Execution Model

The platform model describes in general how the OpenCL framework looks like and gives definitions of a host and an OpenCL device. The memory model explains different memory regions and memory objects introduced in OpenCL. More advanced sections about memory model present details of how shared virtual memory mechanism works, and presents memory consistency model and ordering rules. Since OpenCL 2.0 the programming model does not have its own section. It specifies that the OpenCL execution model supports both data parallel and task parallel programming models.

The execution model is the model that explains how the OpenCL framework really works. It defines responsibilities of a host program, it says what is a command queue, what is a kernel, and it describes how an execution of an OpenCL kernel on a device works. In order to understand OpenCL you must carefully read and understand particularly this part of the specification, and know: how workloads are mapped onto devices, when synchronization happens, what is an index space.
 
# Getting Started

## [CL-basic]()

CL-basic is a C prototype to help you get started with creating your first simple OpenCL application. It offers simplified host-code OpenCL API functions and a sample OpenCL kernel that you can reference to get started quick! In addition, this prototype can be compiled under both Windows and Linux-based systems thanks to the use of CMake.

Host-code functions can be found in files:
> `cl_util.c`

> `cl_util.h`

For getting platform and/or device information, use the following functions are:
```c
void PrintPlatformName(cl_platform_id platform);
void PrintDeviceName(cl_device_id device);
int PrintOpenCLInfo();
void SelectOpenCLPlatformAndDevice(cl_platform_id* pPlatform, cl_device_id* pDevice);
```

For creating and releasing an OpenCL context, the following functions are:
```c
cl_context CreateOpenCLContext(cl_platform_id platform, cl_device_id device);
void ReleaseOpenCLContext(cl_context *pContext);
```

For creating and releasing an OpenCL command queue, the following functions are:
```c
cl_command_queue CreateOpenCLQueue(cl_device_id device, cl_context context);
void ReleaseOpenCLQueue(cl_command_queue *pQueue);
```

For creating and releasing an OpenCL buffer allocated on an OpenCL device, the following functions are:
```c
cl_mem CreateDeviceBuffer(cl_context context, size_t sizeInBytes);
void ReleaseDeviceBuffer(cl_mem *pDeviceBuffer);
```

For copying data rom the host to device, or from the device to the host, the following functions are:
```c
void CopyHostToDevice(void* hostBuffer, cl_mem deviceBuffer, size_t sizeInBytes, cl_command_queue queue, cl_bool blocking);
void CopyDeviceToHost(cl_mem deviceBuffer, void* hostBuffer, size_t sizeInBytes, cl_command_queue queue, cl_bool blocking);
```

For loading an OpenCL source from a file, creating and releasing the OpenCL program, the following functions are:
```c
char* LoadOpenCLSourceFromFile(char* filePath, size_t *pSourceLength);
cl_program CreateAndBuildProgram(cl_context context, char* sourceCode, size_t sourceCodeLength);
void ReleaseProgram(cl_program *pProgram);
```

For creating and releasing OpenCL Kernels, the following functions are:
```c
cl_kernel CreateKernel(cl_program program, char* kernelName);
void ReleaseKernel(cl_kernel *pKernel);
```

An error function has also been prepared to make it easier to translate an error code returned by an OpenCL host function, and it can be used as below:
```c
clError = clEnqueueNDRangeKernel(queue, simpleFunctionKernel, workDim, NULL, globalWorkSize, localWorkSize, 0, NULL, NULL);
CHECK_OCL_ERR("clEnqueueNDRangeKernel", clError);
```

Refer to `main.cpp` for a reference of how these host-code functions are used, and `OpenCLKernels.cl` for how the OpenCL kernel is written. 

# Profiling

# Bibliotgraphy

* [The Khronos OpenCL Working Group, The OpenCL Specification, Version: 2.1](https://www.khronos.org/registry/OpenCL/specs/opencl-2.1.pdf)
* [The Khronos OpenCL Working Group, The OpenCL C Specification, Version: 2.0](https://www.khronos.org/registry/OpenCL/specs/opencl-2.0-openclc.pdf)