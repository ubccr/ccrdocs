# Software Installation Policy  

CCR staff install and maintain software packages that are standard for high performance computing environments. These include toolchains, compilers, programming language environments, and several engineering applications which are organized in CCR’s [standard software environments](../software/releases.md#what-are-ccr-software-environments).  The list of CCR’s currently supported toolchains and CPU microarchitectures can be found [here](../software/releases.md). 

CCR supports thousands of users that specialize in very different fields of expertise, each using different types of software applications. There are a large number of possible ways to install those applications (versions, dependencies, options, etc) and they range from mature, well developed software to cutting edge, bug-prone packages.  Software security and regular maintenance of installed applications are crucial to keeping CCR’s software repository stable and usable.  This complicated combination of competing interests is why the core set of software officially supported by CCR must remain small.  
 

## What can be installed in CCR’s HPC environment? 

Minimum requirements for software to work in the CCR HPC environment: 

 - Must run under modern Linux operating systems 
 - Must be properly licensed for your use (see [here](#licensed-software) for more info) 
 - Must work on the [CPU microarchitectures](../software/march.md) currently supported by CCR 
 - Applications must be supported and actively maintained with security releases (at a minimum) by the developer 

 
!!! Warning "GUI Applications"
    HPC systems are not ideal environments for graphical user interface (GUI) applications.  While GUI applications may run on the HPC clusters, rendering performance is often poor. Before buying software licenses and spending a lot of time doing a complicated software install, check the requirements for the software and contact [CCR staff](../help.md) to verify that it is a good candidate for use in CCR's HPC environment.

 
## Installing Software Applications 

### User Installations  

**Most software should be installed in a research group's project directory, a user's home directory, or used within a container environment whenever possible.**  Software installation methods vary from simple to complex.  At a minimum, you may need to configure your installation to use a non-standard installation directory.  Users will not be able to install operating system packages on CCR systems.  Alternative instructions for installing from source or using a container for your software should be utilized in these cases.  If your software requires compiling from source or using a build system, it is recommended that you utilize the Easybuild software framework to ensure the installation works correctly in the CCR HPC environment or use the software within a container environment.  More information on using Easybuild for installing your own software can be found [here](../software/building.md) and a how-to install with Easybuild is [here](../howto/easybuild.md). CCR’s container documentation can be found [here](../howto/containerization.md).  Our current staffing levels don't allow for individualized software installations, but we can often help users to do this themselves.  Please contact [CCR Help](../help.md) for assistance with software installations and for basic troubleshooting support. 
 
### Requesting the Installation of Software  

To request the installation of a software application into a CCR software environment, please submit an issue in [CCR's GitHub software repository](https://github.com/ubccr/software-layer/issues).  Your software must meet the **[minimum requirements listed above](#what-can-be-installed-in-ccrs-hpc-environment)** to be evaluated.  Applications not meeting those requirements are not eligible to be installed in CCR’s software repository and such requests will be rejected.  

CCR staff will consider installing software that meets the following **minimum criteria**: 

 - Must potentially benefit multiple research groups and not negatively impact other users on the system 
 - Software must be supported and actively maintained with security releases (at a minimum) by the developer  
 - Must be free to use in an academic environment through an open source or free license (see [here](#licensed-software) for more info on licensed software) 
 - Must be compatible with CCR's [current standard software environment](../software/releases.md), including the ability to modify the installation directory.  
 - Custom environments or distribution of files or packages on every compute node can’t be supported. 
 - Websites, databases, or applications that rely on perpetual services being active are not supported.
 - Does not rely on a graphical user interface (GUI) 

When submitting a [GitHub issue](https://github.com/ubccr/software-layer/issues) to request an installation, you'll be asked to fill out a form and provide information about your research group and the software you'd like to use.  Once evaluated by CCR staff, you will receive a decision about whether we can **attempt** the installation.  If we agree to attempt it, you will be asked to provide an example of how to run the software with any necessary input files so CCR staff can test the application once it’s installed.  You may share these in `/vscratch/ccr-help/[CCRUsername]`   

### Things to be aware of  

 - Some installations are straight-forward and can be done within a matter of days; others can be quite time-consuming.  
 - Two weeks' notice is recommended for any software installation request, though this time frame could be extended depending on how many dependent packages are required for installation.  If you require software to meet a deadline, please ensure your request is submitted with plenty of lead time.   
 - It’s important to note that not all software will install successfully or will work in CCR’s HPC environment, despite our valiant efforts.  Sometimes software is written for workstations and does not function correctly in a shared environment.  Some software is not written with clusters in mind and expects to be installed into system directories which can’t be modified.  Some applications need a custom environment on every compute node.  Some software installations take days of effort and still do not work right.   
 - Previous successful installations of software applications do not guarantee we can successfully install newer versions of those applications. 


###  Licensed Software  
**Software that requires a license cannot be installed in CCR’s software repository.** These packages must be installed in your research group's project directory. **It’s important to note that even if the license is free, if the software requires registration and/or accepting a license agreement, this must be done by the faculty member leading the research group and can’t be done by CCR staff.**   

CCR’s HPC environment can only support floating licenses, not node-locked licenses.  If you’re unsure what that means, please contact [CCR Help](../help.md) prior to purchasing a license from the vendor. If your license is not already supported by another IT department at UB, please contact CCR Help prior to purchasing your software.  Supporting a license server is a fee-based service provided by CCR and will require a payment be made prior to gaining access.

### Commercial Software Packages 

It may be possible to install some commercial software applications in CCR’s HPC environment.  Please contact [CCR Help](../help.md) for more information.  Each application is unique and will be evaluated on a case-by-case basis. 


## Software Security 

CCR staff go to great lengths to secure the HPC environment on many fronts.  Software vulnerabilities will be a never-ending battle we all wage to protect the systems and your research from harm.  Though software applications running on CCR’s systems are being executed in an unprivileged manner, this does not leave the systems or your data completely free from risk.  To help protect your work, and that of all other CCR users, keep these security practices in mind when evaluating and writing software: 

 - Test software on your personal computer prior to using it on CCR’s systems. 
 - Know where your software is coming from and who is contributing to it.  Many open-source and closed-source projects have hundreds of dependencies that could be affected by supply chain vulnerabilities. 
 - Know where your input data is coming from and who has been able to modify it. This is often referred to as Scientific Phishing. 
 - Perform ‘defensive programming’ and sanitize/validate all inputs. 
 - Utilize validation tests and continuous integration in order to write robust research software. 

!!! Danger "Notify CCR of Security Updates"
    If you’ve requested the installation of software by CCR staff and are aware of a security patch or update for that application, please contact [CCR Help](../help.md) immediately.  If software is found to have a security vulnerability, CCR may limit access to the application or issue a patch, depending on the severity of the vulnerability. 


## Acceptable Use Policy 

Software used to encourage or increase discriminatory or harassing behavior that violates the [University at Buffalo's policies on acceptable use](https://www.buffalo.edu/administrative-services/policy1/ub-policy-lib/computer-network-use.html) or [CCR’s acceptable use policy](misuse.md) will be rejected. Software requests that violate the security or integrity of CCR resources or the University at Buffalo will be denied. 

 

 