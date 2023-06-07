## Installing Libraries in R  

CCR provides the base R software.  R is available as a software module.  Run `module spider r` command to see what is available as modules and then use the `module load some_module` command to load your preferred version.  **NOTE: The `module spider` command will indicate if additional modules are required to be loaded prior to loading the software module.**  Once loaded you'll be able to install additional packages or libraries in your local environment - either in your home or project directory.  Here we cover examples for R.  

You need to begin by loading an R module; there will typically be several versions available and you can see a list of all of them using the command `module spider r`  You can load load a particular R module using a command like: `module load gcc/11.2.0  openmpi/4.1.1 r/4.2.0`  

Start the R interpreter using the command `R`  

Nearly 20,000 packages are available for R.  To see the full list of R packages available, please visit the R project page: https://cran.r-project.org/  If you want to use a package for R that is not already installed by CCR, you can install your own packages by either downloading the package and installing it or pointing to the R package library and installing directly from there.  The two options are shown below.  Many R packages are developed using the GNU family of compilers so we recommend that you load a gcc module before trying to install any R packages, as shown above. Use the same version of the gcc for all packages you install.  

!!! Tip  
    Make a subdirectory in your home or project directory for R library storage, such as `/projects/academic/yourgroup/$USER/software/$CCR_VERSION/rlibs` used in our examples.  More info on our recommended nomenclature [here](about.md)    


### Installation Options  

_**Option 1: Download and install R packages in your home or project directory:**_

Download the R package you want to install.  In this example, we demonstrate the 'readr' package:  
```
[ccruser@vortex ~]$ wget https://cran.r-project.org/src/contrib/readr_2.1.3.tar.gz  
```

Install the downloaded package using the following command, making sure to point to your rlibs directory.  NOTE: this is done outside of R:  
```
[ccruser@vortex ~]$ R CMD INSTALL -l /projects/academic/yourgroup/$USER/software/$CCR_VERSION/rlibs/ readr_2.1.3.tar.gz  
```

_**Option 2: Install directly from the R Project repository:**_

Load the R module and any dependencies (`module spider r'), then launch R.  In the R session, install the package by specifying the package name, R project repository, and your R library location in your home or project directory.  In this example, we are installing ggplot2:  

```
install.packages("ggplot2", repos = "http://cran.r-project.org", lib = "/projects/academic/yourgroup/$USER/software/$CCR_VERSION/rlibs")  
```  

!!! Tip "Don't want to specify the location each time?"  
    Create a file named .Renviron in your home directory (or edit an existing one) and point R to use your alternate directory.  Include the line (editing for your use case): `R_LIBS_USER=/projects/academic/yourgroup/$USER/software/$CCR_VERSION/rlibs"`  
    Each time R starts it will use this library directory for installations and to search for existing installations.  


**Common Installation Error**

`ERROR: 'configure' exists but is not executable -- see the 'R Installation and Administration Manual'`

If you are trying to install a R library and see this error, it is trying to create a temporary directory to use during the installation and isn't able to.  To resolve this, create a temporary directory in your home or project directory then, after starting R, set the variable before attempting the installation:

```
[ccruser@vortex ~]$ R
> dir.create("/user/$USER/tmp/")
> Sys.setenv(TMPDIR="/user/$USER/tmp/")
> install.packages(“package_name”)
```  

The directory will be used during installation and the temporary files removed when the install is complete.  

!!! Note  
    Not all packages or dependencies will work with the version(s) of R CCR provides.  If this is something your research requires and the installation methods above don't work for you, you will need to install your own version of R or use R in a singularity container.  These topics are beyond the scope of this document.  

**To load an R package from alternate library installation location:**  
```
[ccruser@vortex ~]$ module load R
[ccruser@vortex ~]$ R
library(package_name, lib.loc="/projects/academic/yourgroup/$USER/software/$CCR_VERSION/rlibs/")
```

NOTE: If you use the above tip and create a `~/.Renviron` file you do not need to specify the location.  R will automatically look there if it doesn't find it in the site installation location.  


**Installing R packages from within the R Studio GUI:**  

Whether using CCR's R Studio app in OnDemand or launching it from the command line, users can install R packages into their home or project directories.  Launch R Studio and navigate to the Tools menu and click on `Install Packages`

Make sure the installation directory is specifying either your home directory or a subdirectory within your group's shared project directory and check the `Install dependencies` option.  You may get a warning that the R Studio version needs to be updated.  You will  not be able to do that as it is maintained by CCR.  


###  Installing Bioconductor Libraries  

Bioconductor has it's own package manager.  If you need a library that is not already installed, you can request that CCR installs it - 
[see here for instructions](../software/building.md#software-build-requests) - or install it yourself similar to R libraries shown above.  

```
[ccruser@vortex ~]$ module spider bioconductor  
[ccruser@vortex ~]$ module load gcc/11.2.0  openmpi/4.1.1 r-bundle-bioconductor/3.15-R-4.2.0
[ccruser@vortex ~]$ R
> BiocManager::install('GenomeInfoDb', lib="/projects/academic/yourgroup/$USER/software/$CCR_VERSION/rlibs")
Bioconductor version 3.15 (BiocManager 1.30.17), R 4.2.0 (2022-04-22)
Installing package(s) 'GenomeInfoDb'
trying URL 'https://bioconductor.org/packages/3.15/bioc/src/contrib/GenomeInfoDb_1.32.4.tar.gz'
Content type 'application/x-tar' length 3454932 bytes (3.3 MB)
==================================================
downloaded 3.3 MB

* installing *source* package ‘GenomeInfoDb’ ...
** using staged installation
** R
** inst
** byte-compile and prepare package for lazy loading
** help
*** installing help indices
** building package indices
** installing vignettes
** testing if installed package can be loaded from temporary location
** testing if installed package can be loaded from final location
** testing if installed package keeps a record of temporary installation path
* DONE (GenomeInfoDb)

The downloaded source packages are in
        ‘/tmp/RtmpeIsIDT/downloaded_packages’  
```

!!! Tip "Reminder!"  
    You don't have to specify the location of the installation directory if you setup a `.Renviron` file in your home directory.  See the tip above in the R library installation section.  


### References  

There are many ways you can customize R and Bioconductor for usage and for installations.  If you want to keep libraries for multiple versions of these software products, we highly recommend you read through the documentation.  

[R Documentation](https://www.r-project.org/other-docs.html)  
[CRAN Documentation](https://cran.r-project.org/other-docs.html#english)  
[Bioconductor Documentation](https://www.bioconductor.org/)  
[Bioconductor Package Manager Documentation](https://cran.r-project.org/web/packages/BiocManager/vignettes/BiocManager.html)  



!!! Warning "Support Availability"  
    CCR supports the base installations of R and the R Bioconductor bundle.  Any libraries you install outside of these environments are not supported.  We recommend using resources available on the internet for assistance with any issues you may run into.   