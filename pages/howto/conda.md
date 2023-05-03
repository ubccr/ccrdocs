## Using Anaconda Python  

Anaconda Python is a very popular in the scientific community as it provides thousands of packages and an easy method for users to create and distribute their own via the Anaconda repository.  This can be very convenient for novice users and is a useful solution for simplifying the management of Python and scientific libraries on your personal computer or laptop.  However, it may not always be the most efficient way to utilize the high performance computing environment at CCR.  **We encourage users to consider using the Python compiled and optimized for the processor architectures on CCR's compute nodes which will allow for the best efficiency when running jobs regardless of where in the heterogenous clusters your jobs run. The module system takes care of loading the appropriate version based on what node you're running on.**  If you'd like to make use of CCR's Anaconda installation, we provide a base environment, installed via Easy Build, which has the standard Anaconda packages installed.  CCR does not install additional packages into this environment nor are we able to provide support for user installation of packages. However, here we provide a few recommendations for best practices for proper setup of your conda environment, installation of packages into your environment, and using conda environments in batch jobs.  This documentation is provided as is and we highly recommend you refer to [Anaconda's documentation](https://docs.anaconda.com/) for the most up-to-date and accurate information on their software.    

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

#### Which conda environment should you use?  

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
ccruser@vortex ~ $ eval "$(/cvmfs/soft.ccr.buffalo.edu/versions/2023.01/easybuild/software/Core/anaconda3/2022.05/bin/conda shell.bash hook)"

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
