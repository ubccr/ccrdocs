==This document is a work in progress.  The example shown is a simple one and uses the `ccrsoft/2023.01` software release.  It does not address all the possible issues you might run into compiling and installing software.==

# Easybuild  

CCR staff utilize the Easybuild framework when installing software and this tool is made available to CCR users to install software themselves.  Easybuild ensures that the compilation and linking that happens during a software installation is done correctly and will work with our systems.  CCR staff do not offer courses on using Easybuild, nor are we able to troubleshoot issues you might run into.  However, there is excellent [documentation](https://docs.easybuild.io/) and [tutorials](https://tutorial.easybuild.io/) provided by Easybuild developers.  We provide this document to provide a bit of context to the Easybuild documentation and provide an example of using Easybuild to install a software package.   

## Easybuild and Modules  

One of the key features of EasyBuild is that it automatically generates environment modules which can be used to make a software package available in your session. In addition to defining standard Linux environment variables such as `PATH`, `CPATH` and `LIBRARY_PATH`, EasyBuild also defines some environment variables specific to EasyBuild, two of which may be particularly interesting to users:  

`EBROOT<name>`: Contains the full path to the location where the software `<name>` is installed.  
`EBVERSION<name>`: Contains the full version of the software `<name>` loaded by this module.  

For example, the module `java/11.0.16` defines:  
- `EBROOTJAVA: /cvmfs/soft.ccr.buffalo.edu/versions/2023.01/easybuild/software/Core/java/11.0.16`  
- `EBVERSIONJAVA: 11.0.16`  

You can see the environment variables defined by the `java/11.0.16` module using:  
```
CCRusername@login ~:$ module show java/11.0.16 |grep EB  
```

You can use these as variables on the command line and in scripts.  For example:  

```
CCRusername@login ~:$ cd $EBROOTJAVA
CCRusername@login ~:$ /cvmfs/soft.ccr.buffalo.edu/versions/2023.01/easybuild/software/Core/java/11.0.16$  
```

## Using Easybuild in your own account  

EasyBuild can be used to install software packages in your own account. However, in most cases, it is preferable to ask our technical support to install the software centrally for you. This will ensure that the software package is available on all of our clusters for all users. It will also avoid using up all your quota.  It is often difficult for us to troubleshoot problems when someone else is trying to install software, making it hard to provide support to you.  

!!! Note "When to use or not use Easybuild to install software in your account"  
    There are a few use cases in which you may want to use EasyBuild to install software in your own space (project space preferred over home directories):  
    - if you need a custom or modified build   
    - if you need to install a nightly build, or a version of a software which does not have a release number  
    - if there isn't an existing EB recipe and you want to create your own  
    - if we at CCR are not allowed to install the package centrally for licensing reasons, such as some commercial software packages (Gaussian, VASP and Materials Studio in particular)  

    On the contrary, you should not install software packages in your own space for the following reasons:  

    - if you need a different release version   
    - if you need a software package built using a different compiler, MPI or CUDA implementation  

    When in doubt, please ask [CCR Help](../help.md) for advice.

## What is a recipe

Writing a recipe from scratch will not be discussed here; you can find more about this in the [EasyBuild documentation](https://docs.easybuild.io/). Modifying a recipe for your particular situation is easier, and it is easier still to find a suitable recipe and use it unmodified.  

Recipes, also known as EasyConfig files, are text files containing the information EasyBuild needs to build a particular piece of software in a particular environment. They are named following this convention:

`<name>-<version>-<toolchain name>-<toolchain version>.eb`
where `<name>` is the name of the package, `<version>` is its version, `<toolchain name>` is the name of the toolchain used and `<toolchain version>` is its version. More on toolchains later.

### Installation recipes and logs  

EasyBuild keeps a copy of the recipe used to install each software package, as well as a detailed log inside the installation directory. This is accessible in the directory $EBROOT<name>/easybuild. For example, for the `java/11.0.16` module, the installation directory contains, among other things:  
- `$EBROOTJAVA/easybuild/Java-11.0.16.eb`  
- `$EBROOTJAVA/easybuild/easybuild-Java-11.0.16-20221206.215954.log.bz2`  

During your installation, you will see output indicating where the temporary log files for the build are located.  After completion of the install, the path of the full build log is output by Easybuild.  See more [here](#investigating-logs)  

## An Easybuild Example  

### Easybuild Background  

At CCR, we provide a set of [supported toolchains](../software/releases.md) and users are able to use Easybuild to install software for themselves without administrative privileges.  We provide instructions to get started [here](../software/building.md).  Some packages install quite easily and the `samtools` example provided in our documentation is one of those packages.  However, what happens if you want to install something that CCR doesn't offer, but you're not finding an exact match for a toolchain provided by CCR or the version of the software you want to run?  It's a bit of trial and error, to be honest.  And this is what CCR staff are doing on a daily basis as we work through the [installation requests](../software/building.md#software-build-requests) in our [GitHub repository](https://github.com/ubccr/software-layer/issues).

In this how-to section, we're going to take you through the process to provide you with the information you'll need to be off and running on your own Easybuild installation!

!!! Danger "STOP!"
    Before going forward, ensure that you've read the documentation on using CCR's [software modules](../software/modules.md) as some things have changed in the latest software release.  Are you SURE this software isn't already installed in the latest software release? Use the `module spider` command to search.  You can also check the CCR [GitHub repo](https://github.com/ubccr/software-layer/issues) for open & closed build requests.  Read the information about [building your own software](../software/building.md) and setting up a build environment.  If you're planning to make this software accessible to your entire research group, ensure you've got [this setup](../software/building.md#building-modules-for-your-group) correctly.  


Though you don't need to understand everything about an Easybuild recipe file to install software using Easybuild, we do recommend you [read this](https://docs.easybuild.io/writing-easyconfig-files/) and keep it handy to refer to should questions come up while you're editing these recipe files.  

Easyconfig files are named to include the toolchain and version:  
GNU compilers:  
[...]-foss-2021b.eb  
[...]-GCCcore-11.2.0.eb  

Intel compilers:  
[...]-intel-2022.00.eb  
[...]-iimpi-2022.00.eb  

The EasyBuild config repository contains a lot of recipes which may or may not compile with the toolchains CCR provides.  As a reminder, these are the [toolchains](../software/releases.md) CCR supports.  You must use a recipe for a supported toolchain when installing software using Easybuild.  If you try a recipe for an unsupported toolchain, Easybuild will attempt to install that toolchain for you.  You don't want this as it will take up too much disk space, take very long to build, and is highly likely that installation will fail. 

### What's in a toolchain  

Toolchains are a combination of compiler, MPI implementation, CUDA version, and mathematical libraries, which are used to compile the software package. CCR offers toolchains as modules and you can see what is included in a toolchain by looking at the module.  For example, if you load the `foss/2021b` module you'll see it includes:   
```
depends_on("gcc/11.2.0")
depends_on("openmpi/4.1.1")
depends_on("flexiblas/3.0.4")
depends_on("fftw/3.3.10")
depends_on("scalapack/2.1.0-fb")
```
These are automatically loaded for you when you load the `foss/2021b` module.  When a toolchain is a superset of other toolchains, it allows software packages built with the former to have dependencies on software packages built with the latter.

**When using Easybuild, do NOT use the CCR login nodes.**  Always use a [compile node](../software/building.md) or do this from a compute node in an [OnDemand desktop](../portals/ood.md#desktop-interactive-apps) session or [interactive job](../hpc/jobs.md#interactive-job-submission).  These installations can use a decent amount of disk space so we recommend you use your project directory for all software installations.  We do not recommend using your home directory as these have small quotas.  If you haven't already done so, create an `easybuild` directory in your group's project directory and set the [Easybuild build prefix](../software/building.md#building-modules-for-your-group) to that directory.  Reminder: this is just an example; you'll need to set the path name to your group's shared project directory, which may not be in `/projects/academic`      

```
CCRusername@login ~:$ ssh compile  
CCRusername@compile ~:$ mkdir /projects/academic/[YourGroupName]/easybuild   
CCRusername@compile ~:$ export CCR_BUILD_PREFIX=/projects/academic/[YourGroupName]/easybuild  
```
!!! Tip "Set Easybuild install path EVERY TIME"  
    The `CCR_BUILD_PREFIX` needs to be set each time you install software.  You're telling Easybuild where to put this particular installation.  [More details](../software/building.md#building-modules-for-your-group)   


### Example Easybuild Installation  

For this example, we're going to step through the process of building a software package called `aria2`  

First, we load the Easybuild module and search for an existing Easybuild (EB) recipe (**Reminder: don't do this on a login node!**):

```
$ module load easybuild  
$ eb --search aria2
== found valid index for /cvmfs/soft.ccr.buffalo.edu/versions/2023.01/easybuild/software/Core/easybuild/4.8.1/easybuild/easyconfigs, so using it...
 * /cvmfs/soft.ccr.buffalo.edu/versions/2023.01/easybuild/software/Core/easybuild/4.8.1/easybuild/easyconfigs/a/aria2/aria2-1.35.0-GCCcore-10.3.0.eb
 * /cvmfs/soft.ccr.buffalo.edu/versions/2023.01/easybuild/software/Core/easybuild/4.8.1/easybuild/easyconfigs/a/aria2/aria2-1.36.0-GCCcore-11.3.0.eb

```  

This output shows us that there are 2 existing EB recipes for `aria2` but neither of them are for a supported toolchain.  CCR provides GCC 11.2.0 in `ccrsoft/2023.01` so you could try either one of these EB recipe options.  However, in our experience, we've found it's best to try a toolchain in the same major version as one we have installed (as in GCCcore-11.x.x instead of 10.x.x or 12.x.x).  The recipe in the same major version will have dependency versions closest to what are already installed at CCR.  If we had to choose between a recipe for `foss-2021a` or `foss-2022b`, we'd go with `2021a` as it will more closely match the `foss/2021b` that CCR has installed in `ccrsoft/2023.01`.  If you pick something much older or newer, the less luck you'll have with your software getting installed properly.  Again, this is just our experience, YMMV (your mileage may vary).  

To attempt to install this, we must make a copy of the existing EB recipe and modify it.  The output above shows us where the EB recipe files are stored so we can easily copy to our home directory.  **NOTE: You must change the name of the EB recipe when you copy it, updating the toolchain version.**  

Here we update the name of the EB recipe from `aria2-1.36.0-GCCcore-11.3.0.eb` to `aria2-1.36.0-GCCcore-11.2.0.eb`  If you were to also change the version of the software package you're attempting to install, you need to change that in the EB recipe file name as well.  In this example, we're not doing that.  

```
$ cp /cvmfs/soft.ccr.buffalo.edu/versions/2023.01/easybuild/software/Core/easybuild/4.8.1/easybuild/easyconfigs/a/aria2/aria2-1.36.0-GCCcore-11.3.0.eb aria2-1.36.0-GCCcore-11.2.0.eb
```

This is what the file currently looks like:  

```
easyblock = 'ConfigureMake'

name = 'aria2'
version = '1.36.0'

homepage = 'https://aria2.github.io'
description = "aria2 is a lightweight multi-protocol & multi-source command-line download utility."

toolchain = {'name': 'GCCcore', 'version': '11.3.0'}

source_urls = ['https://github.com/aria2/aria2/releases/download/release-%(version)s']
sources = [SOURCE_TAR_GZ]
checksums = ['b593b2fd382489909c96c62c6e180054c3332b950be3d73e0cb0d21ea8afb3c5']

builddependencies = [
    ('binutils', '2.38'),
    ('Autotools', '20220317'),
    ('CppUnit', '1.15.1'),
]

dependencies = [
    ('zlib', '1.2.12'),
    ('libxml2', '2.9.13'),
    ('SQLite', '3.38.3'),
    ('c-ares', '1.18.1'),
    ('OpenSSL', '1.1', '', SYSTEM),
]

configopts = "--without-gnutls --with-openssl --enable-libaria2 --enable-static"

runtest = 'check'

sanity_check_paths = {
    'files': ['bin/aria2c'],
    'dirs': ['share'],
}

sanity_check_commands = ["aria2c --help"]

moduleclass = 'tools'
```

Open the recipe file in your favorite editor.  The first thing to change is the toolchain line - change from `11.3.0` to `11.2.0`:  
```
toolchain = {'name': 'GCCcore', 'version': '11.2.0'}
```

Then we go through all the dependencies and build dependencies, if there are any, and verify the versions.  We check to see if these packages are already installed in the `ccrsoft/version` that we're building this for (in this example `ccrsoft/2023.01`).  If so, verify the versions are the same as we have listed in the EB recipe and change any that are not.  For this example, our build dependencies (these are required in order to build the software) and dependencies (these are required to run the software) are:  

```
builddependencies = [
    ('binutils', '2.38'),
    ('Autotools', '20220317'),
    ('CppUnit', '1.15.1'),
]

dependencies = [
    ('zlib', '1.2.12'),
    ('libxml2', '2.9.13'),
    ('SQLite', '3.38.3'),
    ('c-ares', '1.18.1'),
    ('OpenSSL', '1.1', '', SYSTEM),
]
```

How do we figure out what CCR has installed?  It's a manual process of running `module spider` for each dependency. If the dependency isn't installed yet in the CCR software repository, Easybuild will try to build it.  For the dependencies that ARE installed, we must match up the version in CCR's repository so that we're not building a second version for no reason.  Here we find that libxml2 is already installed by CCR, but the version is slightly different.  So we would update the version in the EB recipe to 2.9.10 and then it will use the one CCR has installed.   

```
$ module spider libxml2
----------------------------------------------------------------------------------------------------------------
  libxml2: libxml2/2.9.10
----------------------------------------------------------------------------------------------------------------
    Description:
      Libxml2 is the XML C parser and toolchain developed for the Gnome project (but usable outside of the
      Gnome platform).


    You will need to load all module(s) on any one of the lines below before the "libxml2/2.9.10" module is available to load.

      gcccore/11.2.0
```  

We need to check all the dependencies to ensure we don't run into conflicts.  In the case of `sqlite` CCR has 2 versions installed.  If we look at the version listed in this EB recipe, we see it is actually dependent on a different version of the GCC toolchain so we don't want to use that:  

```
$ module spider sqlite/3.38.3

----------------------------------------------------------------------------------------------------------------
  sqlite: sqlite/3.38.3
----------------------------------------------------------------------------------------------------------------
    Description:
      SQLite: SQL Database Engine in a C Library


    You will need to load all module(s) on any one of the lines below before the "sqlite/3.38.3" module is available to load.

      gcccore/11.3.0
```

Instead, we'll change this dependency to version 3.36 which is installed already and uses GCC 11.2.0.  

!!! Tip "Module spider output"
    Sometimes you'll see modules listed in the `module spider` output that have an `(E)` next to them like: `matlab/1.0.2 (E)`  Do NOT use these versions in your Easybuild recipes.  The `(E)` refers to the module being an extension of another module.  If we used this in our EB recipe then the software we build will also depend on that module.    


Once we've updated any dependency versions, we save the file and use the Easybuild dry run (`-M`) option to see if we've met all the dependencies and if not, which ones with Easybuild try to build for us.  This will also tell us if we have an errors in the recipe file.  

```
$ eb -M aria2-1.36.0-GCCcore-11.2.0  
== Temporary log file in case of crash /tmp/eb-xlnc41x4/easybuild-phg4qbmb.log
== Running parse hook for aria2-1.36.0-GCCcore-11.2.0...
== found valid index for /cvmfs/soft.ccr.buffalo.edu/versions/2023.01/easybuild/software/Core/easybuild/4.8.1/easybuild/easyconfigs, so using it...
== Running parse hook for GCCcore-11.2.0.eb...
== Running parse hook for GCCcore-11.2.0.eb...
== Running parse hook for GCCcore-11.2.0.eb...
ERROR: Failed to process easyconfig /user/djm29/aria2-1.36.0-GCCcore-11.2.0: Failed to determine minimal toolchain for dep CppUnit 1.15.1
```  

This output shows us that one of the dependencies isn't built and Easybuild can't find an existing EB recipe for this package and the `GCCcore-11.2.0` toolchain.  This means, we'll need to build it ourselves, in the same manner as we're trying to build `aria2`.  We'll search for an EB recipe, copy it, and modify for the right toolchain version.  Here are the steps:  

```
$ eb --search cppunit  
== found valid index for /cvmfs/soft.ccr.buffalo.edu/versions/2023.01/easybuild/software/Core/easybuild/4.8.1/easybuild/easyconfigs, so using it..
...
 * /cvmfs/soft.ccr.buffalo.edu/versions/2023.01/easybuild/software/Core/easybuild/4.8.1/easybuild/easyconfigs/c/CppUnit/CppUnit-1.15.1-GCCcore-10.3.0.eb
 * /cvmfs/soft.ccr.buffalo.edu/versions/2023.01/easybuild/software/Core/easybuild/4.8.1/easybuild/easyconfigs/c/CppUnit/CppUnit-1.15.1-GCCcore-11.3.0.eb


$ cp /cvmfs/soft.ccr.buffalo.edu/versions/2023.01/easybuild/software/Core/easybuild/4.8.1/easybuild/easyconfigs/c/CppUnit/CppUnit-1.15.1-GCCcore-11.3.0.eb CppUnit-1.15.1-GCCcore-11.2.0.eb  
```
Open `CppUnit-1.15.1-GCCcore-11.2.0.eb` in your favorite editor, change the toolchain version to 11.2.0 and save the file.

Now use the dry run option to test the Cppunit EB recipe:  

```
$ eb -M CppUnit-1.15.1-GCCcore-11.2.0.eb
== Temporary log file in case of crash /tmp/eb-tgz39qah/easybuild-ufl924e3.log
== Running parse hook for CppUnit-1.15.1-GCCcore-11.2.0.eb...
== found valid index for /cvmfs/soft.ccr.buffalo.edu/versions/2023.01/easybuild/software/Core/easybuild/4.8.1/easybuild/easyconfigs, so using it...
== Running parse hook for GCCcore-11.2.0.eb...
== Running parse hook for GCCcore-11.2.0.eb...
== Running parse hook for GCCcore-11.2.0.eb...

1 out of 10 required modules missing:

* avx512/Compiler/gcccore/11.2.0 | cppunit/1.15.1 (cppunit-1.15.1-GCCcore-11.2.0.eb)

== Temporary log file(s) /tmp/eb-tgz39qah/easybuild-ufl924e3.log* have been removed.
== Temporary directory /tmp/eb-tgz39qah has been removed.
```  
This shows us that there are no missing dependencies and we should be able to install this software successfully.  There's no guarantee, of course, but let's try.  Just remove the `-M` option and start the EB build process.  

```
$ eb CppUnit-1.15.1-GCCcore-11.2.0.eb 
.... 
== COMPLETED: Installation ended successfully (took 5 mins 10 secs)
== Results of the build can be found in the log file(s) 
/projects/academic/[YourGroupName]/easybuild/2023.01/software/avx512/MPI/gcc/11.2.0/cppunit/1.15.1/easybuild/easybuild-Cppunit-1-15-1-20240210.021702.log.bz2

== Build succeeded for 1 out of 1
== Temporary log file(s) /tmp/eb-hjerqc87/easybuild-kjcattow.log* have been removed.
== Temporary directory /tmp/eb-hjerqc87 has been removed.
```  
Now that our dependency `Cppunit` is built, we can attempt to install `aria2`  We recommend another dry run just to make sure we've got everything we need:  

```
$ eb -M aria2-1.36.0-GCCcore-11.2.0.eb
== Temporary log file in case of crash /tmp/eb-2kxod_dt/easybuild-d8jkzen1.log
...

1 out of 10 required modules missing:

* avx512/Compiler/gcccore/11.2.0 | aria2/1.36.0 (aria2-1.36.0-GCCcore-11.2.0.eb)

== Temporary log file(s) /tmp/eb-2kxod_dt/easybuild-d8jkzen1.log* have been removed.
== Temporary directory /tmp/eb-2kxod_dt has been removed.
```
Easybuild is now finding the `Cppunit` dependency is met and nothing else needs to be built so we can move forward with the install.  Remove the dry run option, `-M`, and start the installation.  

!!! Tip "Building Dependencies"  
    Easybuild can build dependencies for us.  If this output of the dry run indiciated additional dependencies were needed, we can add the `--robot` option to the end of this installation command to instruct Easybuild to try to build the dependencies.  Be careful with this though!  You should not be building toolchains, compilers, or major software already installed by CCR like python, java, and other large packages unless you really know what you're doing.  

```
$ eb aria2-1.36.0-GCCcore-11.2.0.eb
== COMPLETED: Installation ended successfully (took 31 mins 29 secs)
== Results of the build can be found in the log file(s)
/cvmfs/soft.ccr.buffalo.edu/versions/2023.01/easybuild/software/avx512/Compiler/gcccore/11.2.0/aria2/1.36.0/easybuil
d/easybuild-aria2-1.36.0-20240215.101436.log.bz2

== Build succeeded for 1 out of 1
== Temporary log file(s) /tmp/eb-_ago41dx/easybuild-8vf4s_8o.log* have been removed.
== Temporary directory /tmp/eb-_ago41dx has been removed.
```

This tells us the installation completed successfully and points us to the zipped log file of the build process.  

!!! Tip "Clean up your temporary files"
    When an Easybuild installation completes successfully, the temporary files created during the installation are removed for us.  If a build fails, Easybuild may not have removed those temporary files so we ask that you do so.  

Now let's search for our module, load it, and look at the module to see where it's installed:  

```
$ module spider aria2
----------------------------------------------------------------------------------------------------------------
  aria2: aria2/1.36.0
----------------------------------------------------------------------------------------------------------------
    Description:
      aria2 is a lightweight multi-protocol & multi-source command-line download utility.


    You will need to load all module(s) on any one of the lines below before the "aria2/1.36.0" module is available to load.

      gcccore/11.2.0

    Help:

      Description
      ===========
      aria2 is a lightweight multi-protocol & multi-source command-line download utility.


      More information
      ================
       - Homepage: https://aria2.github.io

$ module load gcccore/11.2.0 aria2/1.36.0
$ module show aria2/1.36.0
----------------------------------------------------------------------------------------------------------------
   /projects/academic/[YourGroupName]/easybuild/modules/avx512/Compiler/gcccore/11.2.0/aria2/1.36.0.lua:
----------------------------------------------------------------------------------------------------------------
help([[
Description
===========
aria2 is a lightweight multi-protocol & multi-source command-line download utility.


More information
================
 - Homepage: https://aria2.github.io
]])
whatis("Description: aria2 is a lightweight multi-protocol & multi-source command-line download utility.")
whatis("Homepage: https://aria2.github.io")
whatis("URL: https://aria2.github.io")
conflict("aria2")
depends_on("zlib/1.2.11")
depends_on("libxml2/2.9.10")
depends_on("sqlite/3.36")
depends_on("c-ares/1.18.1")
depends_on("openssl/1.1")
prepend_path("CMAKE_PREFIX_PATH","/projects/academic/[YourGroupName]/easybuild/2023.01/software/avx512/Compiler/gcccore/11.2.0/aria2/1.36.0")
prepend_path("CPATH","/projects/academic/[YourGroupName]/easybuild/2023.01/software/avx512/Compiler/gcccore/11.2.0/aria2/1.36.0/include")
prepend_path("LIBRARY_PATH","/projects/academic/[YourGroupName]/easybuild/2023.01/software/avx512/Compiler/gcccore/11.2.0/aria2/1.36.0/lib")
prepend_path("MANPATH","/projects/academic/[YourGroupName]/easybuild/2023.01/software/avx512/Compiler/gcccore/11.2.0/aria2/1.36.0/share/man")
prepend_path("PATH","/projects/academic/[YourGroupName]/easybuild/2023.01/software/avx512/Compiler/gcccore/11.2.0/aria2/1.36.0/bin")
prepend_path("PKG_CONFIG_PATH","/projects/academic/[YourGroupName]/easybuild/2023.01/software/avx512/Compiler/gcccore/11.2.0/aria2/1.36.0/lib/pkgconfig")
prepend_path("XDG_DATA_DIRS","/projects/academic/[YourGroupName]/easybuild/2023.01/software/avx512/Compiler/gcccore/11.2.0/aria2/1.36.0/share")
setenv("EBROOTARIA2","/projects/academic/[YourGroupName]/easybuild/2023.01/software/avx512/Compiler/gcccore/11.2.0/aria2/1.36.0")
setenv("EBVERSIONARIA2","1.36.0")
setenv("EBDEVELARIA2","/projects/academic/[YourGroupName]/easybuild/2023.01/software/avx512/Compiler/gcccore/11.2.0/aria2/1.36.0/easybuild/avx512-Compiler-gcccore-11.2.0-aria2-1.36.0-easybuild-devel")
```
Congratulations!  You've just built some software!!

### Investigating Logs  

Easybuild does a great job logging everything it does.  You just have to spend time reviewing all these logs.  At the start of the installation, Easybuild will give you the location and name of the log for the entire installation.  This is accessible while the installation is running but is removed at completion time.  The log file is zipped up and stored for future reference (see output shown in the example above):

```
== Temporary log file in case of crash /tmp/eb-_ago41dx/easybuild-8vf4s_8o.log
```

And with each step of the installation, you'll get a separate log and working directory, for example:  

```
  >> running command:
        [started at: 2024-02-15 09:45:29]
        [working dir: /var/tmp/[CCRusername]/easybuild/build/aria2/1.36.0/GCCcore-11.2.0/aria2-1.36.0]
        [output logged in /tmp/eb-_ago41dx/easybuild-run_cmd-5y2xgnhf.log]
```  
You can tail these log files during the installation to see how it's progressing and what, if anything, might be going wrong.  The working directory holds alot of details, including config files, make files (if necessary), and whatever other pieces the software needs to install.  This is where you can go to find out what exactly the installation is trying to do.  Each software package is different and you may find answers to why your software didn't build, here in the working directory.  After the EB installation ends successfully, the final log file and working directory contents are removed from their temporary space to the software's final resting place.  The EB installer will output the final location of the log file.  If the installation fails, you can refer to these temporary spaces for clues.  Please make sure to remove these temporary files so as not to waste disk space for others using these compile nodes.  

## Frequently asked questions  

### Failed dep
**Why am I still seeing `failed to determine minimal toolchain for dep`?**  
You've checked all the dependencies for your software and you know that they're already installed with the right versions by CCR (or you did this yourself).  Yet, you're still seeing the error `failed to determine minimal toolchain for dep` when trying to install your software.  Make sure that your EB recipe is formatted correctly.  In the list of dependencies, you must match the name of the dependency with the EB recipe configs exactly.  For example, if your recipe has a dependency for `rust/1.54.0` you will see this is already installed by CCR.  However, the name in the EB recipe must be `Rust` not `rust`.  How can you tell how the name should be spelled?  Look at the Easybuild recipe name for the module and use that spelling.  In this example, the EB recipe for rust is: `Rust-1.54.0-GCCcore-11.2.0.eb`  Also, ensure you're not using a module that is an extension to an existing module in your dependency lists.  [See below](#module-extensions)  

Another reason you might see this is because Easybuild can't find the dependency you've already built.  If you've had to modify an Easybuild recipe to build a dependency, that recipe needs to be in a location where the Easybuild installation can find it.  By default, Easybuild is looking in CCR's configuration directories where our recipes are stored.  It will not look in your directory.  To fix this, specify your directory in the Easybuild installation command using the `--robot=` option.  In the above example for building aria2, we would use this and Easybuild would find the recipe for cppunit that we previously built in our home directory:  
`eb aria2-1.36.0-GCCcore-11.2.0.eb --robot=/user/[CCRusername]`  

### Module extensions
Sometimes you'll see modules listed in the `module spider` output that have an (E) next to them like: `matlab/1.0.2 (E)` Do NOT use these versions in your Easybuild recipes. The (E) refers to the module being an extension of another module. If we used this in our EB recipe then the software we build will also depend on the "parent" module.  

### Install a different software version
**How do I update the version of a software?**  
You have an EB recipe to try to install but you want to update the software version.  This completely depends on the type of software you're installing.  In our example above for `aria2` we can see in the EB recipe that this software is being downloaded from a Github repo.

```
source_urls = ['https://github.com/aria2/aria2/releases/download/release-%(version)s']
sources = [SOURCE_TAR_GZ]
checksums = ['b593b2fd382489909c96c62c6e180054c3332b950be3d73e0cb0d21ea8afb3c5']
```
You can navigate to that repo and see if there are other versions available for download.  If so, download the version you'd like to install, making sure it's the same file format (here we need the `tar.gz` file format or we need to change the `sources=` line in the EB recipe).  [See here](https://docs.easybuild.io/writing-easyconfig-files/#common_easyconfig_param_sources_alt) for more on source formats used by Easybuild.  Now use the Linux `sha256sum` command or an online tool to get the `sha256` checksum for the downloaded file. See more on EB checksums [here](https://docs.easybuild.io/writing-easyconfig-files/#common_easyconfig_param_sources_checksums).  Replace the value in the `checksums` line of the EB recipe with this new value.  Then change the version of the software at the top of the EB recipe with the version you want to install.  Finally, rename the EB recipe to change the software version.  For example, if we wanted to install `aria2` version 1.37.0, the name of our EB recipe would be `aria2-1.37.0-GCCcore-11.2.0.eb`

You will see source locations and checksums are required in [Python bundles](../software/modules.md#python) as well.  These can often be downloaded from [PyPi](https://pypi.org/)  

**What if CCR installed software but I want a different version?**  
In most cases, we will only offer one version of a software package per software release.  If you must use a different version, we recommend you check first to see if CCR has a [modified EB recipe](https://github.com/ubccr/software-layer/tree/main/config/easybuild/easyconfigs) for that software.  If so, it will most likely be easiest for you to copy that and modify it for your needs, rather than starting from the original Easybuild recipe.  

### Finding Easybuild Recipes
**Is there anywhere else I can search for Easybuild recipes?**  
Yes!  Although CCR syncs with the official [Easybuild easyconfigs repo](https://github.com/easybuilders/easybuild-easyconfigs), our repo is not always the most up-to-date.  You can use the Github interface to search easily and if you find a recipe you'd like to try, copy the contents and paste into a file, making sure to name the file correctly.   We also highly recommend using The Digital Research Alliance of Canada (formerly Compute Canada) as a [reference](https://github.com/ComputeCanada/easybuild-easyconfigs/tree/computecanada-main/easybuild/easyconfigs).  If there is no EB recipe you will need to create one using other recipes as examples.   

### Easybuild Help 
**Where can I go for more help?**  
This guide was offered as an example and will not transfer over to each and every software package you try to install.  Unfortunately, compiling and installing software is hard and each package is different from the next.  Easybuild provides a reproducible structure and allows us to build software in a way that ensures it will run efficiently and with the highest performance on the CCR systems.  However, it is not always easy.  We recommend the Easybuild [documentation](https://docs.easybuild.io/) and [tutorials](https://tutorial.easybuild.io/) as the primary sources of information.  It is often difficult for CCR staff to troubleshoot software installations run by others, even if you provide us log files.  We have to go through the process of replicating your steps, at which point, it's often easier for us to just do the installation ourselves.  If there is an existing EB recipe available and we don't already have a version of the package installed, we encourage you to submit a build request following [these instructions](https://docs.ccr.buffalo.edu/en/latest/software/building/#software-build-requests).  If you run into problems while using Easybuild, it's possible we can provide some basic assistance through [CCR Help](../help.md).  However, please note there are limits to the amount of individual help we can provide and you may need to work independently to resolve your issues.  

### Module Not Listed
**Why isn't my module showing up?**  
Your Easybuild installation completes successfully but when you run `module avail` you do not see the software listed.  We have this documented [here](../software/modules.md#hierarchical-modules).  `module spider` should be used to find installed modules across all toolchains.  Unless your software does not depend on a specific toolchain, you must load that toolchain first, before you'll see the module listed using `module avail`  Also, ensure you have the custom module paths setup as described [here](../software/building.md#building-modules-for-your-group).  

**Why isn't a CCR module showing up?**  
CCR has installed hundreds of software packages and not all of them are intended to be loaded and used frequently by users.  They may be packages required just to install other packages or tools that are needed for using other software.  To attempt to keep the module spider output cleaner, we have chosen to hide some modules.  No fear!  You can still use these modules just as any others.  To find these, you can tell the module spider command to show any hidden modules that also exist using this command:  `module --show-hidden spider software_name`  

### Setting permissions on installed software  
Sometimes a software package requires certain unix file permissions in order to launch.  This is usually when the software is a licensed product and the vendor wants to ensure only you can access your installation.  If you see something in the documentation for the software you're installing or you attempt to install it with Easybuild and see an error similar to this:  
```
# IMPORTANT!!  
# Needs to be installed with --umask=007  
```  
you will need to use a flag during the Easybuild installation to ensure the file permissions are set correctly.  In this example, we would use:  
`eb recipe_name.eb --umask=007`  

### Easybuild installation hangs  
Sometimes an Easybuild installation will hang with no obvious errors or the installation logs are not updated with useful information.  Easybuild is configured to run in parallel so there are times when the installation can step on itself or log files are not updated because another process has it locked.  This is rare but if you come across this, one thing you can try is to force the Easybuild installation to run in serial.  Add this option to your EB installation command:  `--parallel=1`  