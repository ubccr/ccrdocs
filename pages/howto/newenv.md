# Introducing "CCR Future"  

CCR staff have been working for over a year to provide users with an updated environment that includes a new software infrastructure, new compute nodes, and a new operating system.  Additionally, a new core network switch and updated networking protocols have been put into production.  This combination of projects is what we're referring to as the "CCR Future" environment.  Each of these separate projects has been a monumental task and we've tried to orchestrate these updates while keeping the existing infrastructure in place so you can continue to conduct your research.  However, this is akin to changing the tires on your car while moving at 100 MPH!  It is not easy and it will not work perfectly for everyone.  The information on this page aims to provide more details about the current transition environment - "CCR Future" - so that your research group can transition over a period of weeks and be prepared for the decommissioning of the old modules and compute nodes at the end of the Fall 2023 semester.  

Whether you're a long time CCR user or brand new to our center, we hope to smooth out the process of onboarding to the "CCR Future" environment.  Please note this is an overview document specific to the transition period and users should refer to the wealth of information in the rest of our documentation website for all the details of using CCR's resources.  

**We highly recommend you start by watching this presentation on CCR's new software modules and how to utilize the "CCR Future" environment:**  

![type:video](https://youtube.com/embed/k1fymCTeI0k)   


## Office Hours

Beginning August 31, 2023 CCR staff will host weekly office hours from 11am-12pm on Thursdays to provide support to users switching over to the "CCR Future" environment.  Please join us and bring your questions!  

```
https://buffalo.zoom.us/j/94613848883?pwd=Q2ZjU3VIaWZDZGZPdldjR1JwOUVmZz09 
Meeting ID: 946 1384 8883 
Passcode: 497161 
```
NOTE:  You must authenticate to Zoom prior to joining the meeting

## New Users 

Users new to CCR after August 8, 2023 will automatically be put into the "CCR Future" environment.  This means you don't need to do anything other than follow the directions [below](#the-new-resources) to access the new compute nodes and new OnDemand service.  If you are a member of a research group that owns their own nodes, you may not want to be in the new environment yet.  You may want to go back to the old environment so you can use your group's nodes until they are transitioned to the new environment.  [See here](#faculty-cluster-transition) for guidance. 

!!! Note "ATTN: Faculty Cluster Users"  
    The faculty cluster nodes have not been transitioned into the "CCR Future" environment yet.  We will complete the transition of UB-HPC nodes first, install the newly purchased faculty nodes in the new environment next, and then transition the existing faculty cluster partitions last.  We will contact the owners of nodes in the faculty cluster as we prepare to schedule this transition.  If you do not have many nodes in your partition, you may wish to switch to the "CCR Future" environment now to make use of [CCR's new compute nodes](#the-new-ccr-future-resources) in the UB-HPC cluster.  If want to continue to use your nodes, we provide [recommendations below](#faculty-cluster-transition) for how to work in both environments so you can begin migrating your software and workflows.  

## Existing Users - How to Transition 

- Use the new login server or OnDemand 3.0 portal as described [below](#the-new-ccr-future-resources)  - OR - Create a blank file in your home directory named `.ccr_new_modules` Then log out & back in again to `vortex.ccr.buffalo.edu`  
- Ensure that nothing has been added to the `.bashrc` file in your home directory.  Command aliases are usually fine; however, comment out or remove anything else not provided by CCR.  This is what your `.bashrc` file should look like:  
```
# .bashrc

# Source global definitions
if [ -f /etc/bashrc ]; then
        . /etc/bashrc
fi


if [ -f /etc/bash.bashrc ]; then
    . /etc/bash.bashrc
fi

# Uncomment the following line if you don't like systemctl's auto-paging feature:
# export SYSTEMD_PAGER=

# User specific aliases and functions
# enable color support of ls and also add handy aliases
if [ -x /usr/bin/dircolors ]; then
    test -r ~/.dircolors && eval "$(dircolors -b ~/.dircolors)" || eval "$(dircolors -b)"
    alias ls='ls --color=auto'

    alias grep='grep --color=auto'
    alias fgrep='fgrep --color=auto'
    alias egrep='egrep --color=auto'
fi

```
- Follow the directions [below](#the-new-ccr-future-resources) to access the new resources    
- If you have existing software modules you or your group have built, they will likely need to be re-built for this environment.  See [here](#old-software-modules-installed-by-your-research-group) for more information    


## The New "CCR Future" Resources  

!!! Warning "REMINDER!!!"  
    Do NOT add anything to the `.bashrc` file in your home directory!  Loading modules, enabling conda environments, and other environment-related tasks will almost certainly break your environment on the CCR systems.  It will break CCR's quota tool, cause OnDemand desktops & apps to fail to start, and cause problems with batch scripts on compute nodes.  

**New Login Server**  
We provide two types of login nodes to span the old and the new "CCR Future" environments.  You can login to `vortex-future.ccr.buffalo.edu` and you're, by default, in the "CCR Future" environment.  The login process sources the new environment files and sets up certain things automatically. From vortex-future, you can submit jobs to the reservation of new compute nodes (see below) and you can use commands like `salloc` for interactive jobs on the new nodes.  You can not load software modules (installed in /util) from the old environment on vortex-future.    

You can also access the "CCR Future" environment from `vortex.ccr.buffalo.edu`.  However, you must have a blank file in your home directory named `.ccr_new_modules` so that the login process knows to source the right environment files for the "CCR Future" environment (this is what vortex-future does automatically).  You can submit batch scripts through either the vortex or vortex-future login nodes for compute nodes in either environment.  However, because of the special environment settings on vortex-future, you can only use `salloc` commands to request interactive jobs on the new nodes.  If you want to request interactive jobs on the old nodes this needs to be done from vortex.

**There are some differences to the login nodes so we recommend if you want to use the "CCR Future" environment exclusively you use `vortex-future.ccr.buffalo.edu` as that is setup specifically for this new environment and will be the standard going forward.**  


**New OnDemand Portal**  
To access the new compute nodes and new software via OnDemand, we have installed [OnDemand 3.0](https://ondemand-future.ccr.buffalo.edu).  There are many new features to take advantage of, as well as changes to how we've laid out the apps.  Please [see here](../howto/ondemand.md) for more details.  You will ONLY have access to compute nodes that have been moved to the "CCR Future" environment and ONLY have access to the new software modules.  Faculty cluster nodes will not be available in OnDemand 3.0 until they've been migrated into the new environment. See more on the faculty cluster transition [here](#faculty-cluster-transition).   

The new server URL is:  [https://ondemand-future.ccr.buffalo.edu](https://ondemand-future.ccr.buffalo.edu)


**Newest Compute Nodes**  
The UB-HPC cluster spans both the old and new ("CCR Future") environments.  The nodes in the old environment are running an old version of CentOS 7 and have access to the old software modules (installed in /util) and the new software modules (available in /cvmfs).  Newly purchased compute nodes have been put into the "CCR Future" environment and users can access them using a reservation.  More compute nodes are being migrated into this reservation each week.  To access the reserved compute nodes, specify the following in your batch scripts:  

```
#SBATCH --cluster=ub-hpc
#SBATCH --partition=general-compute
#SBATCH --qos=general-compute
#SBATCH --reservation=ubhpc-future
```

**Using `salloc`?** If you use `salloc` for interactive jobs, you must specify the reservation in your salloc command and run an additional command after being allocated a node.  For example:  

```
salloc --reservation=ubhpc-future --qos=general-compute --partition=general-compute  --job-name "MyJob" --nodes=1 --ntasks=1 --mem=8G --time=00:30:00  

srun --pty /bin/bash --login
```

**Older Compute Nodes**  
The compute nodes currently in the UB-HPC cluster are being reinstalled and placed in the "CCR Future" environment rack by rack every week.  We're starting with the newest equipment and working our way to the oldest of nodes.  By the end of this semester, the only nodes left in the UB-HPC cluster will be 9 year old HP nodes with AVX CPUs.  We are not building software modules for these very old compute nodes.  They will be decommissioned during the December downtime.  As more nodes move to the "CCR Future" environment, wait times will increase on the remaining nodes of the UB-HPC cluster.  By the end of the semester, all UB-HPC cluster users will need to be on the "CCR Future" environment and the ubhpc-future reservation will be removed.  The "CCR Future" environment will then be the default for all UB-HPC cluster users and the old software in /util will not be accessible.  


!!! Tip "Module command errors"  
    Users submitting jobs to older avx2 architecture-based nodes in the faculty cluster may run into issues with the login node environment persisting into the job environment.  This may present with the error `module command not found`.  Please contact [CCR Help](../help.md) for guidance.  The error `module not found` means the module is not available for the architecture of the node you're running on.  CCR's software modules are architecture dependent and most modules have not been built for the oldest nodes in the UB-HPC cluster with AVX CPUs.  There are some nodes in the faculty cluster with AVX2 CPUs.  If you need to run on these nodes, use the `compile-avx2` [compile server](../software/building.md#building-your-own-software) for building your software or specifically request the AVX2 install from CCR. 
  


## Faculty Cluster Transition  

Compute nodes in the faculty cluster will be transitioned rack by rack after the UB-HPC transition is complete.  CCR staff will reach out to the PIs that own the nodes to share more detailed scheduling as we get closer to those dates.  In most cases, we need to coordinate with multiple research groups per rack so we appreciate your patience as we work through these logistics.  For PIs that have purchased new compute nodes, they will be installed in the "CCR Future" environment.  If you have an existing partition, the new nodes will be put in a reservation and will be accessed like the reservation in the UB-HPC cluster.  For PIs that do not yet have a partition, you will need to be using the "CCR Future" environment to access your nodes once they are in production.

**How can faculty cluster users manage this transition period?**  

There are several options for faculty cluster users during the next few months:  

1. You can continue using your cluster partition and the old nodes in the UB-HPC cluster, using the vortex login node and OnDemand.  Ensure you do not have the `.ccr_new_modules` file in your home directory.  BEWARE: the old software modules are being removed from service at the end of this semester and the UB-HPC cluster will be completely in the "CCR Future" environment by then.  You should only choose this option if you install your own software in your project directory.  

2. If you have only a few nodes in your faculty cluster partition and would rather use the new compute nodes in the UB-HPC cluster, you can make the switch now and use the vortex-future login node and/or OnDemand-future exclusively with the new compute nodes in the ubhpc-future reservation ([see above](#the-new-ccr-future-resources)).  When your partition of nodes is migrated to the "CCR Future" environment you can begin using them again.  

3. You can try straddling both environments.  This may be confusing but this will allow you time to migrate your workflows and install any software modules your group needs, while continuing to run calculations with the old software.  To do this, ensure you do not have the `.ccr_new_modules` file in your home directory and use the vortex login node or OnDemand portal for your old workflow and jobs.  Login to vortex-future (which automatically sets up the "CCR Future" environment when you login) or OnDemand-future for your new software installations and to utilize the new compute nodes in the UB-HPC cluster.  **We do want to caution you on this option:**  All environments use the same home directory and many software packages save temporary or cached files here.  Attempting to span both these environments may cause conflicts, depending on what software you use.  We have provided guidance for a suggested naming scheme that aligns with our new software environment for those using [python virtual environments](../howto/python.md) or [Anaconda environments](../howto/conda.md).  This guidance MAY help alleviate overwriting of these specific software environments.  Straddling both the environments will involve some manipulation on your part and your mileage may vary. Good luck!



## Software Modules

### New Software Modules  
In January this year, CCR released a new suite of software modules for use on the HPC clusters. The new software modules include more recent versions of your favorite compiler toolchains, libraries, and software programs. CCR staff continue to work daily to add more software packages to the module list.   If you don't see the software you need, follow the [instructions here](#software-installation-requests) to request new software builds. You can also install your own software by following this [guidance](../software/building.md).

This new software module infrastructure is quite an upgrade to what CCR has offered over the last 20 years and we're excited to make it available to all of our users.  However, we realize this migration will not be painless nor transparent.  We commit to providing as much assistance as we can to users and research groups by providing detailed documentation, training sessions, and CCR Help office hours offered over Zoom.  We highly recommend [viewing this presentation](https://youtu.be/k1fymCTeI0k?si=-n88dZREDOppFoYI) on using the new software modules and building your own software.  Though we're still using LMOD like in the old software environment, there are lots of new options we're using and methods we're using for building software that this presentation covers.  

### Old Software Modules Installed by your Research Group  
Any modules previously created in the old environment will need to be reinstalled into the new module system.  We know, this isn't what you wanted to hear.  We feel your pain.  We're currently trying to reconstruct 20+ years of software installations ourselves.  The reason behind this isn't so much a new version of modules but it's more about the operating system, compilers, and linking used to install your old software.  It is unlikely that software installed years ago will work in the new operating system using newer compilers.  As part of the software infrastructure, CCR provides a compatiblity layer.  Installing software using this will allow these packages to work on any Linux-based operating system, no longer tying us (or you) to a specific flavor of Linux.  This is especially coming in handy with all the turmoil over RedHat derivatives we've seen lately.  This is future-proofing us and will allow for the testing of cutting edge operating systems in the future, which has been asked of us by researchers over the years.  If your software did not require building (using compilers) or linking to the system libraries (for example: python scripts), it MAY be POSSIBLE to convert them over to the new module directory structure so they are available to you.  At that point, you can test to see if the software works on compute nodes in the "CCR Future" environment.  This is not something CCR can provide support for; however, if you'd like to try it, you'd need your module(s) to be in the directory structure [defined here](../software/building.md#building-modules-for-your-group) (see specifically the tip in green).  

### What if we installed our own software without modules?  

If you installed your own software without using modules, it is possible it might work.  However, it's the same basic concept as in the above paragraph.  With a new operating system, updated compilers, and the fact that your software was linked against old libraries, it is unlikely to work on the newly installed compute nodes and it definitely won't be optimized for the new CPUs.  You are absolutely welcome to try it though and we'll keep our fingers crossed for you that it does!  If your code can make use of different CPU architectures, you will want to optimize it by compiling it in CCR's new environment.

### Software Installation Requests  

CCR is accepting requests for software installations and encourages users to "like" any requests they see for software they want to use in [this list](https://github.com/ubccr/software-layer/issues).  This helps us to rank the requests and prioritize the order they are installed.  [Follow these instructions](../software/building.md#software-build-requests) to request a software build.  Currently, we have the staffing capacity only to install software available in the [EasyBuild recipe catalog](https://github.com/easybuilders/easybuild-easyconfigs/tree/develop/easybuild/easyconfigs). We can provide advice and troubleshooting assistance for groups needing to install outside of this environment via [CCR help tickets](../help.md). 

Join us for [office hours](#office-hours) on Thursdays at 11am if you've got questions about the "CCR Future" environment or need help with building software.  


## Frequently asked Questions  

This transition is complicated and we know even after reading all the above information you may be confused.  Here are a few questions we've received recently:  

**Why is there a reservation?**  
We need to keep the new nodes separate from the old nodes because if a user submits a job to the new nodes without having migrated to the new software modules, the job will fail, not having access to the old software modules.


**Why aren't the new nodes available in the scavenger partition?**  
The nodes in the ubhpc-future reservation have been reinstalled with a new operating system and are in a new network.  During this transition period they can't be part of the scavenger partition, because as we mentioned above, we can't have jobs running on the same nodes in the old and new environment.  As more nodes are brought over to the "CCR Future" environment, we'll reach critical mass and the scavenger partition will be switched over for those using the "CCR Future" environment and no longer available to request in the old environment. 


**How can I continue to use the old software modules?**  
If you'd like to remain in the old environment, remove the `~/.ccr_new_modules` file and log out and back into `vortex.ccr.buffalo.edu`  You should NOT use `vortex-future` or `ondemand-future` as both these services are only in the "CCR Future" environment.  You should also not use the `ubhpc-future` reservation to submit jobs as the nodes in that reservation are in the "CCR Future" environment and won't work with old modules.  _**Just a reminder, these old modules will be removed from service at the end of the Fall 2023 semester.**_


**What if I want to use my partition in the faculty cluster AND the "CCR Future" environment?**  
See option 3 in [this section](#faculty-cluster-transition) for guidance.  May the force be with you!  


**How can I tell what resources are available in the ubhpc-future reservation?**  
Because we've got old and new environments in the same cluster it is difficult, at this time, to tell what's available. This will be remedied when all nodes in the UB-HPC cluster have been migrated to the "CCR Future" environment in the coming weeks. A couple of useful commands for finding out information about the nodes and jobs in the reservation include:

```
sinfo --reservation ubhpc-future
squeue --reservation ubhpc-future
snodes all ub-hpc/general-compute|grep FUTURE
```
NOTE: Sometimes you'll see nodes tagged with `FUTURE` but they're not yet available to run on.  This is part of the migration from the old environment to the new.  Thanks for your patience!  


**Where are my new nodes?**  
Many faculty members purchased new nodes during the large purchase facilitated by CCR earlier this year.  We know you're anxious to get access to your new compute nodes!  Unfortunately, we have been waiting on the arrival of racks for the compute nodes and can not install the equipment until they arrive.  Though these were ordered even before our compute nodes were, we're finding these delays common these days.  It took 14 months for a core network switch to arrive last year and we're not expecting InfiniBand cables purchased in May to arrive until December.  We're doing our best to work around these delays and we will get the faculty cluster nodes installed as soon as the racks arrive.  Thank you so much for your patience!  