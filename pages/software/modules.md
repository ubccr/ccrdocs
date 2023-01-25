# Available Software

CCR maintains a suite of software programs, libraries, and toolchains commonly
used in scientific computing. The HPC clusters can execute most software that
runs under Linux. In many cases, the software you need will already be
installed and available to you on the compute nodes. You access the software
using what's called a "module".  If the software you need is not available, you
can ask our staff to install it for you or [do it yourself](building.md).

!!! Warning "New software infrastructure now available"
    CCR is moving to a new software infrastructure described in this document.
    Starting in the Summer of 2023 users will be required to migrate to the
    system. To start using the new software now, simply run this command `touch ~/.ccr_new_modules`.
    You will need to logout and log back in for the changes to take effect. If
    you'd like to temporarily go back to using the old modules in `/util`,
    simply remove that file `rm ~/.ccr_new_modules`.

## Using Modules

Modules are simply configuration files that dynamically change your environment
allowing you to run a particular application or provide access to a particular
library. The module system allows CCR to provide multiple versions of
software concurrently and enables users to easily switch between different
versions without conflicts. Users can also build and maintain their own modules
for more fine grain control over your groups environment. 

Modules are managed using a tool called [Lmod](https://lmod.readthedocs.io)
developed by [TACC](https://www.tacc.utexas.edu/). For a more comprehensive
overview of Lmod you can read the [user guide here](https://lmod.readthedocs.io/en/latest/010_user.html). 

To see what software modules are available, ssh into the login node and run:

```
$ module avail
```

This will return a list of modules available to load into your environment.

!!! Note
    If a module has dependencies you may not see the module listed until
    dependencies are loaded. For example, software compiled with the gcc
    toolchain will not be shown until you load gcc or foss modules. See the
    [hierarchical modules](#hierarchical-modules) section for more information.

If you cannot load a module because of dependencies, you can use the module
spider command to find what dependencies you need to load the module:

```
module spider some_module

# For example, openmpi requires gcc:
$ module spider openmpi
    You will need to load all module(s) on any one of the lines below before 
    the "openmpi/4.1.1" module is available to load.

      gcc/11.2.0
```

To load your chosen modules into the environment run:

```
$ module load some_module_name

# For example:
$ module load python
```

You can specify the version of the software by appending a / with the version
number:

```
module load some_module/version 

# For example:
$ module load python/3.9.5
```

## Hierarchical Modules

CCR uses a hierarchical module naming convention to support programs built with
specific compiler, library, and CPU architecture requirements. For example, when you run
`module avail` on an Intel Skylake compute node (avx512), you will see three
hierarchical levels of modules that look like this:

```output
---------------------------- MPI-dependent avx512 modules -----------------------------

-------------------------- Compiler-dependent avx512 modules --------------------------

------------------------------------ Core modules -------------------------------------
```

Core modules
:    compiler and architecture independent

Compiler-dependent modules
:    depend on a specific CPU architecture and compiler toolchain

MPI-dependent modules
:    depend on a specific CPU architecture, compiler toolchain, and MPI library

!!! Note "Only core modules are shown by default"
    When you run `module avail` only the core modules are shown by default. To
    see modules for a specific compiler toolchain you will need to first load
    the module for the specific compiler toolchain of interest.

CCR supports the following compiler toolchains:

| Toolchain   | Included compilers and libraries                             |
| ----------- | ------------------------------------------------------------ |
| **intel**   | Intel compilers, Intel MPI, and Intel MKL                    |
| **foss**    | GCC, OpenMPI, FlexiBLAS, OpenBLAS, LAPACK, ScaLAPACK, FFTW   |
| **GCC**     | GCC compiler only                                            |

In addition to the compiler toolchains, the hierarchical module system is also
"CPU architecture" aware. The module system will auto-detect what type of CPU
you're running on and display modules built for that specific architecture.

CCR supports the following CPU architectures:

| Architecture  | Supported CPUs                                             |
| ------------- | ---------------------------------------------------------- |
| avx2          | Intel Haswell, Broadwell                                   |
| avx512        | Intel Skylake-SP, Skylake-X, Cascade Lake-SP               |

For specific compiler versions, [see our releases page](releases.md).

## Loading Modules in a Job Script

Modules in a job script can be loaded after your `#SBATCH` directives and
before your actual executable is called. A sample job script that loads Python
into the environment is shown below:

```bash
#!bin/bash
#SBATCH --nodes=1
#SBATCH --time=00:01:00
#SBATCH --ntasks=1
#SBATCH --job-name=test-job

# Load your modules here
module load python

python3 test-program.py
```

For more information, see the [Running Jobs section](../hpc/jobs.md).

## Python

Several python modules are available for use: `python`, `anaconda3`, and
`scipy-bundle`. We encourage users to checkout these modules as they include
lots of common scientific python packages.

| module       | Included python packages                                                                     |
| ------------ | -------------------------------------------------------------------------------------------- |
| python       | Bare python3 interpreter only                                                                |
| scipy-bundle | beniget, Bottleneck, deap, gast, mpi4py, mpmath, numexpr, numpy, pandas, ply, pythran, scipy |
| anaconda3    | [see here](https://docs.anaconda.com/anaconda/packages/py3.9_linux-64/)                            |

We also recommend using [virtual environments](https://packaging.python.org/en/latest/guides/installing-using-pip-and-virtual-environments/#creating-a-virtual-environment).

## R

Two R modules are provided: `r` and `r-bundle-bioconductor`, both of which
include many pre-built R libraries. To see a complete list of R libraries and
packages included with each module run the spider command:

```
$ module spider r
$ module spider r-bundle-bioconductor
```

## Perl

We provide a `perl` module which includes many pre-built CPAN modules. To see
the complete list run: 

```
$ module spider perl
```
