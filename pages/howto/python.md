# Python Options

There are many options for using Python and its derivates on CCR's systems.  CCR provides Python3, Anaconda, and SciPy via it's module system.  These are updated once per year with the oldest version being rotated out.  Users will see a warning when a module is loaded regarding it's planned deprecation, giving you advance notice to update your workflow.  


## Which option to use?  

This page describes the different Python installations and environments offered by CCR and we recommend you read through it all to determine which is best for your research needs or jump to the section you're interested in:  

- [Use CCR's base python modules](#using-ccrs-python-installation)  

    * [Using python virtual environments](#python-virtual-environments)  

- [Use CCR's anaconda module](#using-anaconda-python)  

      * [Using CCR's standard conda environment](#using-ccrs-standard-environment)  
      * [Create your own custom conda environments](#creating-your-own-custom-environment)  

- [Use CCR's SciPy python bundle module](#using-ccrs-scipy-installation) - contains common python scientific libraries pre-installed and may have everything you need to get your project started.  
<br>
- [Install your own anaconda or miniconda](#installing-your-own-anaconda-or-miniconda)



!!! Tip "Nomenclature Used"   
    For these examples, we assume you have access to a shared group project directory located in `/projects/academic` or `/projects/industry`  If you do not already have a directory for yourself within your group's project directory, we recommend you create one and then create a directory structure for your software and Python or Anaconda environments. However, how you organize your software is up to you and your research group.  Throughout this documentation, we use this structure where `yourgroup=your group's directory name` and `$USER=your username`  

    **Python and Anaconda environments can be quite large so we do not recommend you install these in your home directory.**   


## Using CCR's Python Installation  

CCR provides as python part of our software modules. We highly recommend using python virtual environments for your projects. A python virtual environment can be created using a specific version of python and can be used in isolation of other environments. This is convenient if your projects require different versions of Python packages or have differing dependencies. Within the virtual environment you can install additional Python packages These virtual environments can be stored in your home directory or within your group's project directory making them available to other members of your group.


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

    ....

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


