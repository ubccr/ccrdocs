# Building your own software

## Software Repository

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

[EasyBuild](https://easybuild.io/) is a software build and installation framework that allows us to
manage (scientific) software on High Performance Computing (HPC) systems in an
efficient way.

Easyconfig files are used to specify which software to build, which version of
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

- [What is EasyBuild?](https://docs.easybuild.io/en/latest/Introduction.html)
- [EasyBuild Documentation](https://docs.easybuild.io/en/latest/)
- [EasyConfig library](https://github.com/easybuilders/easybuild-easyconfigs)

CCR staff are working on building up our center's software repository using
these Easyconfigs.
