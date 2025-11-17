# Empire AI Cluster Information  

The first test system of the Empire AI Consortium is in production.  This system is provided and managed by the Flatiron Institute.  System specifications can be found [here](https://empireai.freshdesk.com/en/support/solutions/articles/157000007946-alpha-hardware).  This system is referred to as Alpha and its successor Beta is expected to be available in Fall 2025.  

Initial project applications have been submitted to consortium members, reviewed, and are being onboarded on an ongoing basis by the Empire AI director and Flatiron system administrators.  CCR staff provide support to UB research groups that have access to Alpha - both on using the EAI system and in helping to prepare groups to utilize those resources efficiently.

Recording of the Empire AI On-boarding Workshop from June 2025:
![type:video](https://youtube.com/embed/WoACuDqJC0c) 

## Support  

All requests for help should be emailed to `help` `@` `empire-ai.org`.  CCR staff help with supporting researchers and their group members with non-system related questions.  If you are having a system issue, we will help facilitate a resolution but do not have elevated privileges on the Empire AI cluster.  

If you are using CCR's systems to prepare to onboard to Empire AI and need assistance, please submit a ticket to [CCR Help](../help.md).  

##  Allocation Proposals  

Access to Empire AI resources is done via allocations and are organized under collaborating institutions.  UB's allocations fall under the SUNY umbrella.  Requests for proposals for access to Empire AI resources are currently CLOSED for 2025.  We anticipate another round of allocation RFPs to be initiated in early 2026.  This will be communicated to UB PIs from the VPR's office.  

## Project Onboarding  

**Decisions on which projects get selected from UB for access to Empire AI is done by the VPR's office.**  Once a project has been selected for onboarding, the UB PI will be notified by the EAI director and will be asked to complete a form.  Once that's submitted, the PI's information is forwarded to the Empire AI system administrators for account creation.  You will hear directly from one of them when your account is ready and they'll provide additional account setup instructions.   

## Accounts for Research Group Members  

Once the PI of the project has access to Alpha, they may request additional accounts for their students and collaborators.  **DO NOT SHARE ACCOUNTS.**  Submit a ticket to the [EAI support desk](#support) and a CCR staff member will facilitate the account setup.  New users will be asked to complete a form and then the user information is passed to the EAI system administrators for account creation.

## Account Setup  

You will receive notification from the Empire AI system administration team when your account is ready.  Please follow [these instructions](https://empireai.freshdesk.com/en/support/solutions/articles/157000366996-activating-your-new-empire-ai-account) to properly setup your account.  

## Logging In  

You must use an SSH client to login to Alpha.  The hostname is:  
`alpha.empire-ai.org`  

If your username on Alpha is not the same as on your computer, you will need to specify it as part of the ssh command.  For example:  

`ssh [YourUsername]@alpha.empire-ai.org`  

Your username on alpha will be provided by the Empire AI system administrators.


## Storage  

Each user is provided a home directory in `/mnt/home/[YourUsername]`  

In addition to this, each user has a directory in the global scratch storage.  You'll find yours under `/mnt/lustre/suny`  

For more information on storage on Alpha, please see [here](https://empireai.freshdesk.com/en/support/solutions/articles/157000175046-empire-ai-alpha-storage).

At this time there are no quotas on these filesystems; however, we've been told to expect that this will be coming soon.  There is also no automatic clearing of the scratch directories, as there are at CCR.  With the implementation of allocations for beta, there will be quotas on the filesystem.  

There are no shared project or scratch directories, like we offer at CCR.  Instructions for sharing files on Alpha can be found [here](https://empireai.freshdesk.com/en/support/solutions/articles/157000010953-how-can-i-share-data-with-other-users-).

### Data Transfer  

**Globus**  
The Globus data transfer service provides the fastest and most secure data transfer speeds. Refer to CCR's [Globus documentation](../hpc/data-transfer.md#globus-transfers) for info on how to use the web interface and search for "Empire AI Alpha" to find the EAI Globus servers.  You'll be prompted to enter your alpha username and password for access to their Globus collection.  

**SFTP**  
Secure FTP is also an option for moving data to the EAI cluster.  You can initiate transfers via the command line or using a SSH client that provides a GUI, such as FileZilla or CyberDuck.  Refer to CCR's [data transfer documentation](../hpc/data-transfer.md#secure-shell-copy) for guidance, substituting the EAI login node with CCR's where appropriate. 

## Software  

Some software is installed by EAI administrators.  You can see what is available using the command `module avail`  To load software, you specify the full name with the `module load` command.  For example, to load FFTW, you would run: `module load fftw3/openmpi/gcc/64/3.3.10`  

If software can be in an alternate location and without administrative priviledges, install it in your home directory, not your scratch directory.

## Running Jobs

The EAI alpha cluster uses the same job scheduler, Slurm, as CCR uses.  This should make your transition easier.  


### Partitions  

UB users have access to the `suny` partition and should submit all requests for GPU resources there.  For more info on partitions/queues, refer [here](https://empireai.freshdesk.com/en/support/solutions/articles/157000168778-slurm-partitions-queues-).  


### Specifying walltime

The default walltime on the alpha cluster is set to 1 hour.  Make sure to specify your walltime needs using:  
```
## Walltime Format: dd:hh:mm:ss
#SBATCH --time=00:01:00
```
The maximum walltime on the `suny` partition is 7 days.

### Requesting GPUs 

When submitting jobs on the Alpha cluster, just as on CCR's clusters, you must specify the number of GPUs you want.  Use the Slurm option:  `--gpus-per-node=X`


### CPU-only node  

Currently, there is 1 alpha compute node with no GPUs available to all users.  This is great for testing workflows and verifying your code executes without having to wait for a long time in the queue behind GPU jobs.  To use this node, specify: `--partition=cpu`  

### Accessing the node(s) your job is running on  

Whether you've submitted an interactive job or a batch job, you may need to access the compute node your job is running on.  Once the job starts, you will be given a job ID and the name of the job's headnode.  To login to the headnode, use `ssh [nodename]` or [this method](../hpc/login.md#compute-node-logins) we use at CCR.  


## Monitoring Jobs  

Monitoring your jobs and the resources they use is a critical piece of utilizing a cluster environment.  Knowing what your workflow needs and requesting only those resources will ensure you spend the least amount of time in the queue as possible and you'll be a good citizen of the shared environment.  Information about monitoring your CCR jobs can be found [here](../hpc/jobs.md#monitoring-jobs).  Though the EAI cluster doesn't have Grafana or XDMoD for metrics reporting, you can monitor active jobs with tools described [here](../hpc/jobs.md#active-jobs-monitoring---command-line).  For information on GPU usage in an active job, use the `nvidia-smi` command on your job's compute node.  

### When will my job start?  

See [here](../faq.md#when-will-my-job-start)  

It's possible and likely that your job may not have a start time.  It's not possible for the scheduler to estimate all jobs in the queue at all times.  

### What's my job's priority?

The alpha cluster runs in a fairshare mode, similar to CCR's UB-HPC cluster.  See [here](../hpc/jobs.md#job-priority) for tools on assessing priority and fairshare values.

## Scaling Up at CCR  

CCR's academic cluster has a mix of compute nodes from various generations of hardware with a variety of GPU types in them.  Most of these compute nodes have either 1 or 2 GPUs in them; one node has 12 A16 GPUs.  Though you could request multiple nodes with GPUs, our GPU nodes are under heavy demand and wait times can be long, even when only requesting a single GPU.  This, combined with the long wait times on the Alpha cluster, can make scaling your work more difficult. To help with preparing to migrate your workflow to Empire AI, CCR has several options for EAI groups to test on.  

  - **Scavenger partition:**  
  Idle compute nodes in both clusters, including those reserved for industry customers, are available to users of the UB-HPC cluster.  You may run on these idle nodes until a user with a higher priority (the compute node owner or business customer) submit jobs to run on them. All allocations to the "UB-HPC academic partitions" resource have access to scavenger partitions in both the UB-HPC and Faculty clusters.  See [here](../hpc/jobs.md#scavenging-idle-cycles) for details on utitlizing these partitions.  
  - **EAI partition:**  
  This is a test partition for Empire AI projects that are able to scale beyond the GPUs available in CCR's general-compute partition.  Once you're ready for access to this partition, please submit a ticket to [CCR Help](../help.md) and include Grafana charts of recent jobs showing the GPU usage.  
  - **ARM64 partition:**  
  Any CCR researcher may request an allocation for the `ARM64` partition in ColdFront.  This partition contains [NVIDIA Gracehopper nodes](../hpc/clusters.md#compute-nodes) with 2 GH 200 GPUs and 72 ARM64 Neoverse CPUs per node.  These are similar to the next iteration of Empire AI equipment ("beta") anticipated for Fall 2025.  This partition will be an important part of your testing as you prepare to migrate your workflow to beta in the coming months.  NVIDIA containers for this architecture are named with the suffix `-igpu` in the container library.  See [below](#containers) for more info on these.  

## GUI Applications and IDE Tools  

The Empire AI alpha cluster does not provide an interface for GUI-based applications or IDE tools such as VSCode, RStudio, or Jupyter Lab.  At the present time, you may use VSCode to connect to the Alpha login node; however, this may change in the future.  From the login node, you may use the VSCode terminal and SSH to login to the head node of your job.  This method is not recommended and CCR staff are unable to support this.  Some tasks can be automated within R or Jupyter using scripts that can be submitted as batch jobs.  Though we don't provide specific documentation for this, we can offer assistance with finding potential solutions for your workflow.  For visualization, you can transfer your data to CCR and utilize our [Open OnDemand portal](../portals/ood.md).  

## Containers  

CCR recommends utilizing [NVIDIA containers](https://catalog.ngc.nvidia.com/containers) for use with our GPUs, as does Empire AI and our NVIDIA tech support partners.  By using the same pre-built containers on CCR, EAI, and your personal workstations, you can easily transition from one system to the next.  CCR provides detailed documentation on best practices for using [Python](../howto/python.md) and [containers](../howto/containerization.md) as well as a self-paced ["Using Python at CCR" course](https://ublearns.buffalo.edu/d2l/le/discovery/view/course/288741) in UB Learns that covers these topics in detail.  For an example workflow of how to use the NVIDIA containers, see [here](../howto/containerization.md#example-gpu-container-workflow).  

### NVIDIA Resources  

The [NVIDIA catalog](https://catalog.ngc.nvidia.com) includes [pre-built containers](https://catalog.ngc.nvidia.com/containers) for AI/ML, metaverse, and HPC applications and are performance-optimized, tested, and ready to deploy on CCR's GPUs.  NVIDIA also provides hundreds of [pre-trained models](https://catalog.ngc.nvidia.com/models) for computer vision, speech, recommendation, and more.  The NVIDIA [developer program](https://developer.nvidia.com/) offers hundreds of courses 

## Acknowledging CCR & EAI  

We would appreciate you including acknowledgements of CCR and EAI resources, when appropriate, in publications.  See [here](https://docs.ccr.buffalo.edu/en/latest/faq/#how-do-i-acknowledge-the-use-of-ccr-resources) for CCR's acknowledgement wording and [here](https://empireai.freshdesk.com/en/support/solutions/articles/157000359451-acknowledging-use-of-empire-ai-in-a-paper-or-presentation) for Empire AI's.

  

