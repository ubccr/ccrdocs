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
