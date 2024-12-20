# CCR Software Environment Releases

The latest stable release is [2023.01](#202301).

## What are CCR Software Environments?

CCR maintains a suite of software programs, libraries, and toolchains, called
"Standard Software Environments", for use on our clusters. These software
environments are provided through a set of modules which allow you to switch
between different releases. CCR's standard environments identify combinations
of specific compiler toolchains and software modules that are used most
commonly to build other software. These combinations are grouped in modules
named `ccrsoft` and the default version automatically loaded by lmod when you
login.

We typically release a new version of `ccrsoft` on a yearly basis. Previous
software environment releases are made available for a short period for use
while migrating workloads to the latest release. This page contains the
changelog for each software environment release where you can find information
on toolchain versions, new features, deprecations, and important notes.

To switch between CCR software environment releases run the following commands:

```
# View all available software releases
$ module spider ccrsoft

# Load a specific release
$ module load ccrsoft/2023.01
```

!!! Tip "Pin to a specific release"
    When you login the default version of `ccrsoft` module will be loaded
    automatically for you. Users can override the default version and pin to a
    specific release by adding the version to `~/.modulerc`.  For
    example:
    ```
    $ echo "module-version ccrsoft/2023.01 default" > $HOME/.modulerc
    ```
    NOTE: This should be done only once.  To update your default version, edit the file and change the ccrsoft/version information  

## 2024.04

New features/changes in this release include:

- Support for aarch64 (ARMv9.0-A NVIDIA Gracehopper)
- Microarchitecture avx2 renamed to x86-64-v3
- Microarchitecture avx512 renamed to x86-64-v4

Supported compiler toolchains:

| Toolchain   | Version | Included compiles and libraries                              |
| ----------- | ------- | ------------------------------------------------------------ |
| **intel**   | 2023b   | Intel compilers, Intel MPI, and Intel MKL                    |
| **foss**    | 2023b   | GCC, OpenMPI, FlexiBLAS, OpenBLAS, LAPACK, ScaLAPACK, FFTW   |
| **GCC**     | 13.2.0  | GCC compiler only                                            |
| **CUDA**    | 12.4.0  | nvcc                                                         |

Supported CPU Microarchitectures:

| CPU March          | CPU Family  | Supported CPUs                                         |
| ------------------ | ----------- | ------------------------------------------------------ |
| x86-64-v3 (avx2)   |  x86\_64    | Intel Haswell, Broadwell, AMD Zen3                     |
| x86-64-v4 (avx512) |  x86\_64    | Intel Cascade Lake-SP, Ice Lake-SP, Sapphire Rapids-SP, Emerald Rapids-SP, AMD Zen4 |
| neoverse-v2        |  aarch64    | ARMv9.0-A NVIDIA Gracehopper                           |

## 2023.01

New features in this release include:

- Software is now compiled and optimized for specific architectures
- A hierarchical module naming scheme consisting of a 3-level hierarchy:
    - Core level - compiler and architecture independent
    - Compiler level - depend on a specific CPU architecture and compiler toolchain
    - MPI level - depend on a specific CPU architecture, compiler toolchain, and MPI library

Supported compiler toolchains:

| Toolchain   | Version | Included compiles and libraries                              |
| ----------- | ------- | ------------------------------------------------------------ |
| **intel**   | 2022.00 | Intel compilers, Intel MPI, and Intel MKL                    |
| **foss**    | 2021b   | GCC, OpenMPI, FlexiBLAS, OpenBLAS, LAPACK, ScaLAPACK, FFTW   |
| **GCC**     | 11.2.0  | GCC compiler only                                            |
| **CUDA**    | 11.8.0  | nvcc                                                         |
| **NVHPC**   | 22.11   | CUDA 11.8.0, nvcc, nvc++                                     |

Supported CPU Microarchitectures:

| Architecture  | Supported CPUs                                             |
| ------------- | ---------------------------------------------------------- |
| avx2          | Intel Haswell, Broadwell                                   |
| avx512        | Intel Cascade Lake-SP, Ice Lake-SP, Sapphire Rapids-SP, Emerald Rapids-SP, AMD Zen4               |


