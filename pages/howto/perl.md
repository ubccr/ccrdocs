## Perl Module Installation  

CCR provides the base Perl software.  Perl is available in the compatibility layer and also as a software module.  Run `perl --version` to see the compatibility layer version.  Use the `module spider perl` command to see what is available as modules and then use the `module load some_module` command to load your preferred version.  **NOTE: The `module spider` command will indicate if additional modules are required to be loaded prior to loading the software module.**  Once loaded you'll be able to install additional packages or libraries in your local environment - either in your home or project directory.  

!!! Tip  
    Perl uses the term "modules" to indicate libraries or packages to install into your Perl environment.  These are different than Python modules and the Lmod software modules CCR users to enable software environments.


### Specifying Alternate Install Location 

You can store Perl modules in your home directory or use a subdirectory in your project space to share with your entire group.  Because the home directory quotas are small, we recommend using your project directory.  

NOTE:  In this example, `yourgroup` refers to the name of your group's project directory.  Most shared project directories will be found in `/projects/academic` (which we use in this example) but some are in `/projects/industry` or `/projects/academic/courses`  We recommend using [this nomenclature](about.md) that specifies the CCR software version; however, it's not required.    

```  
[ccruser@vortex ~]$ module spider perl
[ccruser@vortex ~]$ module load gcccore/11.2.0 perl

[ccruser@vortex ~]$ wget -O- http://cpanmin.us | perl - -l /projects/academic/yourgroup/$USER/software/$CCR_VERSION/perl5 App::cpanminus local::lib  

```  
The above command does the following:  

`wget -O- http://cpanmin.us` fetches the latest version of `cpanm` and prints it to STDOUT which is then piped to `perl - -l $PROJDIR/.perl5 App::cpanminus local::lib`. The first tells `perl` to expect the program to come in on STDIN, this makes `perl` run the version of `cpanm` we just downloaded. perl passes the rest of the arguments to `cpanm`. The `-l $PROJDIR/.perl5` argument tells `cpanm` where to install `perl` modules, and the other two arguments are two modules to install. `App::cpanmins` is the package that installs `cpanm`. `local::lib` is a helper module that manages the environment variables needed to run modules in a local directory.  

Next we'll issue a few commands to update our `~/.bashrc` file to point perl to our preferred installation directory in the future:    

```
echo `eval $(perl -I /projects/academic/yourgroup/$USER/software/$CCR_VERSION/perl5/lib/perl5 -Mlocal::lib=/projects/academic/yourgroup/$USER/software/$CCR_VERSION/perl5)' >> .bashrc  
echo 'export MANPATH=/projects/academic/yourgroup/$USER/software/$CCR_VERSION/perl5/man:$MANPATH' >> .bashrc  
```

**The above setup steps are only run one time.  Once this setup is in place, all Perl module installations will be directed to the local directory you've specified.**


!!! Note "Restart Required"  
    Before installing any Perl modules you will need to restart your shell (log out and back in again) or run `source ~/.bashrc` for these new settings to take effect.  


### Installing Perl Modules  

Perl packages can now be installed using the `cpanm Module::Name` command. For example, run the following command to install Log4perl and then verify it's in your preferred installation directory:  

```
[ccruser@vortex ~]$ cpanm Log::Log4perl
--> Working on Log::Log4perl
Fetching http://www.cpan.org/authors/id/E/ET/ETJ/Log-Log4perl-1.57.tar.gz ... OK
Configuring Log-Log4perl-1.57 ... OK
Building and testing Log-Log4perl-1.57 ... OK
Successfully installed Log-Log4perl-1.57 (upgraded from 1.54)
1 distribution installed
[ccruser@vortex ~]$ ls -al /projects/academic/yourgroup/$USER/software/$CCR_VERSION/perl5/lib/perl5/Log  
drwxr-sr-x 2 ccruser ccruser   4096 Jun  7 12:53 Log4perl
-r--r--r-- 1 ccruser ccruser 104246 Oct 21  2022 Log4perl.pm

```

### References  

[Perl Documentation](https://perldoc.perl.org/)  
[CPAN Documentation](https://www.cpan.org/)  


!!! Warning "Support Availability"  
    CCR supports the base installation of Perl.  Any modules you install outside of this environment are not supported.  We recommend using resources available on the internet for assistance with any issues you may run into.   