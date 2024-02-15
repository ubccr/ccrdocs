# An Easybuild Example  

We recommend CCR users utilize the Easybuild framework when installing software.  This tool ensures that the compilation and linking that happens during a software installation is done correctly and will work with our systems.  We do not offer instruction on using Easybuild.  However, there is excellent [documentation](https://docs.easybuild.io/) and [tutorials](https://tutorial.easybuild.io/) provided by Easybuild developers.  

## Easybuild Background  

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

As a reminder, these are the [toolchains](../software/releases.md) CCR supports.  You must use one of these when installing software using Easybuild.  If you try a recipe for an unsupported toolchain, Easybuild will attempt to install that toolchain for you.  You don't want this as it will take up too much disk space, take very long to build, and is highly likely that installation will fail. 

**When using Easybuild, do NOT use the CCR login nodes.**  Always use a [compile node](../software/building.md) or do this from a compute node in an [OnDemand desktop](../portals/ood.md#desktop-interactive-apps) session or [interactive job](../hpc/jobs.md#interactive-job-submission).  These installations can use a decent amount of disk space so we recommend you use your project directory for all software installations.  We do not recommend using your home directory as these have small quotas.  If you haven't already done so, create an `easybuild` directory in your group's project directory and set the [Easybuild build prefix](../software/building.md#building-modules-for-your-group) to that directory.  Reminder: this is just an example; you'll need to set the path name to your group's shared project directory, which may not be in `/projects/academic`      

```
~ $ ssh compile  
~ $ mkdir /projects/academic/groupname/easybuild   
~ $ export CCR_BUILD_PREFIX=/projects/academic/groupname/easybuild  
```
!!! Tip "Set Easybuild install path"  
    The `CCR_BUILD_PREFIX` needs to be set each time you install software.  You're telling Easybuild where to put this particular installation.  [More details](../software/building.md#building-modules-for-your-group)   


## Example Easybuild Installation  

For this example, we're going to step through the process of building a software package called `aria2`  

First, we load the Easybuild module and search for an existing Easybuild (EB) recipe (**Reminder: don't do this on a login node!**):

```
~ $ module load easybuild  
~ $ eb -S aria2
== found valid index for /cvmfs/soft.ccr.buffalo.edu/versions/2023.01/easybuild/software/Core/easybuild/4.8.1/easybuild/easyconfigs, so using it...
CFGS1=/cvmfs/soft.ccr.buffalo.edu/versions/2023.01/easybuild/software/Core/easybuild/4.8.1/easybuild/easyconfigs
 * $CFGS1/a/aria2/aria2-1.35.0-GCCcore-10.3.0.eb
 * $CFGS1/a/aria2/aria2-1.36.0-GCCcore-11.3.0.eb
```  

This output shows us that there are 2 existing EB recipes for `aria2` but neither of them are for a supported toolchain.  CCR provides GCC 11.2.0 so you could try either one of these options.  However, in our experience, we've found it's best to try a toolchain in the same major version as one we have installed (as in GCCcore-11.x.x instead of 10.x.x or 12.x.x).  The recipe in the same major version will have dependency versions closest to what is already installed at CCR.  If we had to choose between a recipe for `foss-2021a` or `foss-2022b`, we'd go with `2021a` as it will more closely match the `foss/2021b` that CCR has installed.  If you pick something much older or newer, the less luck you'll have with your software getting installed properly.  Again, this is just our experience, YMMV (your mileage may vary).  

To attempt to install this, we must make a copy of the existing EB recipe and modify it.  The output above shows us where the EB recipe files are stored (`CFGS1=...`) so we can easily copy to our home directory.  **NOTE: You must change the name of the EB recipe when you copy it, updating the toolchain version.**  

Here we update the name of the EB recipe from `aria2-1.36.0-GCCcore-11.3.0.eb` to `aria2-1.36.0-GCCcore-11.2.0.eb`  If you were to also change the version of the software package you're attempting to install, you need to change that in the EB recipe file name as well.  In this example, we're not doing that.  

```
~ $ cp /cvmfs/soft.ccr.buffalo.edu/versions/2023.01/easybuild/software/Core/easybuild/4.8.1/easybuild/easyconfigs/a/aria2/aria2-1.36.0-GCCcore-11.3.0.eb aria2-1.36.0-GCCcore-11.2.0.eb
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

The first thing to change is the toolchain line - change from `11.3.0` to `11.2.0` because this is the version of GCCcore that CCR has installed:  
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
~ $ module spider libxml2
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
~ $ module spider sqlite/3.38.3

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


Once we've updated any dependency versions, we save the file and use the Easybuild dry run (-M) option to see if we've met all the dependencies and if not, which ones with Easybuild try to build for us.  This will also tell us if we have an errors in the recipe file.  

```
~ $ eb -M aria2-1.36.0-GCCcore-11.2.0  
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
~ $ eb -S cppunit  
== found valid index for /cvmfs/soft.ccr.buffalo.edu/versions/2023.01/easybuild/software/Core/easybuild/4.8.1/easybuild/easyconfigs, so using it...
CFGS1=/cvmfs/soft.ccr.buffalo.edu/versions/2023.01/easybuild/software/Core/easybuild/4.8.1/easybuild/easyconfigs
...
 * $CFGS1/c/CppUnit/CppUnit-1.15.1-GCCcore-10.3.0.eb
 * $CFGS1/c/CppUnit/CppUnit-1.15.1-GCCcore-11.3.0.eb

~ $ cp /cvmfs/soft.ccr.buffalo.edu/versions/2023.01/easybuild/software/Core/easybuild/4.8.1/easybuild/easyconfigs/c/CppUnit/CppUnit-1.15.1-GCCcore-11.3.0.eb CppUnit-1.15.1-GCCcore-11.2.0.eb  

vi CppUnit-1.15.1-GCCcore-11.2.0.eb  
# change the toolchain version to 11.2.0 and save the file  
```

Now use the dry run option to test the Cppunit EB recipe:  

```
~ $ eb -M CppUnit-1.15.1-GCCcore-11.2.0.eb
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
This shows us that there are no missing dependencies and we should be able to install this software successfully.  There's no guarantee, of course, but let's try.  Just remove the -M option and start the EB build process.  

```
~ $ eb CppUnit-1.15.1-GCCcore-11.2.0.eb 
.... 
== COMPLETED: Installation ended successfully (took 5 mins 10 secs)
== Results of the build can be found in the log file(s) 
/projects/academic/groupname/easybuild/2023.01/software/avx512/MPI/gcc/11.2.0/cppunit/1.15.1/easybuild/easybuild-Cppunit-1-15-1-20240210.021702.log.bz2

== Build succeeded for 1 out of 1
== Temporary log file(s) /tmp/eb-hjerqc87/easybuild-kjcattow.log* have been removed.
== Temporary directory /tmp/eb-hjerqc87 has been removed.
```  
Now that our dependency `Cppunit` is built, we can attempt to install `aria2`  We recommend another dry run just to make sure we've got everything we need:  

```
~ $ eb -M aria2-1.36.0-GCCcore-11.2.0.eb
== Temporary log file in case of crash /tmp/eb-2kxod_dt/easybuild-d8jkzen1.log
...

1 out of 10 required modules missing:

* avx512/Compiler/gcccore/11.2.0 | aria2/1.36.0 (aria2-1.36.0-GCCcore-11.2.0.eb)

== Temporary log file(s) /tmp/eb-2kxod_dt/easybuild-d8jkzen1.log* have been removed.
== Temporary directory /tmp/eb-2kxod_dt has been removed.
```
Easybuild is now finding the `Cppunit` dependency is met and nothing else needs to be built so we can move forward with the install.  Remove the dry run option, -M, and start the installation.  

!!! Tip "Building Dependencies"  
    Easybuild can build dependencies for us.  If this output of the dry run indiciated additional dependencies were needed, we can add the `--robot` option to the end of this installation command to instruct Easybuild to try to build the dependencies.  Be careful with this though!  You should not be building toolchains, compilers, or major software already installed by CCR like python, java, and other large packages unless you really know what you're doing.  

```
~ $ eb aria2-1.36.0-GCCcore-11.2.0.eb
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
~ $ module spider aria2
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

~ $ module load gcccore/11.2.0 aria2/1.36.0
~ $ module show aria2/1.36.0
----------------------------------------------------------------------------------------------------------------
   /cvmfs/soft.ccr.buffalo.edu/versions/2023.01/easybuild/modules/avx512/Compiler/gcccore/11.2.0/aria2/1.36.0.lua:
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
prepend_path("CMAKE_PREFIX_PATH","/projects/academic/groupname/easybuild/2023.01/software/avx512/Compiler/gcccore/11.2.0/aria2/1.36.0")
prepend_path("CPATH","/projects/academic/groupname/easybuild/2023.01/software/avx512/Compiler/gcccore/11.2.0/aria2/1.36.0/include")
prepend_path("LIBRARY_PATH","/projects/academic/groupname/easybuild/2023.01/software/avx512/Compiler/gcccore/11.2.0/aria2/1.36.0/lib")
prepend_path("MANPATH","/projects/academic/groupname/easybuild/2023.01/software/avx512/Compiler/gcccore/11.2.0/aria2/1.36.0/share/man")
prepend_path("PATH","/projects/academic/groupname/easybuild/2023.01/software/avx512/Compiler/gcccore/11.2.0/aria2/1.36.0/bin")
prepend_path("PKG_CONFIG_PATH","/projects/academic/groupname/easybuild/2023.01/software/avx512/Compiler/gcccore/11.2.0/aria2/1.36.0/lib/pkgconfig")
prepend_path("XDG_DATA_DIRS","/projects/academic/groupname/easybuild/2023.01/software/avx512/Compiler/gcccore/11.2.0/aria2/1.36.0/share")
setenv("EBROOTARIA2","/projects/academic/groupname/easybuild/2023.01/software/avx512/Compiler/gcccore/11.2.0/aria2/1.36.0")
setenv("EBVERSIONARIA2","1.36.0")
setenv("EBDEVELARIA2","/projects/academic/groupname/easybuild/2023.01/software/avx512/Compiler/gcccore/11.2.0/aria2/1.36.0/easybuild/avx512-Compiler-gcccore-11.2.0-aria2-1.36.0-easybuild-devel")
```
Congratulations!  You've just built some software!!

## Investigating Logs  

Easybuild does a great job logging everything it does.  You just have to spend time reviewing all these logs.  At the start of the installation, Easybuild will give you the location and name of the log for the entire installation.  This is accessible while the installation is running but is removed at completion time.  The log file is zipped up and stored for future reference (see output shown in the example above):

```
== Temporary log file in case of crash /tmp/eb-_ago41dx/easybuild-8vf4s_8o.log
```

And with each step of the installation, you'll get a separate log and working directory, for example:  

```
  >> running command:
        [started at: 2024-02-15 09:45:29]
        [working dir: /var/tmp/ccruser/easybuild/build/aria2/1.36.0/GCCcore-11.2.0/aria2-1.36.0]
        [output logged in /tmp/eb-_ago41dx/easybuild-run_cmd-5y2xgnhf.log]
```  
You can tail these log files during the installation to see how it's progressing and what, if anything, might be going wrong.  The working directory holds alot of details, including config files, make files (if necessary), and whatever other pieces the software needs to install.  This is where you can go to find out what exactly the installation is trying to do.  Each software package is different and you may find answers to why your software didn't build, here in the working directory.  After the EB installation ends successfully, the final log file and working directory contents are removed from their temporary space to the software's final resting place.  The EB installer will output the final location of the log file.  If the installation fails, you can refer to these temporary spaces for clues.  Please make sure to remove these temporary files so as not to waste disk space for others using these compile nodes.  

## Frequently asked questions  

**Why am I still seeing `failed to determine minimal toolchain for dep`?**  
You've checked all the dependencies for your software and you know that they're already installed with the right versions by CCR (or you did this yourself).  Yet, you're still seeing the error `failed to determine minimal toolchain for dep` when trying to install your software.  Make sure that your EB recipe is formatted correctly.  In the list of dependencies, you must match the name of the dependency with the EB recipe configs exactly.  For example, if your recipe has a dependency for `rust/1.54.0` you will see this is already installed by CCR.  However, the name in the EB recipe must be `Rust` not `rust`

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
In most cases, we will only offer one version of a software package per software release.  If you must use a different version, we recommend you check first to see if CCR has a modified EB recipe for that software.  If so, it will most likely be easiest for you to copy that and modify it for your needs, rather than starting from the Easybuild recipe.  


**Is there anywhere else I can search for Easybuild recipes?**  
Yes!  Although CCR syncs with the official [Easybuild easyconfigs repo](https://github.com/easybuilders/easybuild-easyconfigs), it is not always the most up-to-date.  You can use the Github interface to search easily and if you find a recipe you'd like to try, copy the contents and paste into a file, making sure to name the file correctly.   We also highly recommend using The Digital Research Alliance of Canada (formerly Compute Canada) as a [reference](https://github.com/ComputeCanada/easybuild-easyconfigs/tree/computecanada-main/easybuild/easyconfigs).  

**Where can I go for more help?**  
This guide was offered as an example and will not transfer over to each and every software package you try to install.  Unfortunately, compiling and installing software is hard and each package is different from the next.  Easybuild provides a reproducible structure and allows us to build software in a way that allows it to run efficiently and with the highest performance on the CCR systems.  However, it is not always easy.  We recommend the Easybuild documentation and tutorials referenced at the top of this document as the primary sources of information.  It is often difficult for CCR staff to troubleshoot software installations run by others, even if you provide us log files.  We have to go through the process of replicating your steps, at which point, it's often easier for us to just do the installation ourselves.  If there is an existing EB recipe available and we don't already have a version of the package installed, we encourage you to submit a build request following [these instructions](https://docs.ccr.buffalo.edu/en/latest/software/building/#software-build-requests).  If there is no EB recipe or we've already installed the package and you just want a different version, it's possible we can provide assistance through [CCR Help](../help.md).  However, please note there are limits to the amount of help we can provide and you may need to work independently to resolve your issues.  
