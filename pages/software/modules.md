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
| avx2          | Intel Haswell, Broadwell                                   |
| avx512        | Intel Skylake-SP, Skylake-X, Cascade Lake-SP               |

For specific compiler versions, [see our releases page](releases.md).

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

### Abaqus  

Abaqus 2024 is available via a Singularity container. Please refer to our [container documentation](../howto/containerization.md) for more information on using Singularity. You can find the Abaqus container here: `/util/software/container/x86_64/abaqus-2024.sif`  This is a large file (10GB) so please be sure to copy it to a location where you have enough space (i.e. your project directory), or you can run the container from this location.  

**Abaqus GUI**  

To run the Abaqus GUI using this container, first start an [OnDemand desktop](../portals/ood.md#interactive-apps) session.  Once started, launch a terminal in the OnDemand desktop.  Then run this command to start the container and launch the Abaqus GUI:  

```
/usr/bin/singularity exec -B /util:/util,/scratch:/scratch /util/software/containers/x86_64/abaqus-2024.sif abaqus cae -mesa
```  

!!! Tip  "Accessing additional directories in your container"  
    The `-B` option is telling Singularity which directories on the node you want to bind mount into the container.  You will automatically get access to your home directory.  The directories we have listed here to bind mount are required.  If you also want access to your project directory you can add `,/projects:/projects` to the list or your specific directory `,/projects/academic/[YourGroupName]:/projects/academic/[YourGroupName]` for example.

**Abaqus command line**  

To run Abaqus from the command line, either interactively or in a batch script, run this command:  

```
/usr/bin/singularity exec -B /util:/util,/scratch:/scratch /util/software/containers/x86_64/abaqus-2024.sif /bin/bash
```  

Once the container starts you'll see the Apptainer command prompt and then you can run the Abaqus command as normal.  For example:  

```
Apptainer> abaqus help  
```

**Abaqus & GPUs**  

If you need to use GPUs with Abaqus you'll need to request a GPU node and add a few things to the Singularity command that starts the container. Add this after the rest of your bind mounts in the Singularity exec command:  
`,/opt/software/nvidia:/opt/software/nvidia --nv`  

From our example above to run the Abaqus GUI on a GPU node, the command would be:  

```
/usr/bin/singularity exec -B /util:/util,/scratch:/scratch,/opt/software/nvidia:/opt/software/nvidia --nv /util/software/containers/x86_64/abaqus-2024.sif abaqus cae -mesa
```

**NOTE:**  If you're using the Abaqus GUI, we recommend running on the [viz partition](../hpc/clusters.md#visualization-nodes) and qos of the UB-HPC cluster.  However, this will work from any GPU node.    

Please refer to the [Abaqus (Simulia) documentation](https://help.3ds.com/2020/English/DSSIMULIA_Established/SIMULIA_Established_FrontmatterMap/sim-t-SIMULIA_EstablishedDocSearchOnline.htm) for additional information on using this software.  



### AlphaFold

To use AlphaFold run:

```
$ module load foss alphafold
```

A couple notes on running AlphaFold:

- AlphaFold does not currently support nvidia H100 cards. So you'll want to use
  any of our A100 or V100 GPU nodes.
- CCR has downloaded the full genetic databases and model parameters and the
  path is automatically included when running run_alphafold.py. The full path
  can be found here: 
  ```
  echo $ALPHAFOLD_DATA_DIR
  /util/software/data/alphafold
  ```
- Many of the examples you'll find online run AlphaFold in docker. You do not
  want to do this. Instead just substitute `python3 docker/run_docker.py` with
  the script provided by the alphfold module `run_alphafold.py`. They will have
  the same CLI arguments.

Below is a sample slurm batch script for running AlphaFold on a GPU node to run
a single sequence prediction:

```bash
#!/bin/bash -l

#SBATCH --time=03:30:00
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=32
#SBATCH --mem=64G
#SBATCH --gpus-per-node=2
#SBATCH --constraint=A100

module load foss alphafold

srun run_alphafold.py --fasta_paths=T1050.fasta \
                      --max_template_date=2020-05-14 \
                      --model_preset=monomer \
                      --db_preset=full_dbs \
                      --output_dir=output
```

### Anaconda Python

CCR does not support Anaconda environments. Please do not use it on the
cluster. We are aware of the fact that Anaconda is widely used in several
domains and is useful for easy installations on a single-user laptop. However,
Anaconda is not well suited for multi-user HPC clusters for the following
reasons:

- Makes wrong assumptions about the OS configuration and location of various system libraries  
- Not meant to keep several versions of the same package on the system  
- Distributes pre-compiled binaries and uses pre-configured compilation options
  which are often not optimal for the processor architectures we have on our cluster  
- Uses the $HOME directory for its installation and generates a huge number of files  
- Modifies the $HOME/.bashrc file, which can easily cause conflicts  
- May not be free for all users.  Please refer to the [Anaconda terms of service documentation](https://legal.anaconda.com/policies/en/)  

Instead we recommend using modules that already include many [popular python
packages](#python). Rather than installing python modules in conda environments users can create
custom python module bundles using easybuild. For more details [see here](#python).

If Easybuild is not an ideal option for your work, you could utilize a container to install Anaconda and
your required packages.  For more information about using containers on CCR's systems, [see here](../howto/containerization.md).  


### LS-DYNA  

LS-DYNA is now part of the Ansys software bundle.  To load the module, use `module load ansys/2023R1`  The lsdyna executables do not show up in the path any longer.  To use them properly, you'll need to use these commands.

**Single Precision**  
`$EBROOTANSYS/v231/ansys/bin/linx64/lsdyna_sp.e`

**Single precision, massively parallel:**  
`$EBROOTANSYS/v231/ansys/bin/linx64/lsdyna_sp_mpp.e`  


**Double Precision**  
`$EBROOTANSYS/v231/ansys/bin/linx64/lsdyna_dp.e`

**Double precision, massively parallel:**  
`$EBROOTANSYS/v231/ansys/bin/linx64/lsdyna_dp_mpp.e`  

Please refer to the Ansys LS-DYNA [manuals](https://lsdyna.ansys.com/manuals/) for further information and options.    


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

Several python modules are available for use. We encourage users to checkout
these modules as they include lots of common scientific python packages.

| module       | Included python packages                                                                     |
| ------------ | -------------------------------------------------------------------------------------------- |
| python-bare  | Bare python3 interpreter only                                                                |
| python       | python3 interpreter plus many commonly used modules                                          |
| scipy-bundle | beniget, Bottleneck, deap, gast, mpi4py, mpmath, numexpr, numpy, pandas, ply, pythran, scipy |
| tensorflow   | TensorFlow                                                                                   |
| pytorch      | PyTorch                                                                                      |

If you require other specific python modules, we recomend you [ask CCR to build
them](../software/building.md#software-build-requests) or create your own python module bundles with easybuild.

Here's an example easybuild recipe that installs a python module from pip:

```python
easyblock = 'PythonBundle'

name = 'mygroup-bundle'
version = '1.0.0'

homepage = 'https://github.com/ubccr/software-layer'
description = """
Custom python modules for my group
"""

toolchain = {'name': 'foss', 'version': '2021b'}

# list any other dependencies here
dependencies = [
    ('Python', '3.9.6'),
    ('SciPy-bundle', '2021.10'),
]

exts_list = [
    # sha256 checksum can be found on pypi, for example:
    # https://pypi.org/project/fuzzywuzzy/#copy-hash-modal-bdeeeb75-5450-499a-ae89-21c91611d2c7
    ('fuzzywuzzy', '0.18.0', {
        'checksums': ['45016e92264780e58972dca1b3d939ac864b78437422beecebb3095f8efd00e8'],
    }),
]

sanity_pip_check = True
use_pip = True

moduleclass = 'math'
```

Save the above to a file called `mygroup-bundle-1.0.0-foss-2021b.eb`. To install run:

```
$ module load easybuild
$ export CCR_BUILD_PREFIX=/projects/academic/[YourGroupName]/easybuild
$ eb mygroup-bundle-1.0.0-foss-2021b.eb
```

To use run:

```
$ module load mygroup-bundle
$ python3
$ import fuzzywuzzy
```

You can also use [virtual
environments](../howto/python.md#virtual-environments)
to manage your python projects but this comes with some caveats.  Please refer to our documentation on proper use of Python on CCR's HPC systems.

### R

Two R modules are provided: `r` and `r-bundle-bioconductor`, both of which
include many pre-built R libraries. To see a complete list of R libraries and
packages included with each module run the spider command:

```
$ module spider r
$ module spider r-bundle-bioconductor
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
[login:~]$ mkdir ~/tmp  
[login:~]$ module load gcc openmpi r  
[login:~]$ R 
Sys.setenv(TMPDIR="/user/$USER/tmp")  
install.packages("ggplot2", repos="http://cran.r-project.org", lib = "/projects/academic/[YourGroupName]/$USER/software/$CCR_VERSION/rlibs")  
``` 


If your research group requires many R libraries not already available in one of CCR's R installations, we recommend you [ask CCR to build
them](../software/building.md#software-build-requests) or create your own custom 
R bundle with easybuild.
