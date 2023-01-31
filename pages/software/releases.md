# CCR Software Releases

CCR maintains a suite of software programs, libraries, and toolchains available
for use on our clusters. We typically release a new version of the software
suite on a yearly basis. Previous releases of the software suite are made
available for a short period for use while migrating workloads to the latest
release. You can always check what version of CCR's software suite you have
loaded by running the following command:

```
$ echo $CCR_VERSION
```

The latest release is [2023.01](#2023.01).

!!! Tip "Pin to a specific release"
    Users can ensure their environment is always pinned to a supported CCR release by 
    adding the version string to this file: `~/.ccr/version`

## 2023.01

Supported compiler toolchains:

| Toolchain   | Version | Included compiles and libraries                              |
| ----------- | ------- | ------------------------------------------------------------ |
| **intel**   | 2022.00 | Intel compilers, Intel MPI, and Intel MKL                    |
| **foss**    | 2021b   | GCC, OpenMPI, FlexiBLAS, OpenBLAS, LAPACK, ScaLAPACK, FFTW   |
| **GCC**     | 11.2.0  | GCC compiler only                                            |

Supported CPU architectures:

| Architecture  | Supported CPUs                                             |
| ------------- | ---------------------------------------------------------- |
| avx           | Intel Sandy Bridge, Ivy Bridge                             |
| avx2          | Intel Haswell, Broadwell                                   |
| avx512        | Intel Skylake-SP, Skylake-X, Cascade Lake-SP               |
