# Building your own software

CCR maintains a global suite of software available to all users via
[Modules](about.md). If you need a particular software package or library
that's not available you can [ask us to build it](#software-build-requests) or
attempt to [build yourself](#building-your-own-modules).  This document
provides some pointers on building custom modules for your group or personal
use. 

## Software build requests

Users can request software be installed by CCR staff by submitting a new [issue
on GitHub here](https://github.com/ubccr/software-layer/issues/new). Please
provide the name of the software or library you're interested and any specific
details such as the URL where the software can be found. We also encourage you
to [search the issues here](https://github.com/ubccr/software-layer/issues) to
see if another user has already submitted a request. Users are strongly
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

EasyBuild recipes, called easyconfigs, are text files (python syntax) used
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
for a compiler CCR already supports.

For more information about EasyBuild [see here](https://docs.easybuild.io/en/latest/).


## Building your own modules

We recommend using [EasyBuild](#about-easybuild) to build your own modules.
EasyBuild will take care of compiling, installing, and creating a Modulefile
for you. CCR provides EasyBuild as it's own module and has pre-configured
EasyBuild with the appropriate settings for CCR's environment. 



specify which software to build, which version of
the software (and its dependencies), which build parameters to use (e.g., which
compiler toolchain to use), etc.  Think of them like a recipe that lists out
what is needed to create a meal.  What ingredients are required and what is
optional?  What order should the ingredients be added?  What are the steps to
preparing the meal?  Are there any special instructions we need to know for how
to properly prepare the dish?  The Easyconfig files list out all of this info
for installing a software application and then when you run the script to
install, the recipe is followed.  These "recipes" are provided by the community
of EasyBuild users and are fully unit tested and vetted.  The EasyBuild
installations allow for parallel builds, reproducibility of previous builds,
extensive logging and error reporting (nothing is THAT easy!), automated
installations, and dependency resolution, among other things.


CCR provides a repository of software using the file system called CERN Virtual
Machine File System (CVMFS).  CCR's CVMFS is mounted as
`/cvmfs/soft.ccr.buffalo.edu` on all CCR front end login servers and compute
nodes. You can even mount this on your own desktop or laptop, if you want! More
on that [here](). Compute Canada provides a great overview of CVMFS
[here](https://docs.alliancecan.ca/wiki/CVMFS) CernVM-FS website and
documentation can be found [here](https://cernvm.cern.ch/fs/)

## Compatibility Layer

The compatibility layer of the CCR software project uses [Gentoo
Prefix](https://wiki.gentoo.org/wiki/Project:Prefix) to provide a known base on
top of the host.  This is the foundation we use to build our software stack on.
Using the Gentoo Prefix allows us to install compilers and other system
packages in a non-standard location which helps avoid conflicts between
systems.  It will no longer matter what base operating system CCR runs on our
nodes or front end servers compared to your own machine as you can use our
combability layer to level the playing field.  Consider us operating system
agnostic going forward!  For those of you interested in system level testing,
we encourage you to check out all the [docs on this prefix
setup](https://wiki.gentoo.org/wiki/Project:Prefix).  However, the majority of
CCR users will probably not care one bit nor notice any difference.

## EasyBuild Software Installation

