# CCR Software Environment Releases

The latest release is [2023.01](#202301).

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
on toolchain versions, new features, deprecations, and import notes.

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
    $ echo "module-version ccrsoft/2023.01 default" >> $HOME/.modulerc
    ```

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

Supported CPU architectures:

| Architecture  | Supported CPUs                                             |
| ------------- | ---------------------------------------------------------- |
| avx2          | Intel Haswell, Broadwell                                   |
| avx512        | Intel Skylake-SP, Skylake-X, Cascade Lake-SP               |

## Legacy

CCR's legacy software release is no longer supported. Users are encouraged to
migrate their workflows to version [2023.01](#202301).

All software in this release was compiled over many years and not optimized for
any specific architectures or toolchains. This release uses a flat naming
scheme so all modules  are directly available for loading.
