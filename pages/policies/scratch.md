# Scratch Usage Policies

## Temporary Storage on CCR Servers  

Scratch space is temporary, volatile storage for files. Temporary scratch space is available to users in two different forms: global and local.

###  Local Scratch (/scratch)
What you need to know about local scratch space:  

- The local scratch space is physically on the node your job is running on.  
- Provides the fastest disk I/O  
- The amount of available disk space in ``/scratch`` varies based on type of compute node. See this list for compute node specs  
- Do NOT use ``/tmp`` or ``/temp`` on any compute nodes as it will fill up the root drive and crash the node, killing your job and any others running on the node!  
- For jobs running on more than one node, local scratch on one node is not accessible from another node.  Users should use global scratch for multi-node jobs.  

!!! Note
    CCR STRONGLY RECOMMENDS using the Slurm environment variable ``$SLURMTMPDIR`` to manage local scratch. Using this variable in your job script will place temporary job data in ``/scratch/<jobid>`` on the node running the job. This data is removed automatically at the completion of your job.

### Global Scratch (/panasas/scratch)  
What you need to know about global scratch space:

- Accessible from all compute and front-end login nodes at CCR  
- Parallel file system that should be used during job execution rather than a user’s home or project directory  
- Groups with active allocation to the Global Scratch resource have access to a sub-directory in ``/panasas/scratch/grp-[groupname]`` - this might be your research group name starting with grp-PIusername or your company name
- Exact directory location can be found on the allocation under your project in ColdFront    

#### Global Scratch Quotas:  
- Groups have a 10 TB default quota for their global scratch directory  
- Groups are also subject to a quota of 4 million files  
- Users have a quota of 2 million files  
- Requests for additional global scratch space should be requested by the PI through ColdFront (https://coldfront.ccr.buffalo.edu) as an allocation change request
- A justification for the extra storage or maximum number of files is required. All requests will be reviewed by the CCR Director, and if approved, the bump in quota will be provided for a period of 60 days  
- We set these user/group quotas for the total number of files in accordance with our system size and projected usage.  Users generating more than a million files per job could affect the performance of the system for everyone.  If you feel your research requires this, we’d like to engage with you to determine if there is an alternate approach  

#### Automatic Deletion of Files in Global Scratch  
- The allowed lifespan of files in global scratch is 60 days from the last file access date.  This is based on the file’s last access timestamp ("atime") on the Panasas file servers.  
- CCR runs an automated cleanup process daily on the filesystem to delete files whose “atime” has reached the maximum lifespan.  
- Altering or duplicating files solely to circumvent the scratch cleanup process is against policy.  **Your user account privileges will be revoked if you attempt to get around this rule (i.e. scripting the touching of files to keep them current).**  

!!! Note  
    Global scratch is a shared resource and policies are set to benefit the entire CCR user community.  If you have any questions about the use of these scratch spaces, please contact CCR help.
