# Empire AI Cluster Information  

The first test system of the Empire AI Consortium is in production.  This system is referred to as Alpha+ (it's the original alpha cluster plus additional compute nodes added after the initial deployment). Its successor, Beta, is expected to be available in late May 2026.  System specifications for both the clusters are in the [Empire AI Alpha+ Beta announcement](https://empireai.freshdesk.com/a/solutions/articles/157000363466).

## Support  

All requests for help should be emailed to `help` `@` `empire-ai.org`.  A subset of CCR staff assist with supporting researchers and their group members with non-system related questions on Empire AI clusters.  If we're able, we will respond to your ticket.  If you are having a system issue, we will help facilitate a resolution with the Empire AI system administrators but do not have elevated privileges on the Empire AI clusters.  

If you are using CCR's systems to prepare to onboard to Empire AI and need assistance with that, please submit a ticket to [CCR Help](../help.md).  

##  Call for Allocation Proposals  

Access to Empire AI resources is done via allocations and is organized under collaborating institutions.  UB's allocations fall under the SUNY umbrella.  Requests for proposals for access to Empire AI resources are currently CLOSED for early 2026.  We anticipate another round of allocation RFPs to be initiated later this year.  This will be communicated to UB Principal Investigators (PIs) from the VPR's office.  

##  Allocations  

Currently, the process of awarding SUNY allocations is reviewed by SUNY following campus recommendations.  UB's Empire AI allocation committee has reviewed all proposal applications for the Fall 2025 call for proposals and SUNY has selected which projects across the institution are to be awarded with allocations on the Empire AI Alpha+ and Beta clusters.  Applicants have been notified by the UB allocations committee as to the results of the review process.  

It is the intention that CCR staff will work with all research groups on preparing to onboard to Empire AI or to help enhance future allocation proposals.  All PIs awarded allocations have been contacted by CCR staff regarding the steps to take to test their workflows and get onboarded to the alpha cluster.  If you require additional assistance, please request a meeting with CCR's research computing & data science facilitators by completing the [CCR Consultation form](https://ubuffalo.teamdynamix.com/TDClient/55/Portal/Requests/ServiceDet?ID=486).  We highly encourage research groups to work with CCR to prepare your workflow for the Beta cluster.  Please refer to the [Preparing for Onboarding](#preparing-for-eai-onboarding) section for more information.


### Unsuccessful Proposals  

If you were not awarded an allocation in this round, don't be discouraged!  There were many more proposals than the system can support.  It is the intention of the teams at CCR and the [Institute for Artificial Intelligence & Data Science (IAD)](https://www.buffalo.edu/ai-data-science.html) to help you and your research group prepare for the next round of proposals.  In the coming months, your group should work to enhance your workflow in CCR's HPC environment so that you will be better prepared for the next call for Empire AI proposals.  If your research group does not have access to CCR, please start by [creating up your accounts](../getting-access.md).  The PI of the group should then [create a project and request allocations](../getting-access.md#requirements-for-accessing-ccrs-resources) in the CCR allocations portal, [ColdFront](https://coldfront.ccr.buffalo.edu).  After access is granted, we recommend reviewing the many [training and documentation resources](../getting-started.md) provided by the CCR support team.  To request a meeting with CCR's research computing & data science facilitators to discuss your group's computing needs, please fill out the [CCR Consultation form](https://ubuffalo.teamdynamix.com/TDClient/55/Portal/Requests/ServiceDet?ID=486).


## Preparing for EAI Onboarding  

The best way for a research group to prepare for onboarding to Empire AI's clusters is to test and scale up their workflows in CCR's HPC environment first.  If your research group does not have access to CCR, please see the ["Unsuccessful Proposals" section above](#unsuccessful-proposals) for account setup information.   For those groups that already have access to CCR, we've provided tips for [scaling up your workflows at CCR](#scaling-up-at-ccr).  The EAI Beta cluster will contain ARM64 processors so we encourage groups to [request allocations for CCR's `arm64` partition](../portals/coldfront.md#request-an-allocation).  This will allow you to test your containers prior to moving them to EAI.  To request a meeting with CCR's research computing & data science facilitators to discuss your group's computing needs, please fill out the [CCR Consultation form](https://ubuffalo.teamdynamix.com/TDClient/55/Portal/Requests/ServiceDet?ID=486).


## Project Onboarding  

CCR staff are equipped to create accounts on the Empire AI cluster for approved PIs and members of their research groups.  Please submit a ticket to [CCR Help](../help.md) to request account creation for your group.  Once the Beta cluster is available for users, CCR will invite research groups to an onboarding workshop. 

This recording of the Empire AI On-boarding Workshop from June 2025 is mostly accurate for utilizing the Alpha cluster:
![type:video](https://youtube.com/embed/WoACuDqJC0c)  

## Accounts for Research Group Members  

Once the PI of the project has access to EAI, they may request additional accounts for their students and collaborators.  **DO NOT SHARE ACCOUNTS.**  Submit a ticket to the [CCR Help](../help.md) and include the person's full name, institutional email address, and cell phone number.  External collaborators are not permitted access the the Empire AI clusters.    

## Account Setup  

You will receive an notification when your account is ready.  Please follow [EAI's account activation instructions](https://empireai.freshdesk.com/en/support/solutions/articles/157000366996-activating-your-new-empire-ai-account) to properly setup your account.  

## Logging In - Alpha Cluster 

You must use an SSH client to login to Alpha.  The hostname is:  
`alpha.empire-ai.org`  

If your username on Alpha is not the same as on your computer, you will need to specify it as part of the ssh command.  For example:  

`ssh [YourUsername]@alpha.empire-ai.org`  

Your username on Alpha will be provided by the Empire AI system administrators.


## Storage  

Each user is provided a home directory in `/mnt/home/[YourUsername]`  

In addition to this, each user has a directory in the global scratch storage.  You'll find yours under `/mnt/lustre/suny`  

For more information on storage on Alpha, please see [EIA's Alpha cluster storage documentation](https://empireai.freshdesk.com/en/support/solutions/articles/157000175046-empire-ai-alpha-storage).

At this time there are no quotas on these filesystems; however, quotas will be enforced once the Beta cluster is in production.  Additional details about quotas and allocations is forthcoming.  There is also no automatic clearing of the scratch directories, as there are at CCR.  With the implementation of allocations for Beta, there will be quotas on the filesystem.  

There are no shared project or scratch directories, like we offer at CCR.  Instructions for sharing files on Alpha can be found in [EAI's file sharing documentation](https://empireai.freshdesk.com/en/support/solutions/articles/157000010953-how-can-i-share-data-with-other-users-).

### Data Transfer  

**Globus**  
The Globus data transfer service provides the fastest and most secure data transfer speeds. Refer to CCR's [Globus documentation](../hpc/data-transfer.md#globus-transfers) for information on how to use the web interface and search for "Empire AI Alpha" to find the EAI Globus servers.  You'll be prompted to enter your EAI username and password for access to their Globus collection.  

**SFTP**  
Secure FTP is also an option for moving data to the EAI cluster.  You can initiate transfers via the command line or using a SSH client that provides a GUI, such as FileZilla or CyberDuck.  Refer to [CCR's data transfer documentation](../hpc/data-transfer.md#secure-shell-copy) for guidance, substituting the EAI login node with CCR's where appropriate. 

## Software  

Some software is installed by EAI administrators.  You can see what is available using the command `module avail`  To load software, you specify the full name with the `module load` command.  For example, to load FFTW, you would run: `module load fftw3/openmpi/gcc/64/3.3.10`  

If software can be installed in a non-standard, alternate location and without administrative priviledges, install it in your home directory, not your scratch directory.

## Running Jobs

The EAI cluster uses the same job scheduler, Slurm, as CCR uses.  This should make your transition easier.  


### Partitions  

UB users have access to the `suny` partition and should submit all requests for GPU resources there.  Users also have access to the [CPU-only node](#cpu-only-node) in the `cpu` partition.  For more information on partitions/queues, refer to [CCR's Slurm partition documentation](https://empireai.freshdesk.com/en/support/solutions/articles/157000168778-slurm-partitions-queues-).  


### Specifying walltime

The default walltime on the alpha cluster is set to 1 hour.  Make sure to specify your walltime needs using:  
```
## Walltime Format: dd:hh:mm:ss
#SBATCH --time=00:01:00
```
The maximum walltime on the `suny` partition is 7 days.

### Job Limits    

The alpha cluster has several job limits users should be aware of.  The `MaxJobsPU` or maximum number of jobs a user can run at one time is set to 30.  The `MaxSubmitPU` or the maximum number of jobs a user can submit to the queue at once is set to 200.  

### Requesting GPUs 

When submitting jobs on the Alpha cluster, just as on CCR's clusters, you must specify the number of GPUs you want.  Use the Slurm option:  `--gpus-per-node=X`


### CPU-only node  

Currently, there is 1 alpha compute node with no GPUs available to all users.  This is great for testing workflows and verifying your code executes without having to wait for a long time in the queue behind GPU jobs.  To use this node, specify: `--partition=cpu`  

### Accessing the node(s) your job is running on  

Whether you've submitted an interactive job or a batch job, you may need to access the compute node your job is running on.  Once the job starts, you will be given a job ID and the name of the job's headnode.  To login to the headnode, use `ssh [nodename]` or using `srun` as per [CCR's job login instructions](../hpc/login.md#compute-node-logins).  


## Monitoring Jobs  

Monitoring your jobs and the resources they use is a critical piece of utilizing a shared cluster environment.  Knowing what your workflow needs and requesting only those resources will ensure you spend the least amount of time in the queue as possible and you'll be a good citizen of the shared environment.  Information about monitoring your CCR jobs can be found in [CCR's job monitoring documentation](../hpc/jobs.md#monitoring-jobs).  Though the EAI cluster doesn't have Grafana or XDMoD for metrics reporting, you can monitor active jobs with tools described in [CCR's job monitoring documentation](../hpc/jobs.md#active-jobs-monitoring---command-line).  For information on GPU usage in an active job, use the `nvidia-smi` command on your job's compute node.  

### When will my job start?  

See [CCR's job start documentation](../faq.md#when-will-my-job-start)  

It's possible and likely that your job may not have a start time.  It's not possible for the scheduler to estimate all jobs in the queue at all times.  

### What's my job's priority?

The alpha cluster runs in a fairshare mode, similar to CCR's UB-HPC cluster.  See [CCR's job priority documentation](../hpc/jobs.md#job-priority) for tools on assessing priority and fairshare values.

## Scaling Up at CCR  

CCR's academic (`UB-HPC`) cluster has a mix of compute nodes from various generations of hardware with a variety of GPU types in them.  Most of these compute nodes have either 1 or 2 GPUs in them; one node has 12 A16 GPUs.  Though you could request multiple nodes with GPUs, our GPU nodes are under heavy demand and wait times can be long, even when only requesting a single GPU.  This, combined with the long wait times on the EAI cluster, can make scaling your work more difficult. CCR provides a detailed listing of its resources in [CCR's hardware specification documentation](../hpc/clusters.md#ub-hpc-detailed-hardware-specifications).  

To help with preparing to migrate your workflow to Empire AI, CCR has several options for research groups to test on:  

  - **Scavenger partitions:**  
  Idle compute nodes in both the `UB-HPC` and `Faculty` clusters, including those reserved for industry customers, are available to CCR users.  You may run on these idle nodes until a user with a higher priority (the compute node owner or business customer) submit jobs to run on them. All allocations to the "UB-HPC academic partitions" resource have access to scavenger partitions in both the UB-HPC and Faculty clusters.  See [CCR's scavenger documentation](../hpc/jobs.md#scavenging-idle-cycles) for details on utitlizing these partitions.  
  - **EAI partition:**  
  This is a test partition for Empire AI projects that are able to scale beyond the GPUs available in CCR's general-compute partition.  Once you're ready for access to this partition, please submit a ticket to [CCR Help](../help.md) and include Grafana charts of recent jobs showing the GPU usage.  It's important to be aware that the nodes in this partition are shared with that of the `industry-dgx` partition.  These nodes were purchased with economic development money; therefore, industry customers get first access to them.  This means jobs submitted to the `eai-test` partition may be preempted, just as if using the [`scavenger` partition](../hpc/jobs.md#scavenging-idle-cycles).  
  - **ARM64 partition:**  
  Any research group may [request an allocation](../portals/coldfront.md#request-an-allocation) for the `ARM64` partition in ColdFront.  This partition contains NVIDIA Gracehopper nodes with 2 GH200 GPUs and 72 ARM64 Neoverse CPUs per node.  These are similar to the next iteration of Empire AI equipment ("Beta").  This partition will be an important part of your testing as you prepare to migrate your workflow to Beta in the coming months.  NVIDIA containers for this architecture are named with the suffix `-igpu` in the container library.  See the [container section below](#containers) for more information on these.  

    !!! Tip  
        When running jobs on the `arm64` partition, please be aware of additional [environment setup](../software/march.md#neoverse-v2) required. 

## GUI Applications and IDE Tools  

The Empire AI cluster does not provide an interface for GUI-based applications or IDE tools such as VSCode, RStudio, or Jupyter Lab.  At the present time, you may use VSCode to connect to the EAI login node; however, this may change in the future.  From the login node, you may use the VSCode terminal and SSH to login to the head node of your job.  This method is not recommended and CCR staff are unable to support this.  Some tasks can be automated within R or Jupyter using scripts that can be submitted as batch jobs.  Though we don't provide specific documentation for this, we can offer assistance with finding potential solutions for your workflow.  For visualization, you can transfer your data to CCR and utilize our [Open OnDemand portal](../portals/ood.md).  CCR provides interactive apps through OnDemand for [Matlab](../portals/ood.md#matlab-app), [RStudio](../portals/ood.md#rstudio-app), [VSCode](../portals/ood.md#vscode-app), [Jupyter Lab/Notebook](../portals/ood.md#jupyter-notebook-apps), and the ability to use [containers with Jupyter](../portals/ood.md#jupyter-app-for-containers) and [RStudio](../portals/ood.md#rstudio-app).  

## Containers  

CCR **HIGHLY** recommends utilizing [NVIDIA containers](https://catalog.ngc.nvidia.com/containers) for use with our GPUs, as does Empire AI and our NVIDIA tech support partners.  By using the same pre-built containers on CCR, EAI, and your personal workstations, you can easily transition from one system to the next.  CCR provides detailed documentation on best practices for using [Python](../howto/python.md) and [containers](../howto/containerization.md) as well as a self-paced ["Using Python at CCR" course](https://ublearns.buffalo.edu/d2l/le/discovery/view/course/288741) in UB Learns that covers these topics in detail.  For an example workflow of how to use the NVIDIA containers, see [CCR's GPU container example](../howto/containerization.md#example-gpu-container-workflow). To prepare for the EAI Beta cluster, you will want to use the `ARM64` containers and CCR's `arm64` partition.  Refer to the [Scaling Up at CCR](#scaling-up-at-ccr) section for more information.     

### Apptainer & Singularity  

Empire AI provides [Singularity/Apptainer](../howto/containerization.md#apptainer) on the cluster for users to run containers.  Unlike CCR, you'll need to load the module in order to use this software.  Once loaded, you can use with the `singularity` or `apptainer` command:  
```
module load singularity  
which singularity
alias singularity='apptainer'
        /cm/local/apps/apptainer/current/bin/apptainer
```

### NVIDIA Resources  

The [NVIDIA catalog](https://catalog.ngc.nvidia.com) includes [pre-built containers](https://catalog.ngc.nvidia.com/containers) for AI/ML, metaverse, and HPC applications and are performance-optimized, tested, and ready to deploy on CCR's GPUs.  NVIDIA also provides hundreds of [pre-trained models](https://catalog.ngc.nvidia.com/models) for computer vision, speech, recommendation, and more.  The NVIDIA [developer program](https://developer.nvidia.com/) offers hundreds of courses 

## Acknowledging CCR & EAI  

We would appreciate you including acknowledgements of CCR and EAI resources, when appropriate, in publications.  See [CCR's acknowledgement FAQ](https://docs.ccr.buffalo.edu/en/latest/faq/#how-do-i-acknowledge-the-use-of-ccr-resources) for CCR's acknowledgement wording and [EAI's acknowledgement documentation](https://empireai.freshdesk.com/en/support/solutions/articles/157000359451-acknowledging-use-of-empire-ai-in-a-paper-or-presentation) for Empire AI's.

