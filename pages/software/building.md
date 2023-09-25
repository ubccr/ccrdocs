# Building your own software

CCR maintains a global suite of software available to all users via
[Modules](modules.md). If you need a particular software package or library
that's not available you can [ask us to build it](#software-build-requests) or
attempt to [build yourself](#building-a-new-software-module).  This document
provides some pointers on building custom modules for your group or personal
use. 

!!! Warning "You must build software on compile nodes"
    You will not be able to compile software on the login nodes. You must first
    ssh into a compile node before building software. After logging in to the
    login node, simply run `ssh compile`.  There are some nodes in the faculty cluster with AVX2 CPUs.  If you need to run on these nodes, use the `compile-avx2` compile server for building your software. 

## Software build requests

Users can request software be installed by CCR staff by submitting a new [issue
on GitHub here](https://github.com/ubccr/software-layer/issues/new). Please
provide the name of the software or library you're interested in and any specific
details such as the URL where the software can be found. We also encourage you
to [search the issues here](https://github.com/ubccr/software-layer/issues?q=is%3Aissue+is%3Aopen+label%3Abuild-request) 
to see if another user has already submitted a request. Users are strongly
encourage to vote on which software is to be installed by adding a "like" or
"thumbs up" on the issue. Due to limited staffing we'll be installing more
popular software requests first so it's important you vote.

## About EasyBuild

CCR uses [EasyBuild](https://easybuild.io/) for building software. EasyBuild is
a software build and installation framework that helps manage software on High
Performance Computing (HPC) systems in an efficient and reproducible way.

EasyBuild is written in python and uses simple human readable build recipes.
EasyBuild provides a vast repository of build recipes for all kinds of software
shared with the greater HPC community. There's a good chance that the software
you're looking for already has an EasyBuild recipe.

EasyBuild recipes, called easyconfigs, are text files (python syntax) used to
instruct EasyBuild how to build software. You can browse the community
supported [recipes here](https://github.com/easybuilders/easybuild-easyconfigs/tree/develop/easybuild/easyconfigs).

The standard EasyBuild recipe filename format is:

```
<software name>-<version>-<compiler>-<compiler version>.eb

Example:

  SAMtools-1.16.1-GCC-11.2.0.eb

   Software Name: SAMtools
         Version: 1.16.1
        Compiler: GCC
Compiler Version: 11.2.0
```

When building software with EasyBuild, it's very important to pay attention to
the compiler and compiler version as it will be much easier to build software
for [a compiler CCR already supports](releases.md).

For more information about EasyBuild [see here](https://docs.easybuild.io/en/latest/).

EasyBuild will take care of compiling, installing, and creating a Modulefile
for you. CCR provides EasyBuild as it's own module and has pre-configured
EasyBuild with the appropriate settings for CCR's environment. To load CCR's
easybuild module simply run this:

```
$ module load easybuild
```

!!! Note 
    Compiling certain software will be CPU architecture specific. Runing `echo
    $CCR_ARCH` will show you what CPU architecture you're currently running on.
    If you need to build for a specific architecture, you can request a
    specific compile node by running `ssh compile-avx512` or `ssh compile-avx2`.

## Building a new software module

If you can't find the software you're looking for from the [available software](modules.md) 
provided by CCR, you can attempt to build it yourself. You can use easybuild to
search for recipes to build. For example:

```
$ module load easybuild
$ eb -S some_package_name

# For example
$ eb -S samtools
 * $CFGS1/s/SAMtools/SAMtools-1.13-GCC-10.3.0.eb
 * $CFGS1/s/SAMtools/SAMtools-1.13-GCC-11.3.0.eb
 * $CFGS1/s/SAMtools/SAMtools-1.14-GCC-11.2.0.eb
 * $CFGS1/s/SAMtools/SAMtools-1.15-GCC-11.2.0.eb
 * $CFGS1/s/SAMtools/SAMtools-1.15.1-GCC-11.2.0.eb
 * $CFGS1/s/SAMtools/SAMtools-1.16.1-GCC-11.2.0.eb
```

Select the recipe, be sure to select the one [for a supported compiler
toolchain](releases.md) if necessary and build the software by running the
following command:

```
# Check what are the dependencies
$ eb SAMtools-X.X.X-GCC-Y.Y.Y.eb -M

# Build the the software and all the dependencies at once
$ eb SAMtools-X.X.X-GCC-Y.Y.Y.eb --robot

# Build only the software (no deps)
$ eb SAMtools-X.X.X-GCC-Y.Y.Y.eb

```

Once the above command is complete you should see your new module when you run
`module avail` under the `Your Modules` section:

```
$ module avail
----- Your personal Compiler-dependent avx512 modules ---------
   samtools/X.X.X (bio)
```

For an excellent tutorial on how to build software with easybuild [see here](https://easybuilders.github.io/easybuild-tutorial/).

## Building modules for your group

By default, easybuild modules are stored in `$HOME/.local/easybuild/$CCR_VERSION`. 
This should be fine for small software libraries and personal use. However, the
downsides are your group members will not be able to see your modules and you can
easily fill up your home directory quota.  To build software modules in your
projects space, simply set the `CCR_BUILD_PREFIX` env variable to your desired
location [before running easybuild](#building-a-new-software-module). For example:

```
$ module load easybuild
$ export CCR_BUILD_PREFIX=/projects/academic/grp-ccrstaff/easybuild
# verify the install path. Note CCR_VERSION will always be appended to the path
$ eb --show-config | grep installpath
installpath             (E) = /projects/academic/grp-ccrstaff/easybuild/2023.01
```

To ensure your new custom modules show up in `module avail`, you can set the
`CCR_CUSTOM_BUILD_PATHS` env variable. Note: this only has to be done once. 

```
# Also set the env variable so new modules get picked up in the menu
$ export CCR_CUSTOM_BUILD_PATHS=$CCR_BUILD_PREFIX

# To ensure this path gets picked up on login
$ mkdir -p $HOME/.ccr
$ echo $CCR_CUSTOM_BUILD_PATHS > ~/.ccr/modulepaths
```

!!! Tip "Multiple custom module paths"
    You can set multiple custom module paths in this file `~/.ccr/modulepaths`.
    Paths are colon `:` separated. For example:
    `/projects/path1:/projects/path2`. It's expected that each path has
    sub-directories `CCR_VERSION/modules` which contain module files for the
    specific CCR_VERISON.
