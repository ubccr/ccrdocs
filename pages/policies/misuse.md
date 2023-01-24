# System Usage Policies  

Here we define policies for the proper use of CCR systems.  This is not an exhaustive list, by any means, however, it covers critical points of interest to users such as shared system usage, scratch usage, and the batch scheduler policy.  

## Permitted Usage

The University at Buffalo's Center for Computational Research maintains servers, clusters, and websites designed for UB's faculty and staff researchers, their students and external collaborators, and industry customers.  All users of CCR systems are required to comply with ALL of the University at Buffalo's Information Technology Policies as well as all CCR policies both explicitly stated here as well as implicitly.  In other words, just because you CAN do something, doesn't mean you SHOULD do it.  

!!! Tip "CCR enforces UBIT Policies"  
    Please refer to the [University at Buffalo's Computer and Network Use Policy](http://www.buffalo.edu/administrative-services/policy1/ub-policy-lib/computer-network-use.html) as the University's policies applies to all CCR resources as well.  


Every time you login to a CCR server via SSH, you are presented with a login banner which states the CCR Computing and Network Use Policy (CNUP), detailed here: https://buffalo.edu/ccr/support/policies.html  

This login banner is also viewable on the OnDemand dashboard.  However, even if it is not explicitly displayed, any CCR server, website, or other resource you login to managed by CCR requires your acknowledgement and agreement to comply with this policy.  

==If you do not agree with the CCR CNUP, you are required to log off immediately==


## Misuse of Systems and Abuse of Account

We reserve the right to disable any account, without prior notice, that is causing problems internally, externally or violating the University at Buffalo’s information technology policies, CCR policies, and/or the laws of New York State or the United States of America.  Users committing such offenses may be reported to the University at Buffalo's IT security officer or the local authorities.

!!! Warning "Do NOT Share Accounts!"
    UB nor CCR accounts are NOT TO BE SHARED with anyone.  There is no reason whatsoever to share your password, authentication credentials or SSH keys with anyone.  Doing so will result in your CCR account being deactivated and your actions being reported to the University at Buffalo's IT security office  

**Did you know?**  
CCR offers project storage space for groups to securely share data and can work with your group to support this collaboration.  Do NOT share your account with anyone.

**Attempts to circumvent policies**  

**Fairshare system for batch job scheduling:**  
The clusters' batch queuing system is designed to give everyone a fair shot at the highest level of throughput for their jobs.  Attempting to circumvent the queue or fairshare system (i.e. cut to the front of the line) is strictly prohibited and will result in your account being deactivated and potential disciplinary action by the University at Buffalo IT security office. See below for more information on this policy.  

**Scratch Scrubber Policy**  
CCR provides free, high throughput scratch storage space for use when running your jobs.  However, this is TEMPORARY storage space intended for transient storage while jobs are running.  Users are expected to move their data from /pananas/scratch to their home or project directory when their job is complete.  Any data over 60 days old is deleted automatically nightly.  Any efforts to modify file dates to purposely subvert this policy are prohibited.  We have sophisticated scripts that monitor for attempts to subvert the system.  Users violating this policy risk ALL of their data in /panasas/scratch being deleted without notice and account deactivation. [See below](##) for more information on this policy.  


!!! Warning
    Violation of CCR policies is a violation of UB Computing and Use policies.  Offenders can be referred to the University at Buffalo's IT security office for disciplinary procedures.

## Scratch Usage Policies

**Temporary Storage on CCR Servers**  

Scratch space is temporary, volatile storage for files. Temporary scratch space is available to users in two different forms: global and local.

**Local Scratch (/scratch)**  
What you need to know about local scratch space:  
- The local scratch space is physically on the node your job is running on.  
- Do NOT use ``/tmp`` or ``/temp`` on any compute nodes as it will fill up the root drive and crash the node, killing your job and any others running on the node!  
- Files stored in local scratch directories are automatically deleted at the end of your job.  

!!! Tip
    **CCR STRONGLY RECOMMENDS** using the Slurm environment variable ``$SLURMTMPDIR`` to manage local scratch. Using this variable in your job script will place temporary job data in ``/scratch/<jobid>`` on the node running the job. This data is removed automatically at the completion of your job.

**Global Scratch (/panasas/scratch)**  
What you need to know about global scratch space:  
- Accessible from all compute and front-end login nodes at CCR  
- Parallel file system that should be used during job execution rather than a user’s home or project directory  
- Groups with active allocation to the Global Scratch resource have access to a sub-directory in ``/panasas/scratch/grp-[groupname]`` - this might be your research group name starting with grp-PIusername or your company name     
- Groups have a 10 TB default quota for their global scratch directory  
- Groups are also subject to a quota of 4 million files and users have a quota of 2 million files  
- We set these user/group quotas for the total number of files in accordance with our system size and projected usage.  Users generating more than a million files per job could affect the performance of the system for everyone.  If you feel your research requires this, we’d like to engage with you to determine if there is an alternate approach  

**Automatic Deletion of Files in Global Scratch**  
- The allowed lifespan of files in global scratch is 60 days from the last file access date.  This is based on the file’s last access timestamp ("atime") on the Panasas file servers.  
- CCR runs an automated cleanup process daily on the filesystem to delete files whose “atime” has reached the maximum lifespan.  
- Altering or duplicating files solely to circumvent the scratch cleanup process is against policy.  

==**Your user account privileges will be revoked if you attempt to get around this rule (i.e. scripting the touching of files to keep them current).**==  

!!! Note "Be a good citizen"
    Global scratch is a shared resource and policies are set to benefit the entire CCR user community.  If you have any questions about the use of these scratch spaces, please [contact CCR Help](../help.md).

## Batch Scheduler Policy

The batch scheduler (Slurm) is configured with a number of scheduling policies to keep in mind. The policies attempt to balance the competing objectives of reasonable queue wait times and efficient system utilization. The details of these policies differ slightly on each system.   

_**Exceptions to the scheduler limits can not be granted as changes can adversely affect other users' jobs as well as the scheduler**_

**Hardware limits**  
[UB-HPC cluster hardware configurations](https://www.buffalo.edu/ccr/support/research_facilities/ub-hpc.html)  
[Industry partition hardware configurations](http://www.buffalo.edu/ccr/support/research_facilities/industry_cluster.html)

Each system differs in the number of processors (cores) and the amount of memory and disk they have per node. We commonly find jobs waiting in the queue that cannot be run on the system where they were submitted because their resource requests exceed the limits of the available hardware. Jobs never migrate between clusters or partitions, so please pay attention to these limits.  CCR currently has more standard (general-compute) nodes and only a small number of large memory and GPU nodes. Your jobs are likely to wait in the queue much longer for a large memory or GPU node than for a standard node. Users often inadvertently request more memory than is available on a standard node and end up waiting for one of the scarce large memory nodes, so check your requests carefully.  

**Walltime limits per job**  
Walltime limits vary per system.  The ub-hpc cluster has a maximum walltime of 72 hours, with the exception of the viz partition which has a maximum of 24 hours.  The faculty cluster partitions vary in max walltime up to a maximum of 30 days.  If your jobs require longer run times, you will need to utilize a form of checkpointing where your job can be picked up where it left off and continue its calculations.  


**Limits per user**  
These limits are applied separately on each cluster and also vary by partition.  Jobs submitted in excess of these limits are rejected by the scheduler.  Limits are per user and include both queued and running jobs.  


| Cluster      | Partition | Limit per User     |
| :---        |    :----:   |          ---: |
| UB-HPC      | general-compute (academic users)       | 1000   |
|    | debug (academic users)        | 4      |
|    | scavenger (academic users)         | 1000      |
|    | viz (accessible via OnDemand viz desktop apps)         | 1      |
|    | industry (business customers only)         | 1000      |
| Faculty   | All faculty cluster partitions          | 1000      |
|    | scavenger (academic users)         | 1000      |


**Short jobs for debugging**  
A small number of nodes are set aside in the debug partition of the ub-hpc cluster with a walltime limit of 1 hour available to academic users. Users are permitted to submit 4 jobs to the debug partition at one time.  These nodes are intended for use in testing codes and setting up job parameters to run on a larger scale.  They are not intended for users to use long-term.  If we believe this policy is being abused, the user will be warned and, if excessive use continues, access to the debug partition will be blocked.


**Scavenger Partition**  
There are scavenger partitions on all CCR clusters.  These partitions provide a way for academic users to access idle nodes.  Jobs submitted to the scavenger partitions will run when there are no other pending or running jobs to run on these idle nodes.  Once a user with access to that partition submits a job requesting resources, jobs in the scavenger partition are stopped and re-queued.  This means if you're running a job in the scavenger partition on an industry node and an industry user submits a job requiring the resources you're consuming, your job will be stopped.  Use of the scavenger partition requires advanced setup and knowledge and is a privilege.  If your jobs are determined to cause problems on any of the private cluster nodes and we receive complaints from the owners of those nodes, your access to the scavenger partitions will be removed.

**Fairshare Limits**  
To keep any one user or group from monopolizing the system when others need the same resources, the scheduler imposes what are known as fairshare limits. If a user or group uses large amounts of computing resources over a period of a month, any new jobs they submit during that period will have reduced priority.  More details on fairshare calculations can be [found here](../hpc/jobs.md)  

**Priority**  
The priority of a job is influenced by many factors, including the processor count requested, the length of time the job has been waiting, how much other computing has been done by the user and their group over the last month (fairshare), and if the group has access to a QOS that provides a priority boost. However, having the highest priority does not necessarily mean that a job will run immediately, as there must also be enough processors and memory available to run it.  See our documentation on the [job scheduler](../hpc/jobs.md) for more info on how priority is calculated and how to check the priority of your pending job(s)  
