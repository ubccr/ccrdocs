# Installing Perl Packages or R libraries

CCR provides the base Perl and R software packages.  Perl is available in the compatibility layer and also as a software module.  Run `perl --version` to see the compatibility layer installation version.  Use the `module spider perl` or `module spider r` command to see what is available as modules and then use the `module load some_module` command to load your preferred version.  **NOTE: The `module spider` command will indicate if additional modules are required to be loaded prior to loading the software module.**  Once loaded you'll be able to install additional packages or libraries in your local environment - either in your home or project directory.  Here we cover examples for Perl and  R.  More details on how to install Python packages and Anaconda modules can be [found here](python.md).  

## Perl Modules  

You can store Perl modules in your home directory or use a subdirectory in your project space to share with your entire group.  

NOTE:  In this example, `YourGroupDir` refers to the name of your group's project directory.  Most shared project directories will be found in `/projects/academic` (which we use in this example) but some are in `/projects/industry` or `/projects/academic/courses`  

**Home Directory Perl Module Setup**  

The first time you install Perl modules, a local cpan and perl5 directory will be created.  Accept the defaults here and it will be created in `/user/CCRusername/.cpan` and `/user/CCRusername/perl5`  The `cpan` utility will offer to append a variety of environment variable settings to your `.bashrc` file, which you should agree to. You can then type the command `quit` in the interface to exit the `cpan` software. **Before installing any Perl modules you will need to restart your shell or run `source ~/.bashrc` for these new settings to take effect.**  

```
[ccruser@vortex ~]$ module load gcccore/11.2.0
[ccruser@vortex ~]$ module load perl

[ccruser@vortex ~]$ cpan
...

Would you like me to configure as much as possible automatically? [yes]
...
What approach do you want?  (Choose 'local::lib', 'sudo' or 'manual')
 [local::lib]
...
```
When the initial configuration is done, you can install any of the more than 25,000 packages available on CPAN. For example:

```
[ccruser@vortex:~]$ cpan

cpan shell -- CPAN exploration and modules installation (v2.28)
Enter 'h' for help.

cpan[1]> install module-name

```

**Project Directory Perl Module Setup**  

In the above example during the initialization of cpan, our `.bashrc` file was modified with additional PERL environment variables.  This points cpan to install modules into your home directory.  To redirect these installations to a shared project directory, we must modify the `.bashrc` file to change the location these variables point to.  

!!! Warning  
    Make sure the subdirectories you want to use for cpan and perl5 are created or they will be created for you. NEVER use your global scratch directory for storing these files!   

Edit the `.bashrc` file in your home directory and change the PERL variables from your home directory path to the project diretory path you want to use.

```
[ccruser@vortex:~]$ vi ~.bashrc  

PATH="/projects/academic/YourGroupDir/perl5/bin${PATH:+:${PATH}}"; export PATH;
PERL5LIB="/projects/academic/YourGroupDir/perl5/lib/perl5${PERL5LIB:+:${PERL5LIB}}"; export PERL5LIB;
PERL_LOCAL_LIB_ROOT="/projects/academic/YourGroupDir/perl5${PERL_LOCAL_LIB_ROOT:+:${PERL_LOCAL_LIB_ROOT}}"; export PERL_LOCAL_LIB_ROOT;
PERL_MB_OPT="--install_base \"/projects/academic/YourGroupDir/perl5\""; export PERL_MB_OPT;
PERL_MM_OPT="INSTALL_BASE=/projects/academic/YourGroupDir/perl5"; export PERL_MM_OPT;
```  
Save the file and then restart your shell or run `source ~/.bashrc` for these new settings to take effect.  Next time you use cpan to install a Perl module it will be redirected to your shared project directory.  


## R Library Installation  

You need to begin by loading an R module; there will typically be several versions available and you can see a list of all of them using the command `module spider r`  You can load load a particular R module using a command like: `module load gcc/11.2.0  openmpi/4.1.1 r/4.2.0`  

Start the R interpreter using the command `R`  

Nearly 20,000 packages are available for R.  To see the full list of R packages available, please visit the R project page: https://cran.r-project.org/  If you want to use a package for R that is not already installed by CCR, you can install your own packages by either downloading the package and installing it or pointing to the R package library and installing directly from there.  The two options are shown below.  Many R packages are developed using the GNU family of compilers so we recommend that you load a gcc module before trying to install any R packages, as shown above. Use the same version of the gcc for all packages you install.  

!!! Tip  
    Make a subdirectory in your home or project directory for R library storage, such as `/user/CCRusername/rlibs` used in our examples    

_**Option 1: Download and install R packages in your home or project directory:**_

Download the R package you want to install.  In this example, we demonstrate the 'readr' package:  
`[ccruser@vortex ~]$ wget https://cran.r-project.org/src/contrib/readr_2.1.3.tar.gz`

Install the downloaded package using the following command, making sure to point to your rlibs directory.  NOTE: this is done outside of R:  
`[ccruser@vortex ~]$ R CMD INSTALL -l /user/ccruser/rlibs readr_2.1.3.tar.gz`  

_**Option 2: Install directly from the R Project repository:**_

Load your preferred R module and GCC, then launch R.  In the R session, install the package by specifying the package name, R project repository, and your R library location in your home or project directory.  In this example, we are installing ggplot2:  

`install.packages("ggplot2", repos = "http://cran.r-project.org", lib = "/user/ccruser/rlibs")`  


**Common Installation Error**

`ERROR: 'configure' exists but is not executable -- see the 'R Installation and Administration Manual'`

If you are trying to install a R library and see this error, it is trying to create a temporary directory to use during the installation and isn't able to.  To resolve this, create a temporary directory in your home or project directory then, after starting R, set the variable before attempting the installation:

```
[ccruser@vortex ~]$ R
> dir.create("/user/username/tmp/")
> Sys.setenv(TMPDIR="/user/username/tmp/")
> install.packages(“package_name”)
```
The directory will be used during installation and the temporary files removed when the install is complete.  

**To load an R package from user (or projects) space:**  
```
[ccruser@vortex ~]$ module load R
[ccruser@vortex ~]$ R
library(package_name, lib.loc="/user/ccruser/rlibs/")
```

**Installing R packages from within the R Studio GUI:**  

Whether using CCR's R Studio app on OnDemand or launching it from the command line, users can install R packages into their home or project directories.  Launch R Studio and navigate to the Tools menu and click on 'Install Packages'

Make sure the installation directory is specifying either your home directory or a subdirectory within your group's shared project directory and check the "Install dependencies" option.

!!! Note  
    Not all packages or dependencies will work with the version(s) of R CCR provides.  If this is something your research requires and the installation methods above don't work for you, you may need to install your own version of R or use R in a singularity container.  These topics are beyond the scope of this document.  
