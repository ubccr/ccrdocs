# CCR Software Releases

The latest release is [2023.01](#202301).

CCR maintains a suite of software programs, libraries, and toolchains available
for use on our clusters. We typically release a new version of the software
suite on a yearly basis. Previous releases of the software suite are made
available for a short period for use while migrating workloads to the latest
release. 

To switch between CCR software releases run the following commands:

```
# Check what version you're currently running
$ echo $CCR_VERSION

# View all available software releases
$ module spider ccrsoft

# Load a specific release
$ module load ccrsoft/2023.01
```

!!! Tip "Pin to a specific release"
    Users can ensure their environment is always pinned to a supported CCR release by 
    adding the version string to this file: `~/.ccr/version`

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
