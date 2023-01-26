# Frequently Asked Questions

## How do I get access?  

CCR's resources are available to research faculty at UB, their students and collaborators, industry customers, and some small classes that require high performance computing for their coursework.  Please see the information on our [Getting Access page](getting-access.md) for detailed information about reporting requirements and any restrictions there may be regarding access.  If you have questions about our access policy or procedures, please contact [CCR Help](help.md)  

## What is my CCR username?

Your CCR username is the same as your UBIT username.  If you do not have a UB account, your CCR username is usually the first letter of your first name plus your last name.  However, if you're unsure, please [contact CCR Help](help.md).

## I have a new phone, how do I update my two factor authentication?  

We highly recommend if you are switching phones, that you add another device to  your CCR account first.  For example, add a tablet or personal computer as an addition device to your account before getting rid of your old phone.  If you have access to both old and new phone, you can add your new phone to your CCR account prior to removing the token from the old phone. Follow the [instructions here](/2fa/#managing-tokens-for-devices) for adding a new device.   If neither of these options is available and you no longer have access to the only device connected to your CCR account, your account is locked out.  Please contact [CCR Help](help.md) to receive instructions for unlocking the account.

## Why can't I login?  

This is a very generic question that is difficult for us to answer.  CCR supports many services.  If you were to ask this question in a help ticket we would respond with: _**What are you trying to login to?  Are you getting any error messages?**_  So we'll provide links here to the primary services CCR users login to and the corresponding documentation:  

- [OnDemand](/portals/ood/#login-to-ccrs-ondemand)  
- [HPC clusters command line SSH or SFTP logins](/hpc/login)  
- [Lake Effect Research Cloud Horizon Dashboard](/cloud/using)

_**Common errors:**_  

- **SSH error "no supported authentication methods available":**  SSH keys are required for command line SSH and SFTP access to CCR's login nodes.  Password logins are not accepted.  Please see [more info here](/hpc/login/#connecting-with-ssh)  
-  **SSH error "Permission denied (publickey)":** You either do not have your SSH public key uploaded to your CCR account (see error above) or you are not specifying the private key on your personal device when trying to login to CCR.  See this [page for more info](/hpc/login/#logging-in)  
-  **Missing home directory:**  Your account hasn't been provisioned yet.  See [here for more info](#why-am-i-seeing-a-home-directory-missing-error-on-login)  
-  **Password expired:**  Reset your password using the [identity management portal](https://idm.ccr.buffalo.edu).   instructions can be [found here](/portals/idm/#change-your-ccr-password)  
-  **Invalid credentials:**  This means either your password, one time token, or both were entered incorrectly.   
-  **Access denied or You don't have access to this resource:**  If receiving this when attempting to login to ColdFront or OnDemand, this means you do not have two factor authentication enabled.  2FA is required.  Follow [these instructions](/2fa/#enabling-two-factor-authentication) to enable it.    

## Why am I seeing a 'Home directory missing' error on login?  

This usually means your account has not yet been provisioned.  After you create your CCR account, you must be added to an active allocation that gives you access to CCR's resources.  Once this is done, your account gets provisioned with the appropriate access and a home directory, if you're a new user.  This account provisioning happens at the end of every business day so you may not be able to login immediately after getting added to an allocation.  If it's been several business days since you've been added but you're still seeing this message, please [contact CCR Help](help.md).  For more information on access and allocations, please [see here](/getting-access/#allocation-requests).  

## Why is the ColdFront allocation showing active but I can't login?  

This is the same reason as [this](#why-am-i-seeing-a-home-directory-missing-error-on-login) - your account has not yet been provisioned.  

## Why do I get "Fatal system error" or "Account already exists" error when creating a new account?  

When trying to create a new CCR account, you get an error that says "fatal system error" or "account with this username already exists" please contact [CCR help](help.md).  Staff will need to take manual action to rectify the problem.  

## Why can I login to the help portal but not my CCR account?  

The Freshdesk help desk portal accounts are separate from our CCR system accounts.  This allows people who do not yet have a CCR account to request help from CCR staff.  For more info on CCR accounts, see our [Getting Access](getting-access.md) page.  For more info on the help desk portal, [see here](help.md).  

## Can I use something other than a smartphone for two factor authentication?  

Yes!  Though smartphones are the recommended second factor for your CCR account, if you don't have one or done want to use yours, you can utilized a desktop application (i.e. Authy) or a programmable hardware security key.  There are many on the market including Yubico Yubikeys, Google Titan security keys, and others [recommended by UBIT](https://www.buffalo.edu/ubit/services/duo/options/security-key.html).  **CCR is not able to integrate with the hardware security keys provided by UBIT because they are not programmable and we're unable to get the "secret" needed to join them to our authentication system.** Please contact [CCR Help](help.md) for details on how to configure your hardware key.    

## How can I check how full my directories are?  

CCR's `iquota` tool will provide you quota and usage for your home directory and any shared project or global scratch directories you may also have access to.  You'll first need to authenticate with the `ccrkinit` command.  Enter your password and 6 digit one time token (OTP) when prompted, as shown here:  

```
[ccruser@vortex:~]$ ccrkinit
Enter OTP Token Value:
```
NOTE: You will not see the characters typed when entering your password and OTP.  

```
iquota --path /user/username
iquota --path /projects/academic/groupname
iquota --path /panasas/scratch/grp-groupname
```

Alternatively, you can view this information on the [ColdFront](https://coldfront.ccr.buffalo.edu) dashboard. More details about storage and quotas can be [found here](/hpc/storage).

##  Why am I see the error "kinit: Unknown credential cache type while getting default ccache" when using ccrkinit?  

This error is caused by Anaconda conflicting with the Kerberos used by CCR's authentication system.  Some users load Anaconda environments or personal/group Python or Anaconda modules in their `.bashrc` file (found in your home directory).  These environments break Kerberos (and also OnDemand desktops and apps!) so we do not recommend loading them in the .bashrc file.   

## How can I transfer my files to/from UB Box?

Please see the [recommended instructions from UBIT here](/hpc/data-transfer/#transferring-files-with-ub-box)  

## When will my job start?

You can list information on your job’s start time using the squeue command:

`squeue --user=your-username --start`

Note that Slurm’s estimated start time can be a bit inaccurate. This is because Slurm calculates this estimation off the jobs that are currently running or queued in the system. Any job that is submitted after yours with a higher priority may delay your job.  Alternatively, if jobs complete in less time than they've requested, more jobs can start sooner than anticipated.  

For more information on the `squeue` command, take a look at our [Useful Slurm Commands](hpc/jobs/#useful-slurm-commands) information or visit the [Slurm page on squeue](https://slurm.schedmd.com/squeue.html)  

## How can I tell what my job's priority is?  

You can check to see what your job's priority is compared to others in the queue, using the `sprio` command:    
```
sprio -j jobid  
sprio -u username
```  

To list jobs in the queue based on priority from highest to lowest, use the `sranks` command  

## Why is my job pending with reason ‘ReqNodeNotAvail’?  

The `ReqNodeNotAvail` message usually means that your node has been reserved for maintenance during the period you have requested within your job script. This message often occurs in the days leading up to our regularly scheduled maintenance, which is performed the last Tuesday of every month (unless otherwise noted on our [downtime schedule](https://ubccr.freshdesk.com/support/discussions/topics/13000032108)). For example, if you run a job with a 72 hour wall clock request on the last Tuesday of the month, you will see the `ReqNodeNotAvail` status because the node is reserved for maintenance within that 72-hour window. You can confirm whether the requested node has a reservation by typing `scontrol show reservation` to list all active reservations.  

If you receive this message, the following solutions are available:  

1. Submit a job requesting less time so that it does not intersect with the maintenance window

2. Wait until after the maintenance window has finished and your job will resume automatically when there are resources available.   

## How can I get information on CCR clusters such as how busy they are and wait times?  

From a login node, use the command `sqstat` to see a comprehensive overview of cluster usage.  This information is also displayed on our [cluster status pages](https://www.buffalo.edu/ccr/support/machine-status.html).  To find more detailed information on node availability, use the `snodes` command.  

## Why do I get an ‘Invalid Account, Partition, or QOS Specification’ error when I try to run a job?  

If you're getting errors like these, you're not specifying the right combination of cluster, account, partition, and qos based on what your account has access to:  

```
salloc: error: Job submit/allocate failed: Invalid qos specification
salloc: error: Job submit/allocate failed: Invalid account or account/partition combination specified
sbatch: error: Batch job submission failed: Invalid partition or qos specification
```

CCR uses Quality of Service (QOS) to restrict access to partitions and to provide research groups that support CCR financially with a boost in their job priorities. Slurm will use your default account, unless you specify differently in your job script or when starting an OnDemand app.  Use the `slimits` command to see what accounts and QOS settings you have access to. This is managed in [ColdFront under allocations](/portals/coldfront.md).   More details on QOS and partition limits can be [found here](hpc/jobs/#slurm-directives-partitions-qos).  Information on [becoming a CCR supporter can be found on our website](https://www.buffalo.edu/ccr/support/ccr-help/accounts.html#boost).  

## Why am I getting a QOSMaxSubmitJobPerUserLimit error when I try to submit a job?

You may see this error when submitting batch scripts or when attempting to launch apps in OnDemand:  
```
sbatch: error: QOSMaxSubmitJobPerUserLimit
sbatch: error: Batch job submission failed: Job violates accounting/QOS policy (job submit limit, user's size and/or time limits)
```

You will get this error if you have reached the partition or per user limits as [described here](/hpc/jobs/#slurm-directives-partitions-qos).  For example, if you have 1000 jobs in the general-compute partition and try to submit another one, you will get this error.  If you've already launched one viz desktop, you've reached your limit.  Wait for some of your jobs to finish and submit more at that time.  

## Why isn't my job running immediately using a priority boost QOS?

The priority boost is not a ticket to the front of the line (queue).  It is one of multiple factors that go into calculating a job's priority.  Your group's jobs get an additional boost on the QOS portion of the job's fairshare calculation.

## How do I know what to request an allocation for?  

Please see [this section of the Getting Access](/getting-access/#available-resources) page for a break down of currently available resources at CCR.

## How can I check what allocations I am on?  

Use [ColdFront](https://coldfront.ccr.buffalo.edu) to view the projects and allocations you have access to. These dictate what resources you have access to as well as what Slurm accounts and shared group directories you may have access to.  More information about ColdFront can be [found here](/portals/coldfront.md)  

## How can I turn off notifications in ColdFront?  



## How do I acknowledge the use of CCR resources?  

Please acknowledge resources provided by CCR in publications as follows:  

**Support provided by the Center for Computational Research at the University at Buffalo [1].**

and cite as (using the appropriate citation format):  

[1] Center for Computational Research, University at Buffalo, http://hdl.handle.net/10477/79221.  
