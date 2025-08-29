# Available Software

CCR maintains a suite of software programs, libraries, and toolchains, called
"Standard Software Environments", for use on our clusters. For details, [see
here](releases.md).

The HPC clusters can execute most software that runs under Linux. In many
cases, the software you need will already be installed and available to you on
the compute nodes. You access the software using what's called a "module".  If
the software you need is not available, you [can ask our staff](building.md#software-build-requests)
to install it for you or [do it yourself](building.md).

Watch this virtual workshop to learn more about using software on CCR's HPC systems:  
![type:video](https://youtube.com/embed/Eonl9_wTrEo)  

## Using Modules

Modules are simply configuration files that dynamically change your environment
allowing you to run a particular application or provide access to a particular
library. The module system allows CCR to provide multiple versions of
software concurrently and enables users to easily switch between different
versions without conflicts. Users can also build and maintain their own modules
for more fine grained control over your groups environment. 

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
| x86-64-v3 (formerly avx2)          | Intel Haswell, Broadwell                                   |
| x86-64-v4 (formerly avx512)        | Intel Cascade Lake-SP, Ice Lake-SP, Sapphire Rapids-SP, Emerald Rapids-SP, AMD Zen4              |
| neoverse-v2          |      ARMv9.0-A NVIDIA Gracehopper                             |

For specific software environment and compiler versions, [see our releases page](releases.md).

## Loading Modules in a Job Script

Modules in a job script can be loaded after your `#SBATCH` directives and
before your actual executable is called. A sample job script that loads Python
into the environment is shown below:

```bash
#!bin/bash -l
#SBATCH --nodes=1
#SBATCH --time=00:01:00
#SBATCH --ntasks=1
#SBATCH --job-name=test-job

# Optionally load a specific software environment
module load ccrsoft/xxxx.yy

# Load your modules here
module load some_module

python3 test-program.py
```

For more information, see the [Running Jobs section](../hpc/jobs.md).

## Application Specific Notes

CCR maintains a [repository](https://github.com/ubccr/ccr-examples) of examples for use in the HPC environment.  This includes example Slurm scripts for a variety of use cases, some application-specific usage examples, and examples on using containers.  This repository will be updated over time so check back frequently for updates.  

### Abaqus  

See [here](https://github.com/ubccr/ccr-examples/tree/main/containers/2_ApplicationSpecific/abaqus) for an example of running Abaqus with Apptainer.

### AlphaFold

See [here](https://github.com/ubccr/ccr-examples/blob/main/slurm/2_ApplicationSpecific/alphafold/README.md) for an example of running AlphaFold2.

### Anaconda Python

CCR does not support running Anaconda natively in the HPC environment. Please do not install it in your home or project directory. We are aware of the fact that Anaconda is widely used in several domains and is useful for easy installations on a single-user laptop. However, Anaconda is not well suited for multi-user HPC clusters for the following reasons:

- Makes wrong assumptions about the OS configuration and location of various system libraries  
- Not meant to keep several versions of the same package on the system  
- Distributes pre-compiled binaries and uses pre-configured compilation options
  which are often not optimal for the processor architectures we have on our cluster  
- Uses the $HOME directory for its installation and generates a huge number of files  
- Modifies the $HOME/.bashrc file, which can easily cause conflicts  
- May not be free for all users.  Please refer to the [Anaconda terms of service documentation](https://legal.anaconda.com/policies/en/)  

As an alternative, we suggest one of the following options for using and installing Python packages:  
1. Use CCR's modules that already include many [popular python packages](#python)  
2. Create your own custom python module bundles using [Easybuild](../howto/easybuild.md).  
3. Use a container with conda installed.  We provide a simple [example](https://github.com/ubccr/ccr-examples/blob/main/containers/2_ApplicationSpecific/conda/README.md) of building and customizing a container for conda in our [`ccr-examples` repository](https://github.com/ubccr/ccr-examples).  For more information about using containers on CCR's systems, [see here](../howto/containerization.md).  

For more details please refer to our [Python documentation](../howto/python.md) or check out the ["Using Python at CCR"](https://ublearns.buffalo.edu/d2l/le/discovery/view/course/288741) course in UB Learns.  


### LS-DYNA  

See [here](https://github.com/ubccr/ccr-examples/tree/main/slurm/2_ApplicationSpecific/lsdyna) for an example of using LS-DYNA.

### Perl

We provide a `perl` module which includes many pre-built CPAN modules. To see
the complete list run: 

```
$ module spider perl
```

Installing additional packages from [CPAN](http://www.cpan.org/) can be done
using the `cpan` tool, which must first be initialized correctly in order to
install them in your home or projects space.

During the first execution of the command `cpan` the utility will ask you if you
want to allow it to configure the majority of settings automatically. Respond
`yes`.

```
$ module load gcc perl
$ cpan
...
Would you like me to configure as much as possible automatically? [yes]
...
What approach do you want?  (Choose 'local::lib', 'sudo' or 'manual')
 [local::lib]
...
```

The cpan utility will offer to append a variety of environment variable
settings to your `.bashrc` file, which you can agree to or set these manually.
Before installing any Perl modules you will need to restart your shell for
these new settings to take effect (logout/login).

Now you can use cpan to install packages:

```
$ module load gcc perl
$ cpan

cpan shell -- CPAN exploration and modules installation (v2.28)
Enter 'h' for help.

cpan[1]> install Chess
....
```

If you require other specific perl modules, we recommend you [ask CCR to build
them](../software/building.md#software-build-requests) or create your own perl
module bundles with easybuild.

### Python

Several python modules are available for use. We encourage users to checkout these modules as they include lots of common scientific python packages.

| module       | Included python packages                                                                     |
| ------------ | -------------------------------------------------------------------------------------------- |
| python-bare  | Bare python3 interpreter only                                                                |
| python       | python3 interpreter plus many commonly used modules                                          |
| scipy-bundle | beniget, Bottleneck, deap, gast, mpi4py, mpmath, numexpr, numpy, pandas, ply, pythran, scipy |
| tensorflow   | TensorFlow                                                                                   |
| pytorch      | PyTorch                                                                                      |


If you require other python libraries not included within CCR's python modules, you can install them yourself but you MUST be careful in doing so.  Instructions you may find online for installing python packages may not work the same in CCR's HPC environment.  We provide extensive documentation and training guides for Python to ensure you have a successful experience.  Which method you use will depend on your workflow and your needs.  We have some suggestions:  

  - Not sure?  Check out the ["Using Python at CCR"](https://ublearns.buffalo.edu/d2l/le/discovery/view/course/288741) course in UB Learns for a full walk through of all the Python options and suggestions for when to use each one.  
  - Prefer to read documentation?  Check out this [How to Use Python at CCR](../howto/python.md) page.
  - Already know you want to use containers?  See [here](../howto/containerization.md) for CCR's container docs.  If you're using GPU-enabled codes, make sure to review [this guide](../howto/containerization.md#gpu-enabled-containers-with-apptainer) first!  
  - Already using other Easybuild modules and want to build your own Python bundle?  See [here](../howto/easybuild.md) for instructions.  
  - Already have your Python environment ready to go?  See [here](https://github.com/ubccr/ccr-examples/blob/main/slurm/2_ApplicationSpecific/python/README.md) for examples on how to run Python using Slurm scripts.  
  - Know you really can't do without conda?  See [here](https://github.com/ubccr/ccr-examples/blob/main/containers/2_ApplicationSpecific/conda/README.md) for an example of how to build and run a conda container.

 

### R

**Software Modules**  

[**ccrsoft/2023.01**](../software/releases.md#202301)  
Two R modules are provided in `ccrsoft/2023.01`: `r` and `r-bundle-bioconductor`, both of which
include many pre-built R libraries. To see a complete list of R libraries and
packages included with each module run the spider command:

```
$ module spider r
$ module spider r-bundle-bioconductor
```

[**ccrsoft/2024.04**](../software/releases.md#202404)  
Two R modules are provided in `ccrsoft/2024.04`: `r` and `r-bundle-cran`, both of which
include many pre-built R libraries. To see a complete list of R libraries and
packages included with each module run the spider command:

```
$ module spider r
$ module spider r-bundle-cran
```

You can install packages from [CRAN](https://cran.r-project.org/) using
`install.packages` while running an interactive R session. For example:

```
$ install.packages("ggplot2", repos="http://cran.r-project.org",
                   lib = "/projects/academic/yourgroup/$USER/software/$CCR_VERSION/rlibs")
```

To install a package that you downloaded run:

```
$ R CMD INSTALL -l /projects/academic/[YourGroupName]/$USER/software/$CCR_VERSION/rlibs/ readr_2.1.3.tar.gz  
```

!!! Tip "Don't want to specify the location each time?"  
    Create a file named .Renviron in your home directory (or edit an existing
    one) and point R to use your alternate directory.  Include the line (editing for your use case):
    `R_LIBS_USER=/projects/academic/[YourGroupName]/$USER/software/$CCR_VERSION/rlibs"`
    Each time R starts it will use this library directory for installations and
    to search for existing installations.  

Sometimes R library installations will fail with errors such as `installation of package ‘library_name’ had non-zero exit status` or similar.  This is a result of the software trying to save temporary files where you do not have permission to write files.  As a workaround, create a temporary directory within your home or project directory and point the R library installation to use it.  As an example:  
```
$ mkdir ~/tmp  
$ module load gcc openmpi r  
$ R 
> Sys.setenv(TMPDIR="/user/$USER/tmp")  
> install.packages("ggplot2", repos="http://cran.r-project.org", lib = "/projects/academic/[YourGroupName]/$USER/software/$CCR_VERSION/rlibs")  
``` 


If your research group requires many R libraries not already available in one of CCR's R installations, we recommend you [ask CCR to build
them](../software/building.md#software-build-requests) or create your own custom R bundle with easybuild.

**Bioconductor Containers**  

CCR provides 4 containers from [Docker Hub](https://hub.docker.com/u/bioconductor) that include R, RStudio, and Bioconductor libraries.  These containers can be used on the command line in [interactive or batch jobs](../hpc/jobs.md#running-applications-on-the-clusters).  They can be found here:  
```
/util/software/containers/x86_64
```
They are named the same as on Docker Hub and relate to Bioconductor's naming convention - starting with either `tidyverse` or `ml-verse`.  These are available in the [RStudio app](../portals/ood.md#rstudio-app) in OnDemand as well.


### RStudio  

Multiple versions of RStudio are available within the available R installations and containers.  In order to launch the RStudio GUI, you must do so using the [RStudio app](../portals/ood.md#rstudio-app) in OnDemand.  

### SAS  

See [here](https://github.com/ubccr/ccr-examples/tree/main/containers/2_ApplicationSpecific/sas) for an example of running SAS using Apptainer.
