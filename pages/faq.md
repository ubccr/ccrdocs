# Frequently Asked Questions

## How do I get access?  

CCR's resources are available to research faculty at UB, their students and collaborators, industry customers, and some small classes that require high performance computing for their coursework.  Please see the information on our [Getting Access page](getting-access.md) for detailed information about reporting requirements and any restrictions there may be regarding access.  If you have questions about our access policy or procedures, please contact [CCR Help](help.md)  

## What is my CCR username?

Your CCR username is the same as your UBIT username.  If you do not have a UB account, your CCR username is usually the first letter of your first name plus your last name.  However, if you're unsure, please [contact CCR Help](help.md).

## I have a new phone, how do I update my two factor authentication?  

We highly recommend if you are switching phones, that you add another device to  your CCR account first.  For example, add a tablet or personal computer as an addition device to your account before getting rid of your old phone.  If you have access to both old and new phone, you can add your new phone to your CCR account prior to removing the token from the old phone. Follow the [instructions here](2fa.md#managing-tokens-for-devices) for adding a new device.   If neither of these options is available and you no longer have access to the only device connected to your CCR account, your account is locked out.  Please contact [CCR Help](help.md) to receive instructions for unlocking the account.

## Why can't I login?  

This is a very generic question that is difficult for us to answer.  CCR supports many services.  If you were to ask this question in a help ticket we would respond with: _**What are you trying to login to?  Are you getting any error messages?**_  So we'll provide links here to the primary services CCR users login to and the corresponding documentation:  

- [OnDemand](portals/ood.md#login-to-ccrs-ondemand)  
- [HPC clusters command line SSH or SFTP logins](hpc/login.md)  
- [Lake Effect Research Cloud Horizon Dashboard](cloud/using.md)

_**Common errors:**_  

- **SSH error "no supported authentication methods available":**  SSH keys are required for command line SSH and SFTP access to CCR's login nodes.  Password logins are not accepted.  Please see [more info here](hpc/login.md#connecting-with-ssh)  
-  **SSH error "Permission denied (publickey)":** You either do not have your SSH public key uploaded to your CCR account (see error above) or you are not specifying the private key on your personal device when trying to login to CCR.  See this [page for more info](hpc/login.md#logging-in)  
-  **Missing home directory:**  See [here for more info](#why-am-i-seeing-a-home-directory-missing-error-on-login)  
-  **Password expired:**  Reset your password using the [identity management portal](https://idm.ccr.buffalo.edu).   instructions can be [found here](portals/idm.md#change-your-ccr-password)  
-  **Invalid credentials:**  This means either your password, one time token, or both were entered incorrectly. Please ensure you're using CCR's two factor authentication correctly.  See [here](2fa.md) for instructions as it's different than our UBIT accounts.  If you're sure of this, then we recommend [changing your password](portals/idm.md#change-your-ccr-password).  
-  **Access denied or You don't have access to this resource:**  If receiving this when attempting to login to ColdFront or OnDemand, this means you do not have two factor authentication enabled.  2FA is required.  Follow [these instructions](2fa.md#enabling-two-factor-authentication) to enable it.  
- When trying to login to **OnDemand** you see an error like: **Bad request**, **Server not available** or **Something Bad Happened.  Please contact site admin**:  These are often caused by corrupted cache files in your browser.  Clear your browser cache and cookies data and restart your browser or try a different browser.  Incognito windows often do not solve this problem.     

## How do I verify my account?  

At the time of CCR account creation, an email is sent to the new user asking them to verify their account.  The link contained in the email is only valid for 15 minutes.  If you did not have an opportunity to click the link within 15 minutes and it no longer works, please contact [CCR Help](help.md) for guidance.  Please check your junk or spam folder as sometimes these emails are misclassified by UB email filters.  If you click on the link and see an error like `something bad happened` please clear your browser cache, restart your browser and try the link again.  


## Why is the ColdFront allocation showing active but I can't login?  

Your account has not yet been provisioned.  Our systems sync with ColdFront daily at 5pm, updating accounts and providing access to resources.  This means it can be up to 24 hours after getting added to an allocation before you're able to use it, which includes logging into the HPC environment.  If you were logged into CCR systems at the time of the sync, you may need to log out and back in again to see the changes to your account.

## Why do I get "Fatal system error" or "Account already exists" error when creating a new account?  

When trying to create a new CCR account, you get an error that says "fatal system error" or "account with this username already exists" please contact [CCR help](help.md).  Staff will need to take manual action to rectify the problem.  

## Why am I seeing a home directory missing error on login?  

The first time you login to a CCR server, your home directory will need to be created. When using SSH for login, this is done automatically.  If using OnDemand, follow the instructions provided to initiate the creation of your home directory and SSH key pair for use on the cluster within the OnDemand terminal app. If, after completing the steps, the OnDemand dashboard does not reload, log out and back in again.  

## Can I use something other than a smartphone for two factor authentication?  

Yes!  Though smartphones are the recommended second factor for your CCR account, if you don't have one or don't want to use yours, you can utilize a desktop application (i.e. Authy) or a programmable hardware security key.  There are many on the market including Yubico Yubikeys, Google Titan security keys, and others [recommended by UBIT](https://www.buffalo.edu/ubit/services/duo/options/security-key.html). Please contact [CCR Help](help.md) for details on how to configure your hardware key. **CCR is not able to integrate with the hardware security keys provided by UBIT because they are not programmable and we're unable to get the "secret" needed to join them to our authentication system.**     

## Why do I see a blank window when starting an OnDemand desktop? Why are the desktop icons not working?  

Occasionally, when users try to start an interactive session in OnDemand, the desktop displays as a blank blue or grey window with no applications menu or way to open a terminal window.  Sometimes the desktop will launch but the icons don't work.  Files get cached when sessions are opened and then either get corrupted or can't be used.  To fix this problem, delete the following hidden subdirectories in your home directory and start a new OnDemand desktop session:  

```
rm -rf ~/.vnc  
rm -rf ~/.cache  
rm -rf ~/.config/xfce4  
```

## How can I fix the `XFCE PolicyKit Agent` error in OnDemand desktop sessions?  

If you see an error box that says `XFCE PolicyKit Agent` you can click the `Close` button and proceed with using the OnDemand desktop.  

## Why does my OnDemand desktop or app show it's starting but then it immediately ends?  

Refer to [this OnDemand troubleshooting](howto/ood-trouble.md#why-does-my-ondemand-desktop-or-app-show-its-starting-but-then-it-immediately-ends) info.  

## How can I check how full my directories are?  

CCR's `iquota` tool will provide you quota and usage for your home directory and any shared project or global scratch directories you may also have access to.  You'll first need to authenticate with the `ccrkinit` command.  Enter your password and 6 digit one time token (OTP) when prompted, as shown here:  

```
CCRusername@login:~$ ccrkinit
Enter OTP Token Value:
```
NOTE: You will not see the characters typed when entering your password and OTP.  

```
iquota --path /user/[CCRusername]  
iquota --path /projects/academic/[YourGroupName]  
iquota --path /vscratch/grp-[YourGroupName]  
```

Alternatively, you can view this information on the [ColdFront](https://coldfront.ccr.buffalo.edu) dashboard. More details about storage and quotas can be [found here](hpc/storage.md).

##  Why am I see the error "kinit: Unknown credential cache type while getting default ccache" when using ccrkinit?  

This error is caused by Anaconda conflicting with the Kerberos used by CCR's authentication system.  Some users load Anaconda environments or personal/group Python or Anaconda modules in their `~/.bashrc` file (found in your home directory).  These environments break Kerberos (and also OnDemand desktops and apps!).  To fix this, edit the file and remove everything between the two `>>> conda initialize >>>` lines.  Then save the file, log out of CCR, and log back in again.  Do NOT delete the `~/.bashrc` file!  Anaconda is not recommended for HPC systems and is no longer supported on CCR's systems for [these reasons](software/modules.md#anaconda-python). Please refrain from using this software and if you need help finding an alternative for your workflow, contact [CCR Help](help.md) for recommendations.  

## Why am I getting 'no space left on device' errors?  

If you're sure you're not [over quota](hpc/storage.md) in either file size or number of files, it may be an issue with file permissions.  In the shared project and global scratch directories, users must ensure the group ownership of a file or directory is set to the faculty or project group of that directory.  This is set automatically for new files and when copying files.  However, sometimes users override these defaults.  If you get this error, this is definitely the problem:  
`mv: failed to preserve ownership for 'filename': no space left on device`  

**Other possible reasons for this error:**  
:  **Moving Files:**  If you are trying to move a file from another location, change the group ownership of the file before moving it or use the copy command instead.

:  **Editing or Creating New Files:**  If you get this error when trying to edit an existing file or trying to create a new one, it is because the 'sticky bit' is not set correctly on the subdirectory you are trying to write in.  You must add the sticky bit to the group permissions on the subdirectory to fix this: `chmod g+s directory_name` NOTE: You will NOT have to do this if you do not alter the default permissions within the project or scratch directory.  This is only if you copy over subdirectories that do not have this set or accidentally change the permissions and want to set them back.

:  **Compiling Code:**  It could be that your permissions are correct but the code you're compiling is using your primary unix group when creating new files.  When running `make install` you may see an error like `file INSTALL cannot copy file` or when trying to install a conda package you may see ` An error occurred while installing package 'None'. OSError(28, 'No space left on device'` As a work around, switch to your research group unix group using the command `newgrp group-name` and then proceed with the install.  

## How can I see what the file permissions are?  

The `getfacl` command is an easy way to see the permissions of a file or directory.  It will display the file/directory name, owner of the file/directory, group name that owns the file/directory, and the detailed permissions of the file/directory.  See also: `man getfacl` or `getfacl --help`  

## How can I transfer my files to/from UB Box?

Please see [these instructions](hpc/data-transfer.md##using-globus-to-transfer-files-to-and-from-ub-box) and utilize Globus to transfer files to UB Box. 

## Why am I'm getting module not found errors?  

There are a few types of module errors you might see:  
- `module command not found` means the system doesn't know anything about the software modules.  Ensure the first line of your batch script is: `#!/bin/bash -l`  
- `module not found` means the system can't find the specifc module you're trying to load.  
  - If you're using the faculty cluster, make sure the node you're running on supports the software you want to use.  If you're running on an x86-64-v3 (avx2) CPU, the software may not be built yet.  Submit a [build request](software/building.md#software-build-requests)  
  - You have not loaded the module's dependencies prior to loading the module you want to use.  [See here](software/modules.md#hierarchical-modules) for more info on the hierarchical module scheme  
  - You are trying to load modules from a different software release.  CCR sets a default software release on all systems.  If you want to use a module from a different release than what is the default, you must load the software release version first.  [See here](software/releases.md) for more details.  


## When will my job start?

You can list information on your job’s start time using the squeue command:

`squeue --user=[CCRusername] --start`

Note that Slurm’s estimated start time can be a bit inaccurate. This is because Slurm calculates this estimation off the jobs that are currently running or queued in the system. Any job that is submitted after yours with a higher priority may delay your job.  Alternatively, if jobs complete in less time than they've requested, more jobs can start sooner than anticipated.  

For more information on the `squeue` command, take a look at our [Useful Slurm Commands](hpc/jobs.md#useful-slurm-commands) information or visit the [Slurm page on squeue](https://slurm.schedmd.com/squeue.html)  

## How can I tell what my job's priority is?  

For more information on job priority [see here](hpc/jobs.md#job-priority).  

## Why isn't my job running immediately using a priority boost QOS?

The priority boost is not a ticket to the front of the line (queue).  It is one of multiple factors that go into calculating a job's priority.  Your group's jobs get an additional boost on the QOS portion of the job's fairshare calculation.  For more information on job priority and fairshare calculations [see here](hpc/jobs.md#job-priority).  

## Why is my job pending with reason ‘ReqNodeNotAvail’?  

The `ReqNodeNotAvail` message usually means that your node has been reserved for maintenance during the period you have requested within your job script. This message often occurs in the days leading up to our regularly scheduled maintenance, which is performed the last Tuesday of every month (unless otherwise noted on our [downtime schedule](https://ubccr.freshdesk.com/support/discussions/topics/13000032108)). For example, if you run a job with a 72 hour wall clock request on the last Tuesday of the month, you will see the `ReqNodeNotAvail` status because the node is reserved for maintenance within that 72-hour window. You can confirm whether the requested node has a reservation by typing `scontrol show reservation` to list all active reservations.  

If you receive this message, the following solutions are available:  

1. Submit a job requesting less time so that it does not intersect with the maintenance window

2. Wait until after the maintenance window has finished and your job will resume automatically when there are resources available.   

If this message is not due to an upcoming maintenance downtime, then it means that whatever type of node or feature you requested is not available in the partition you submitted your job to run on. 

## How can I get information on CCR clusters such as how busy they are and wait times?  

From a login node, use the command `sqstat` to see a comprehensive overview of cluster usage.  This information is also displayed on our [cluster status pages](https://www.buffalo.edu/ccr/support/machine-status.html).  To find more detailed information on node availability, use the `snodes` command.  

## Why do I get an ‘Invalid Account, Partition, or QOS Specification’ error when I try to run a job?  

If you're getting errors like these, you're not specifying the right combination of cluster, account, partition, and qos based on what your account has access to:  

```
salloc: error: Job submit/allocate failed: Invalid qos specification
salloc: error: Job submit/allocate failed: Invalid account or account/partition combination specified
sbatch: error: Batch job submission failed: Invalid partition or qos specification
```

CCR uses Quality of Service (QOS) to restrict access to partitions and to provide research groups that support CCR financially with a boost in their job priorities. Slurm will use your default account, unless you specify differently in your job script or when starting an OnDemand app.  Use the `slimits` command to see what accounts and QOS settings you have access to. This is managed in [ColdFront under allocations](portals/coldfront.md).   More details on QOS and partition limits can be [found here](hpc/jobs.md#slurm-directives-partitions-qos).  Information on [becoming a CCR supporter can be found on our website](https://www.buffalo.edu/ccr/support/ccr-help/accounts.html#boost).  


## Why am I getting a QOSMaxSubmitJobPerUserLimit error when I try to submit a job?

You may see this error when submitting batch scripts or when attempting to launch apps in OnDemand:  
```
sbatch: error: QOSMaxSubmitJobPerUserLimit
sbatch: error: Batch job submission failed: Job violates accounting/QOS policy (job submit limit, user's size and/or time limits)
```

You will get this error if you have reached the partition or per user limits as [described here](hpc/jobs.md#slurm-directives-partitions-qos).  For example, if you have 1000 jobs in the general-compute partition and try to submit another one, you will get this error.  If you've already launched one viz desktop, you've reached your limit.  Wait for some of your jobs to finish and submit more at that time.  

## Why am I seeing the job status AssocMaxGRESPerJob on my pending job?  

You may see `AssocMaxGRESPerJob` as a reason your job isn't running.  This means that your job is requesting more GPUs than is allowed for the Slurm account that you've selected your job to run under.  Some accounts (usually those associated with courses) are restricted to using only 1 GPU per job, while other accounts aren't allowed to use any.  The Intro to CCR course has no requirements for GPU use; therefore, the `introccr` Slurm account is blocked from using GPUs.

## Why do I get an "Invalid feature specification?" error  

Compute nodes in the clusters are tagged with Slurm "features" including CPU and GPU types, high speed interconnects (like Infiniband), rack locations, CPU architectures, and more.  You can read more about these features or tags [here](hpc/jobs.md#node-features).  When specifying them either in a Slurm batch script or in the node features field in OnDemand apps, you must ensure that the requests you're making match up with the available compute nodes.  Usually when you see the `invalid feature specification` error, this means the combination of resources you're requesting is not available in the CCR cluster and partition that you're requesting.  Refer to the link above for more information on evaluating what features are available on which compute nodes.  

## How do I login to the compute node my job is running on?  

Please refer to [these instructions](hpc/login.md#compute-node-logins). 

## How do I fix "sbatch: error: Batch script contains DOS line breaks"?

If you receive an error message like this when trying to submit a job, it is because your batch script was edited in a Windows editor, not a unix editor.  Windows editors can add line breaks that the unix interpreter doesn't recognize.  You may receive an error such as:
```
sbatch: error: Batch script contains DOS line breaks (\r\n)
sbatch: error: instead of expected UNIX line breaks (\n).
```
Run the dos2unix command on your file to remove the Windows line breaks.  For example:  `dos2unix myBatchFile`  

Use the 'man' command to see all the options for the dos2unix command:  `man dos2unix`

## How do I fix the error: module command not found?

Please ensure this is the first line of your batch script:

```
#!/bin/bash -l
```

## How do I change my default cluster?  

Do you use the faculty cluster more than the primary and default UB-HPC cluster?  If so, you can change your default cluster so you don't need to specify the cluster name flag when running Slurm commands.  To make the change temporary for your existing login shell, run: `export SLURM_CONF=/util/software/config/slurm/faculty/slurm.conf`  To make this change permanent, add that to your `~/.bashrc` file under the `User specific aliases and functions` section of the file.  

## How do I request all CPUs on a node with more than one GPU?  

You may wish to request a single GPU on a node and all of the node's CPUs.  However, the GPUs are bound to specific CPUs so the job will only run on the CPUs associated with the GPU you're running on.  Specifying the `--exclusive` flag in your job script or requesting all of the node's CPUs will not change this.  If you would like to use all cores on a node with one of the GPUs, you must specify this in  your Slurm script: `#SBATCH --gres-flags=disable-binding`  

Refer to the [Slurm documentation](https://slurm.schedmd.com/gres.conf.html#OPT_Cores) for further information.  

## Why does my application keep getting killed on the login nodes?  

[Login nodes](hpc/clusters.md#login-nodes) have a 15 minute time limit on running processes and are not intended for running applications.  Please submit a [job to the cluster](hpc/jobs.md#running-applications-with-jobs) for running or debugging applications or use a [compile node](hpc/clusters.md#compile-nodes) for installing software.

## Why does my SSH session automatically disconnect?  

SSH connections will time out either due to inactivity or network disruptions.  If your sessions are disconnecting due to inactivity, one thing you can do to keep the SSH connection open is to have ssh send a periodic keep alive packet to the server so it will not timeout.  Add the `-o ServerAliveInterval=600` option to your ssh login command.  SSH can be sensitive to any disruptions in the network which can be common with Wi-Fi networks.  Sometimes the 'keep alive' setting prevents this.  Other times, it may be that you have a setting on your Wi-Fi or ethernet adapter that tells the operating system it can put the device to sleep after a period of inactivity.  This is especially common on Windows.  Check your network adapters for 'Power Settings' and uncheck any options that tell the system it can disable the device to save power.  This will vary by operating system so we recommend you conduct an internet search for the appropriate instructions.  

## Where can I find a list of linux commands?  

There are lots of resources on the internet to learn basic linux commands.  We provide a cheat sheet of useful linux and Slurm commands [here](https://buffalo.box.com/s/nqj3neyt2w1dtb3gix6zxqx5gcc9x30n).  

## How do I know what to request an allocation for?  

Please see [this section of the Getting Access](getting-access.md#available-resources) page for a break down of currently available resources at CCR.

## How can I check what allocations I am on?  

Use [ColdFront](https://coldfront.ccr.buffalo.edu) to view the projects and allocations you have access to. These dictate what resources you have access to as well as what Slurm accounts and shared group directories you may have access to.  More information about ColdFront can be [found here](portals/coldfront.md).  Please note our systems sync with ColdFront daily at 5pm, updating accounts and providing access to resources.  This means it can be up to 24 hours after getting added to an allocation before you're able to use it, which includes logging into the HPC environment.

## How can I turn off notifications in ColdFront?  

Coldfront users are automatically subscribed to receive notifications regarding their project(s) and allocation(s).  These email notifications include things like allocations that are expiring soon and allocation status changes.  Users can turn off these notifications by logging in to [ColdFront](https://coldfront.ccr.buffalo.edu), clicking on your project, and unchecking the check box by your name under the "Enable Notifications" column.  PIs and managers on projects are not able to turn off notifications.  If you're certain you do not want to be reminded of allocation renewals, please [contact CCR Help](help.md) for a manual override.  

## How can I get my class access to CCR?  

CCR **may** be able to accommodate small classes that require small amounts of cycles on the primary UB-HPC cluster.  Please [contact us](help.md) to discuss your course's needs. If you've already discussed with us, you should create a project and request allocations in ColdFront as [detailed here](portals/coldfront.md).  Students need to have created themselves a [CCR system account](getting-access.md) before you can add them to your ColdFront project.

## How can I access my project directory from a Jupyter Notebook?  

Create a symbolic link in your home directory that points to your project directory.  Then you'll be able to navigate through the sym link in the Jupyter Notebook.  To create a symbolic link in your home directory called 'projects' run the `ln -s` command, replacing the full path of your project directory and your username in the example below:  
`ln -s /projects/academic/[YourGroupName] /user/[CCRusername]/projects`

You'll then have the link `/user/[CCRusername]/projects` that takes you to your project directory.  

## Where can I find examples for running on CCR's HPC clusters?  

CCR staff curate a [GitHub repository](https://github.com/ubccr/ccr-examples) of specific examples for running applications on the HPC clusters and installing software using Easybuild.  These examples include basic Slurm batch scripts, specific examples for popular software applications, and examples for building and running containers.  Not every application installed at CCR has an example so these are intended to be modified by users for their specific use case.  This repository is actively developed so we encourage you to visit regularly for new content.

## How do I acknowledge the use of CCR resources?  

Please acknowledge resources provided by CCR in publications as follows:  

**Support provided by the Center for Computational Research at the University at Buffalo [1].**

and cite as (using the appropriate citation format):  

[1] Center for Computational Research, University at Buffalo, http://hdl.handle.net/10477/79221.  
