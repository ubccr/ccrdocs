# Python Options

There are many options for using Python and its derivates on CCR's systems.  CCR provides, at most, two versions of Python and two versions of Anaconda as well as SciPy (Scientific Python libraries) via it's modules system.  These are updated once per year with the oldest version being rotated out.  Users will see a warning when a module is being deprecated giving you advance notice to update your workflow.  

**This page describes the different options and we recommend you read through it all to determine which is best for your research needs**

## Recommended Organization for Python  

For these examples, we will assume you have access to a group shared project directory located in `/projects/academic` or `/projects/industry`  If you do not already have a directory for yourself within your group's project directory, create one.  Then we recommend creating a directory structure for your software and Python environments.  We recommend, and use throughout this documentation, this structure where `yourgroup=your group's directory name` and `$USER=your username`  

```
ccruser@vortex ~ $ mkdir /projects/academic/yourgroup/$USER  
ccruser@vortex ~ $ mkdir /projects/academic/yourgroup/$USER/software
ccruser@vortex ~ $ mkdir /projects/academic/yourgroup/$USER/software/python  
ccruser@vortex ~ $ mkdir /projects/academic/yourgroup/$USER/software/python/venvs
ccruser@vortex ~ $ mkdir /projects/academic/yourgroup/$USER/software/anaconda
ccruser@vortex ~ $ mkdir /projects/academic/yourgroup/$USER/software/anaconda/envs
```

!!! Note  
    Not all users have access to a shared project directory.  Please verify your access via [ColdFront](../portals/coldfront.md).  

## Using CCR's Python Installation  

CCR provides as part of the currently supported toolchains.  We do not recommend using a version included within the operating system nor the one provided in CCR's compatibility layer.  These can differ across login and compute nodes and can be replaced with newer versions, potentially affecting your project.  These are also compiled to make the best use out of the architecture you're running on rather than offering one solution for the lowest common denominator.  Rather, using one contained in CCR's software repository toolchain provides you the most flexibility and usability across all CCR systems.  We highly recommend using python virtual environments for your projects.  A python virtual environment can be created using a specific version of python and can be used in isolation of other environments.  This is convenient if your projects require different versions of Python packages or have differing dependencies.  Within the virtual environment you can install additional Python packages  These virtual environments can be stored in your home directory or within your group's project directory making them available to other members of your group.  


### Python software modules

Find and display the available Python modules using the `module spider` command, then load the version of Python you'd like to use.  If you have no requirements, we recommend loading the latest.  The spider output will tell you if there are other modules you must load prior to loading your selected python. For example:  
```
ccruser@vortex ~ $ module spider python  
------------------------------------------------------------------------------------------------------------
  python:
------------------------------------------------------------------------------------------------------------
    Description:
      Python is a programming language that lets you work more quickly and integrate your systems more
      effectively.

     Versions:
        python/3.9.5-bare
        python/3.9.5
        python/3.9.6-bare
        python/3.9.6
     Other possible modules matches:
        ipython

ccruser@vortex ~ $ module spider python/3.9.6    
------------------------------------------------------------------------------------------------------------
  python: python/3.9.6
------------------------------------------------------------------------------------------------------------
    Description:
      Python is a programming language that lets you work more quickly and integrate your systems more
      effectively.

    Properties:
      Tools for development

    You will need to load all module(s) on any one of the lines below before the "python/3.9.6" module is available to load.

      gcccore/11.2.0

    This module provides the following extensions:

       alabaster/0.7.12 (E), appdirs/1.4.4 (E), asn1crypto/1.4.0 (E), atomicwrites/1.4.0 (E), attrs/21.2.0 (E), Babel/2.9.1 (E), backports.entry_points_selectable/1.1.0 (E), backports.functools_lru_cache/1.6.4 (E), bcrypt/3.2.0 (E), bitstring/3.1.9 (E), blist/1.3.6 (E), CacheControl/0.12.6 (E), cachy/0.3.0 (E), certifi/2021.5.30 (E), cffi/1.14.6 (E), chardet/4.0.0 (E), charset-normalizer/2.0.4 (E), cleo/0.8.1 (E), click/8.0.1 (E), clikit/0.6.2 (E), colorama/0.4.4 (E), crashtest/0.3.1 (E), cryptography/3.4.7 (E), Cython/0.29.24 (E), decorator/5.0.9 (E), distlib/0.3.2 (E), docopt/0.6.2 (E), docutils/0.17.1 (E), ecdsa/0.17.0 (E), filelock/3.0.12 (E), flit-core/3.3.0 (E), flit/3.3.0 (E), fsspec/2021.7.0 (E), future/0.18.2 (E), glob2/0.7 (E), html5lib/1.1 (E), idna/3.2 (E), imagesize/1.2.0 (E), importlib_metadata/4.6.3 (E), importlib_resources/5.2.2 (E), iniconfig/1.1.1 (E), intervaltree/3.1.0 (E), intreehooks/1.0 (E), ipaddress/1.0.23 (E), jeepney/0.7.1 (E), Jinja2/3.0.1 (E), joblib/1.0.1 (E), jsonschema/3.2.0 (E), keyring/21.2.0 (E), keyrings.alt/4.1.0 (E), liac-arff/2.5.0 (E), lockfile/0.12.2 (E), MarkupSafe/2.0.1 (E), mock/4.0.3 (E), more-itertools/8.8.0 (E), msgpack/1.0.2 (E), netaddr/0.8.0 (E), netifaces/0.11.0 (E), nose/1.3.7 (E), packaging/20.9 (E), paramiko/2.7.2 (E), pastel/0.2.1 (E), pathlib2/2.3.6 (E), paycheck/1.0.2 (E), pbr/5.6.0 (E), pexpect/4.8.0 (E), pip/21.2.2 (E), pkginfo/1.7.1 (E), platformdirs/2.2.0 (E), pluggy/0.13.1 (E), poetry-core/1.0.3 (E), poetry/1.1.7 (E), psutil/5.8.0 (E), ptyprocess/0.7.0 (E), py/1.10.0 (E), py_expression_eval/0.3.13 (E), pyasn1/0.4.8 (E), pycparser/2.20 (E), pycrypto/2.6.1 (E), Pygments/2.9.0 (E), pylev/1.4.0 (E), PyNaCl/1.4.0 (E), pyparsing/2.4.7 (E), pyrsistent/0.18.0 (E), pytest/6.2.4 (E), python-dateutil/2.8.2 (E), pytoml/0.1.21 (E), pytz/2021.1 (E), regex/2021.8.3 (E), requests-toolbelt/0.9.1 (E), requests/2.26.0 (E), scandir/1.10.0 (E), SecretStorage/3.3.1 (E), semantic_version/2.8.5 (E), setuptools-rust/0.12.1 (E), setuptools/57.4.0 (E), setuptools_scm/6.0.1 (E), shellingham/1.4.0 (E), simplegeneric/0.8.1 (E), simplejson/3.17.3 (E), six/1.16.0 (E), snowballstemmer/2.1.0 (E), sortedcontainers/2.4.0 (E), sphinx-bootstrap-theme/0.7.1 (E), Sphinx/4.1.2 (E), sphinxcontrib-applehelp/1.0.2 (E), sphinxcontrib-devhelp/1.0.2 (E), sphinxcontrib-htmlhelp/2.0.0 (E), sphinxcontrib-jsmath/1.0.1 (E), sphinxcontrib-qthelp/1.0.3 (E), sphinxcontrib-serializinghtml/1.1.5 (E), sphinxcontrib-websupport/1.2.4 (E), tabulate/0.8.9 (E), threadpoolctl/2.2.0 (E), toml/0.10.2 (E), tomlkit/0.7.2 (E), typing_extensions/3.10.0.0 (E), ujson/4.0.2 (E), urllib3/1.26.6 (E), virtualenv/20.7.0 (E), wcwidth/0.2.5 (E), webencodings/0.5.1 (E), wheel/0.36.2 (E), xlrd/2.0.1 (E), zipfile36/0.1.3 (E), zipp/3.5.0 (E)

ccruser@vortex ~ $ module load gcccore/11.2.0 python/3.9.6  
ccruser@vortex ~ $ which python
/cvmfs/soft.ccr.buffalo.edu/versions/2023.01/easybuild/software/avx512/Compiler/gcccore/11.2.0/python/3.9.6/bin/python  

```
### Python Virtual Environments  

You can make as many virtual environments as you need for various projects you're working on.  These can be stored in your home or project directory.  Once you've created the virtual environment, you activate it and then install additional Python packages as needed.  

Make a directory to store your virtual environments (if not already done so above):  
`mkdir /projects/academic/yourgroup/$USER/python/venvs`  
Create a virtual environment, naming it appropriately for your use case:  
`python -m venv /projects/academic/yourgroup/$USER/python/venvs/myproject`  
Activate the virtual environment:  
`source /projects/academic/yourgroup/$USER/python/venvs/myproject/bin/activate`  
You will then see you're in your virtual environment:  
`(myproject) [ccruser@vortex:~]$`  
To deactivate the python environment:  
`(myproject) [ccruser@vortex:~]$ deactivate`  

#### Installing Python Packages  

With your Python virtual environment activated, we recommend using the `pip` package manager to install and uninstall Python packages.  First, install and update pip, then list the currently installed packages within your virtual environment.  At this point, you can install additional packages. Here we show installing the `matplotlib` package as an example, which installs additional packages it depends on.

```
(myproject) [ccruser@vortex:~]$ pip install --upgrade pip
(myproject) [ccruser@vortex:~]$ pip list  
Package    Version
---------- -------
pip        22.3.1
setuptools 56.0.0
style      1.1.0
update     0.0.1
(myproject) [ccruser@vortex:~]$ pip install matplotlib
Collecting matplotlib
  Downloading matplotlib-3.6.2-cp39-cp39-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (11.8 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 11.8/11.8 MB 98.7 MB/s eta 0:00:00
Collecting packaging>=20.0
  Downloading packaging-22.0-py3-none-any.whl (42 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 42.6/42.6 kB 13.2 MB/s eta 0:00:00
Collecting pyparsing>=2.2.1
  Downloading pyparsing-3.0.9-py3-none-any.whl (98 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 98.3/98.3 kB 23.1 MB/s eta 0:00:00
Collecting kiwisolver>=1.0.1
  Downloading kiwisolver-1.4.4-cp39-cp39-manylinux_2_12_x86_64.manylinux2010_x86_64.whl (1.6 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.6/1.6 MB 119.0 MB/s eta 0:00:00
Collecting pillow>=6.2.0
  Downloading Pillow-9.3.0-cp39-cp39-manylinux_2_28_x86_64.whl (3.3 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 3.3/3.3 MB 164.7 MB/s eta 0:00:00
Collecting numpy>=1.19
  Downloading numpy-1.24.0-cp39-cp39-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (17.3 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 17.3/17.3 MB 117.4 MB/s eta 0:00:00
Collecting python-dateutil>=2.7
  Downloading python_dateutil-2.8.2-py2.py3-none-any.whl (247 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 247.7/247.7 kB 41.2 MB/s eta 0:00:00
Collecting contourpy>=1.0.1
  Downloading contourpy-1.0.6-cp39-cp39-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (296 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 296.3/296.3 kB 62.0 MB/s eta 0:00:00
Collecting fonttools>=4.22.0
  Downloading fonttools-4.38.0-py3-none-any.whl (965 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 965.4/965.4 kB 114.8 MB/s eta 0:00:00
Collecting cycler>=0.10
  Downloading cycler-0.11.0-py3-none-any.whl (6.4 kB)
Collecting six>=1.5
  Downloading six-1.16.0-py2.py3-none-any.whl (11 kB)
Installing collected packages: six, pyparsing, pillow, packaging, numpy, kiwisolver, fonttools, cycler, python-dateutil, contourpy, matplotlib
Successfully installed contourpy-1.0.6 cycler-0.11.0 fonttools-4.38.0 kiwisolver-1.4.4 matplotlib-3.6.2 numpy-1.24.0 packaging-22.0 pillow-9.3.0 pyparsing-3.0.9 python-dateutil-2.8.2 six-1.16.0

(myproject) [ccruser@vortex:~]$ pip list
Package         Version
--------------- -------
contourpy       1.0.6
cycler          0.11.0
fonttools       4.38.0
kiwisolver      1.4.4
matplotlib      3.6.2
numpy           1.24.0
packaging       22.0
Pillow          9.3.0
pip             22.3.1
pyparsing       3.0.9
python-dateutil 2.8.2
setuptools      56.0.0
six             1.16.0
style           1.1.0
update          0.0.1

```

!!! Tip    
    There are times when installing one Python package may break your environment.  We strongly recommend making a copy of your virtual environment directory prior to installing additional packages so if something goes wrong you can remove the broken venv and replace it with the backup.  

#### Using your Virtual Environment  

You can now use the same virtual environment over and over again. Each time:

- Load the same environment modules that you loaded when you created the virtual environment, i.e. `gcccore/11.2.0 python/3.9.6`  
- Then activate the virtual environment using `source ENV/bin/activate` where `ENV=location of your virtual environment directory`  

#### Using a virtual environment in the OnDemand Jupyter Notebook app  

Coming soon!  


## Using CCR's SciPy Installation  

In addition to the base Python modules, CCR provides SciPy as a software module too.  [SciPy](https://www.scipy.org/) provides algorithms for optimization, integration, interpolation, eigenvalue problems, algebraic equations, differential equations, statistics and many other classes of problems.   

First use `module spider` to see what versions of `scipy` CCR has available.  The `scipy-bundle` module includes many extensions.  Use the `module spider` command with the version number to see the list of all extensions and their versions included with that scipy installation.  This will also give you information about which modules need to be loaded prior to loading the `scipy-bundle`  Then use the `module load` command to load all prerequisites and the `scipy-bundle` as shown here:     

```
ccruser@vortex ~ $ module spider scipy-bundle  

------------------------------------------------------------------------------------------------------------
  scipy-bundle:
------------------------------------------------------------------------------------------------------------
    Description:
      Bundle of Python packages for scientific software

     Versions:
        scipy-bundle/2021.10

------------------------------------------------------------------------------------------------------------
  For detailed information about a specific "scipy-bundle" package (including how to load the modules) use the module's full name.
  Note that names that have a trailing (E) are extensions provided by other modules.
  For example:

     $ module spider scipy-bundle/2021.10
------------------------------------------------------------------------------------------------------------

ccruser@vortex ~ $ module spider scipy-bundle/2021.10  

------------------------------------------------------------------------------------------------------------
  scipy-bundle: scipy-bundle/2021.10
------------------------------------------------------------------------------------------------------------
    Description:
      Bundle of Python packages for scientific software


    You will need to load all module(s) on any one of the lines below before the "scipy-bundle/2021.10" module is available to load.

      gcc/11.2.0  openmpi/4.1.1

    This module provides the following extensions:

       beniget/0.4.1 (E), Bottleneck/1.3.2 (E), deap/1.3.1 (E), gast/0.5.2 (E), mpi4py/3.1.1 (E), mpmath/1.2.1 (E), numexpr/2.7.3 (E), numpy/1.21.3 (E), pandas/1.3.4 (E), ply/3.11 (E), pythran/0.10.0 (E), scipy/1.7.1 (E)

    Help:

      Description
      ===========
      Bundle of Python packages for scientific software

ccruser@vortex ~ $ module load gcc/11.2.0 openmpi/4.1.1 scipy-bundle
ccruser@vortex ~ $ module load scipy-bundle  

```


## Using Anaconda Python  

Anaconda Python is a very popular in the scientific community as it provides thousands of packages and an easy method for users to create and distribute their own via the Anaconda repository.  This can be very convenient for novice users and is a useful solution for simplifying the management of Python and scientific libraries on your personal computer or laptop.  However, it may not always be the most efficient way to utilize the high performance computing environment at CCR.  We encourage users to consider using the Python compiled and optimized for the processor architectures on CCR's compute nodes which will allow for the best efficiency when running jobs regardless of where in the heterogenous clusters your jobs run. The module system takes care of loading the appropriate version based on what node you're running on.  If you'd like to make use of CCR's Anaconda installation, we provide a base environment which has the standard Anaconda packages installed.  

### Configuring conda with `.condarc`  

The conda package manager allows modification of default settings to be done through a text file known as the `.condarc`. This file exists within a user’s `$HOME` directory and can be quickly be accessed using the file’s full path at `~/.condarc`.

Your `$HOME` directory (located in `/user/$USER`) is allotted a [small quota](/hpc/storage#enterprise-level-network-attached-storage). By default, conda puts all package source code and environments in your `$HOME` directory causing you to quickly run out of space. The steps here modify the conda configuration file to change the default locations for packages and environments to your group's shared project directory, as [described above](#recommended-organization-for-python).  

Open your `.condarc` file in your favorite text editor (e.g., nano, vim, [OnDemand Files app](/portals/ood#files-app)) and paste the following four lines (modifying directory path names as necessary for your individual setup):  

!!! Note  
    This file may not exist yet – if not, just create a new file with this name

```
pkgs_dirs:
  - /projects/academic/yourgroup/$USER/.conda_pkgs
envs_dirs:
  - /projects/yourgroup/$USER/software/anaconda/envs
```
Then save and exit the file. You won’t need to perform this step again – it’s permanent unless you modify `.condarc` later.

The `.condarc` file provides a variety of settings that can be detailed to speed up your workflows. For more information on `.condarc`, check out the [Anaconda documentation](https://docs.conda.io/projects/conda/en/latest/user-guide/configuration/use-condarc.html).  


### Using CCR's Anaconda Installation  

View available Anaconda distributions using the `module spider` command.  Then load the version you'd like to use as shown here:  

```
ccruser@vortex ~ $ module spider anaconda
------------------------------------------------------------------------------------------------------------
  anaconda3: anaconda3/2022.05
------------------------------------------------------------------------------------------------------------
    Description:
      Built to complement the rich, open source Python community, the Anaconda platform provides an
      enterprise-ready data analytics platform that empowers companies to adopt a modern open data science
      analytics architecture.


    This module can be loaded directly: module load anaconda3/2022.05


ccruser@vortex ~ $ module load anaconda3
ccruser@vortex ~ $ which python
/cvmfs/soft.ccr.buffalo.edu/versions/2023.01/easybuild/software/Core/anaconda3/2022.05/bin/python
```

#### Which environment to use?  

CCR offers a standard Anaconda environment that contains hundreds of packages.  However, there are thousands of conda packages out there and you may need one we don't have installed.  So what do you do?  

__1. Use one of CCR's pre-installed environments.__  

* Pros: You can begin using one of these immediately, and they contain many of the most widely used python packages.  
* Cons: These are root-owned environments, so you **can not** add additional packages.  CCR does not accept requests to install additional packages into our standard conda environments.   

or  

__2. Create your own custom environment(s).__  

* Pros: You own these, so you can add packages as needed, control package versions, etc.  
* Cons: There really aren't any cons, other than the time needed to create a custom environment (usually 5-30 minutes depending on the number of packages you install). You can create one to use for all your work or you can create many to use for different purposes or to better control versions and dependencies.   

#### Using CCR's standard environment  

After loading a CCR Anaconda module, use [conda commands](#basic-conda-commands-to-get-you-started) to view the included Python packages, see the available environment(s), and activate the base environment as shown here:  

```
ccruser@vortex ~ $ conda list
# packages in environment at /cvmfs/soft.ccr.buffalo.edu/versions/2023.01/easybuild/software/Core/anaconda3/2022.05:
#
# Name                    Version                   Build  Channel
_ipyw_jlab_nb_ext_conf    0.1.0            py39h06a4308_1
_libgcc_mutex             0.1                        main
_openmp_mutex             4.5                       1_gnu
aiohttp                   3.8.1            py39h7f8727e_1
aiosignal                 1.2.0              pyhd3eb1b0_0
alabaster                 0.7.12             pyhd3eb1b0_0
anaconda                  2022.05                  py39_0
anaconda-client           1.9.0            py39h06a4308_0
anaconda-navigator        2.1.4            py39h06a4308_0
anaconda-project          0.10.2             pyhd3eb1b0_0
anyio                     3.5.0            py39h06a4308_0
appdirs                   1.4.4              pyhd3eb1b0_0
argon2-cffi               21.3.0             pyhd3eb1b0_0
argon2-cffi-bindings      21.2.0           py39h7f8727e_0
arrow                     1.2.2              pyhd3eb1b0_0
astroid                   2.6.6            py39h06a4308_0
...
...
zlib                      1.2.12               h7f8727e_2
zope                      1.0              py39h06a4308_1
zope.interface            5.4.0            py39h7f8727e_0
zstd                      1.4.9                haebb681_0

ccruser@vortex ~ $ conda env list
# conda environments:
#
base                  *  /cvmfs/soft.ccr.buffalo.edu/versions/2023.01/easybuild/software/Core/anaconda3/2022.05

ccruser@vortex ~ $ eval "$(/cvmfs/soft.ccr.buffalo.edu/versions/2023.01/easybuild/software/Core/anaconda3/2022.05/bin/conda shell.bash hook)"

(base) ccruser@vortex ~ $
```
!!! Warning  
    Do NOT add the eval statement to your `.bashrc` file!  

You will know that you have properly activated the environment if you see `(base)` in front of your prompt.  If everything you need to use is contained in the CCR base environment, you're done!  If not, you will need to create your own environment as described in the next section.  

#### Creating your own custom environment  

NOTE: In this example, we're using the suggestion directory structure as [described above](#recommended-organization-for-python)

**Step 1:** If you haven't already done so, configure your `.condarc` file to [point to an alternate location](#configuring-conda-with-condarc) you have permission to write to.  Otherwise it will try creating an environment in CCR's software repository which will fail.  

**Step 2:** Initialize Anaconda if you haven't already done so:  

```
ccruser@vortex ~ $ module load anaconda3
cruser@vortex ~ $ eval "$(/cvmfs/soft.ccr.buffalo.edu/versions/2023.01/easybuild/software/Core/anaconda3/2022.05/bin/conda shell.bash hook)"

(base) ccruser@vortex ~ $
```
**Step 3:**  Create a custom environment  

Here we create a new environment called `mycustomenv` (you can name it whatever you want) and you'll see it's saved to the directory we specify in our `.condarc` file  

```
(base) ccruser@vortex ~ $ conda create -n mycustomenv
Collecting package metadata (current_repodata.json): done
Solving environment: done


==> WARNING: A newer version of conda exists. <==
  current version: 4.12.0
  latest version: 22.11.1

Please update conda by running

    $ conda update -n base -c defaults conda

## Package Plan ##

  environment location: /projects/academic/yourgroup/$USER/software/anaconda/envs/mycustomenv


Proceed ([y]/n)? y
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use
#
#     $ conda activate mycustomenv
#
# To deactivate an active environment, use
#
#     $ conda deactivate
```

!!! Note  
    Though you may see a warning to update conda, as shown in this example, you will not be able to.  If you need a different version of Anaconda, you will need to [install your own](#installing-your-own-anaconda-or-miniconda).

**__Specifying Python version for your custom environment__**

When creating a custom environment you can specify a Python version to use.  For example:  

```
(base) ccruser@vortex ~ $ conda create -n mycustomenv python=3.10
```
You will be presented with a list of packages it needs to update or install and given an opportunity to move forward or exit the installation.  

**Step 4:** Activate your new environment  

```
(base) ccruser@vortex ~ $ conda activate mycustomenv
(mycustomenv) ccruser@vortex ~ $
```
There are no packages installed in your new environment so you'll need to install whatever your project requires.  

#### Installing Anaconda Packages  

The best way to install packages in an Anaconda environment is to install everything you need with one command, because it forces conda to resolve package conflicts. For example:  

```
(mycustomenv) ccruser@vortex ~ $ conda install numpy scipy tensorflow
```

For more information on managing conda enviornments, [check out Anaconda's documentation here.](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html)  

#### Troubleshooting

If you are having trouble loading a package, you can use `conda list` or `pip freeze` to list the available packages and their version numbers in your current conda environment. Use `conda install <package>` to add a new package or `conda install <package==version>` for a specific version; e.g., `conda install numpy=1.16.2`.

Sometimes conda environments can "break" if two packages in the environment require different versions of the same shared library. In these cases you try a couple of things.
* Reinstall the packages all within the same install command (e.g., `conda install <package1> <package2>`). This forces conda to attempt to resolve shared library conflicts.
* Create a new environment and reinstall the packages you need (preferably installing all with the same `conda install` command, rather than one-at-a-time, in order to resolve the conflicts).

### Basic conda commands to get you started

| Command | Function |
|---------|----------|
| `conda list` | List the packages currently installed in the environment |
| `conda search <package>` | Searches the Anaconda package channel for a package named `<pakage>` |
| `conda install <package>` | Installs a package named `<package>` to your currently loaded environment |
| `conda uninstall <package>` | Uninstalls a package named `<package>` from your currently loaded environment |
| `conda env list` | List the conda environments currently available |
| `conda create <env>` | Creates a new anaconda enviornment named `<env>` |
| `conda remove --name <env> --all` | Removes an environment named `<env>` |
| `conda deactivate` | Deactivates current enviornment |



### Installing your own Anaconda or Miniconda

Users are able to install their own software within their home or group's project directory.  Anaconda has a very large storage footprint so we do **NOT** recommend installing this in your home directory.  In fact, unless you absolutely need the full Anaconda software set, we highly recommend using miniconda instead.  Users should refer to the [Anaconda](https://www.anaconda.com/) or [Miniconda](https://docs.conda.io/en/latest/miniconda.html) documentation as this is outside of the scope of CCR support.  For reference, you will need to download the appropriate installer for Linux (x86 64-Bit).  


If you move ahead with installing Anaconda yourself, please be aware of the following:  

  - Anaconda very often installs software (compilers, scientific libraries etc.) which already exist on our clusters as modules, with a configuration that is not optimal.  
  - It installs binaries which are not optimized for the processor architecture on our clusters.  
  - It makes incorrect assumptions about the location of various system libraries.  
  - Anaconda uses the `$HOME` directory for its installation, where it writes an enormous number of files. A single Anaconda installation can easily absorb more than half of your quota for your home directory.  Please be sure to use the `--prefix` option and direct the installation to your group's project directory instead and setup your `.condarc` to point to an alternative location than your home directory as [described here](#configuring-conda-with-condarc).  
  - Anaconda modifies the `$HOME/.bashrc` file, which can easily cause conflicts.  Please respond `No` when prompted to initialize the Anaconda installation OR edit your `$HOME/.bashrc` file to remove the lines added by the installer.  This will be everything between the two `>>> conda initialize >>>` lines.  

!!! Warning  
    We can't stress that last item enough.  Activating a conda environment in your `.bashrc` file **WILL break** things including, but not limited to, command line quota checking, OnDemand desktops, and Jupyter Notebooks

Refer to the [custom environment section of the Anaconda docs](#creating-your-own-custom-environment) for information on setting up your own environments after installing your personal version of Anaconda.  Once your software is installed, you can create your own private software module for you and/or your group to use.  Please see our [documentation on the module system](modules.md).  
