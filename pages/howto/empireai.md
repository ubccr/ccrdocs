# Empire AI Cluster Information

The alpha+ and beta systems of the Empire AI Consortium are in production.  System specifications for both the clusters are in the [Empire AI Alpha+ Beta announcement](https://empireai.freshdesk.com/a/solutions/articles/157000363466).

This page provides information specific to University at Buffalo users of the Empire AI systems.  Please refer to the [Empire AI documentation](https://empireai.freshdesk.com/support/solutions) for all technical usage and general policy information.

## Support

All requests for help should be emailed to `help` `@` `empire-ai.org`.  A subset of CCR staff assist with supporting UB researchers and their group members with non-system related questions on Empire AI clusters.  If we're able, we will respond to your ticket.  If you are having a system issue, we will help facilitate a resolution with the Empire AI system administrators but do not have elevated privileges on the Empire AI clusters.  

If you are using CCR's systems to prepare to onboard to Empire AI and need assistance with that, please submit a ticket to [CCR Help](../help.md).  

## Call for Allocation Proposals

Access to Empire AI resources is done via allocations and is organized under collaborating institutions.  UB's allocations fall under the SUNY umbrella.  Requests for proposals for access to Empire AI resources are currently CLOSED for early 2026.  We anticipate another round of allocation RFPs to be initiated later this year.  This will be communicated to UB Principal Investigators (PIs) from the VPR's office.  

## Allocations

Empire AI conducts an annual call for proposals to allocate access to its computing clusters. Resource allocation is managed through a Multi-Factor Priority scheduling system that helps ensure equitable access across the ten participating institutions.

Applicants for the 2025-26 cycle have been notified by the UB allocations committee as to the results of the review process.  All PIs awarded allocations have been contacted by CCR staff regarding the steps to take to test their workflows and get onboarded to the Alpha and Beta clusters.  If you require additional assistance, please request a meeting with CCR's research computing & data science facilitators by completing the [CCR Consultation form](https://ubuffalo.teamdynamix.com/TDClient/55/Portal/Requests/ServiceDet?ID=486).  Please refer to the [Preparing for Onboarding](#preparing-for-eai-onboarding) section for more information on testing workflows for the Beta cluster architecture.

### Unsuccessful Proposals

If you were not awarded an allocation in this round, don't be discouraged!  There were many more proposals than the system can support.  It is the intention of the teams at CCR and the [Institute for Artificial Intelligence & Data Science (IAD)](https://www.buffalo.edu/ai-data-science.html) to help you and your research group prepare for the next round of proposals.  In the coming months, your group should work to enhance your workflow in CCR's HPC environment so that you will be better prepared for the next call for Empire AI proposals.  If your research group does not have access to CCR, please start by [creating up your accounts](../getting-access.md).  The PI of the group should then [create a project and request allocations](../getting-access.md#requirements-for-accessing-ccrs-resources) in the CCR allocations portal, [ColdFront](https://coldfront.ccr.buffalo.edu).  After access is granted, we recommend reviewing the many [training and documentation resources](../getting-started.md) provided by the CCR support team.  To request a meeting with CCR's research computing & data science facilitators to discuss your group's computing needs, please fill out the [CCR Consultation form](https://ubuffalo.teamdynamix.com/TDClient/55/Portal/Requests/ServiceDet?ID=486).

### Allocations Requests Outside Annual Cycle  

UB faculty seeking access outside of the annual proposal cycle may request consideration for available service units. To do so, please complete [this form](https://ubuffalo.teamdynamix.com/TDClient/55/Portal/Requests/Service/542/Empire-AI-Allocation-Request) (UBIT login required) with information about your project. Requests will be reviewed by the Office of Research, Innovation and Economic Development and submitted to Empire AI for consideration based on available resources.


## Preparing for EAI Onboarding

The best way for a research group to prepare for onboarding to Empire AI's clusters is to test and scale up their workflows in CCR's HPC environment first.  If your research group does not have access to CCR, please see the ["Unsuccessful Proposals" section above](#unsuccessful-proposals) for account setup information.   For those groups that already have access to CCR, we've provided tips for [scaling up your workflows at CCR](#scaling-up-at-ccr).  The EAI Beta cluster contains ARM64 processors so we encourage groups to [request allocations for CCR's `arm64` partition](../portals/coldfront.md#request-an-allocation).  This will allow you to test your containers prior to moving them to EAI.  To request a meeting with CCR's research computing & data science facilitators to discuss your group's computing needs, please fill out the [CCR Consultation form](https://ubuffalo.teamdynamix.com/TDClient/55/Portal/Requests/ServiceDet?ID=486).

## Project Onboarding

New projects are created by CCR staff - first creating an account for the PI and then creating a project in ColdFront.  These projects are reviewed, activated, and provisioned by EAI staff.  Once approved, you may begin submitting jobs.  Faculty with active EAI accounts may submit a ticket to [Empire AI](#support) to request additional accounts for your group members.

We highly recommend all new users watch this [Empire AI Orientation video](https://ub.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=fa690d07-453a-4ac0-91c0-b4ec00cc4481) (Panopto login required) creating October 2026.

## Accounts for Research Group Members

Once the PI of the project has access to EAI, they may request additional accounts for their students and collaborators.  **DO NOT SHARE ACCOUNTS.**  Submit a ticket to the [Empire AI](#support) and include the person's full name, institutional email address, and cell phone number.  **External collaborators are not permitted access to the Empire AI clusters.**  

## Account Setup

You will receive an notification when your account is ready.  Please follow [EAI's account activation instructions](https://empireai.freshdesk.com/en/support/solutions/articles/157000366996-activating-your-new-empire-ai-account) to properly setup your account.  

## Getting Started

### Choosing the Right System

Once you have access to Empire AI's systems, please start with [this excellent article](https://empireai.freshdesk.com/support/solutions/articles/157000374441-empire-ai-getting-started-alpha-grace-beta-) detailing out the various capabilities of the clusters and the use cases for each type of hardware

### Mixed Architecture Guidance

The alpha cluster consists of the alpha+ nodes and alpha grace nodes which are two different architecture types.  Please refer to the [Empire AI recommendations](https://empireai.freshdesk.com/support/solutions/articles/157000373787-alpha-and-grace-mixed-architecture-guidance) for utilizing these systems.

### Using the NVIDIA GB200 NVL72 System

NVIDIA's Grace-Blackwell 200 SuperPod makes up the NVL72 system which is designed for large-scale AI and HPC workloads including very large, multi-node jobs that need strong scaling across many GPUs.  Please refer to [Empire AI's documentation](https://empireai.freshdesk.com/support/solutions/articles/157000373786-getting-started-on-the-nvidia-gb200-nvl72) on utilizing these nodes to their greatest potential.

## Service Units and Allocations for Alpha+Beta

Empire AI will begin enforcing allocation usage on October 1, 2026.  SUNY has assigned service units to each project based on the proposals and requests submitted. You are now able to view your project usage in [Empire AI’s ColdFront](https://coldfront.empireai.edu/) allocation portal.  This round of service units will end in June 2027.  Please review the [EAI documentation](https://empireai.freshdesk.com/support/solutions/articles/157000363467-service-units-and-allocations-for-alpha-beta) for more details on service unit calculations.


## Logging In

### Alpha Login Nodes

You must use an SSH client to login to Alpha.  The hostname is:  
`alpha.empire-ai.org`  

If your username on Alpha is not the same as on your computer, you will need to specify it as part of the ssh command.  For example:  

`ssh [YourUsername]@alpha.empire-ai.org`  

Your username on Alpha will be provided by the Empire AI system administrators.

### Beta Login Nodes

You must use an SSH client to login to Alpha. The hostname is:  
`ssh beta.empireai.edu`

If your username on Beta is not the same as on your computer, you will need to specify it as part of the ssh command. For example:

`ssh [YourUsername]@beta.empireai.edu`

Your username on Beta will be provided in the Empire AI new account information received via email.

## Submitting Jobs

Please refer to the [documentation](https://empireai.freshdesk.com/support/solutions/articles/157000374441-empire-ai-getting-started-alpha-grace-beta-) provided by Empire AI for full details on running jobs on the Alpha and Beta clusters.  Here we want to draw your attention to changes being made on the Alpha cluster in September 2026.  The partition names and QOS values will be made to align with the Beta cluster setup.  Therefore, if you're using the `suny` partition and QOS values to submit jobs, you'll need to update your batch scripts or interactive job requests.  All jobs will also need to use the research group's Slurm subaccount. We will no longer use `--account=suny`  

To view your Slurm account and association access use this formatting:  
```
sacctmgr show user [YourUsername] format=user,cluster,account%30,QOS%50  
```
This will display your Slurm account (`suny`) and your subaccount in the form of: `su_PIusername_tag`  
For example: `su_jsmith_llm`  

This is the value you'll use for the Slurm account directive in batch scripts and interactive job requests.  If you have access to multiple projects, you may use any sub-account you have access to.  **As of 9/21/26, all jobs are required to specify an account.**  

Users of the **original Alpha cluster nodes (x86_64)** should use:  
```
--partition=alpha
--qos=depends...see link below
```
[Alpha QOS tiers](https://empireai.freshdesk.com/support/solutions/articles/157000374474-alpha-job-submission-and-qos-overview)

Users of the **Alpha cluster Grace-Grace nodes (arm64/aarch64)** should use:
```
--partition=grace
--qos=depends...see link below
```
[Alpha Grace-Grace nodes QOS tiers](https://empireai.freshdesk.com/support/solutions/articles/157000374494-empire-ai-grace-%E2%80%94-job-submission-and-qos-overview)
Documentation on using Alpha can be [found here](https://empireai.freshdesk.com/en/support/solutions/articles/157000374441-empire-ai-getting-started-alpha-grace-beta-).

Users of the **Beta cluster** should use:
```
--partition=beta
--qos=depends...see link below
```
[Beta cluster QOS tiers](https://empireai.freshdesk.com/support/solutions/articles/157000375992-empire-ai-beta-%E2%80%94-job-submission-and-qos-overview)  
Documentation on using Beta can be [found here](https://empireai.freshdesk.com/support/solutions/articles/157000373786-getting-started-on-the-nvidia-gb200-nvl72).  

### Job Limits

Job submission limits on both the Alpha and Beta cluster are set on the QOS.  Please see the links in the above section for more information.  

#### Alpha

Users must request at least 1 GPU to gain access to all but the CPU-only compute node.  Jobs requesting one GPU will be automatically redirected to an RTX 6000 node.  You will notice the following feature added to your job in the job information:  
```
Features=rtx6000
```
 If you request a specific type of GPU but only one of them, the job will be redirected to an RTX node, and you will see this notice:
```
job\_submit/rtx6000\_gpu\_governance: this is a --gres=gpu:1 job - it will be queued to the RTX 6000 node pool
```
Jobs requesting more than 1 GPU will not be altered at this time.


#### Beta

Jobs are required to request a minimum of 4 GPUs per job to ensure proper alignment with workloads designed for the NVL72 system.  Jobs that do not request 4 or more GPUs will see the error:  
```
srun/sbatch: error: QOSMinGRES\
srun/sbatch: error: Unable to allocate resources: Job violates accounting/QOS policy (job submit limit, user's size and/or time limits)
```

#### GPU Usage Monitoring

Monitoring of GPU usage is in place and jobs not utilizing the GPUs may be automatically canceled without notice if they are not using the resources requested.  


### Cluster Status  

You may view current and historical system status using the [EAI System Status](https://rootly.com/teams/empireai/status-pages/public-system-status-page/public) page.  This tool provides the ability to subscribe to receive updates in real time.


## Storage

### Storage Options  

Please refer to the [Empire AI storage documentation](https://empireai.freshdesk.com/en/support/solutions/articles/157000376738-empire-ai-storage-architecture-user-workflow-guide) for details and workflow suggestions.  This is an overview of the storage options:  

**Home Directories:**  
- Each user is provided a home directory in `/mnt/home/[YourUsername]`  
- There are 100GB quotas on home directories
- Usage is not charged to the group's service units  

**Project Directories:**  
- Each project has it's own subdirectory under `/projects/suny/[PIusername]/[ProjectName]`  
- Quotas are based on requests made in the project proposal  
- Usage is billed in [service units per month](https://empireai.freshdesk.com/en/support/solutions/articles/157000363467-service-units-and-allocations-for-alpha-beta)  
- Usage billing can be viewed and tracked in [ColdFront](https://coldfront.empireai.edu/)  
- If your project needs more than 100TB, please contact [CCR Help](../help.md) to discuss charges  

**Global Scratch Directories:**  
- Each user has a directory in the global scratch storage.  
- You'll find yours under `/mnt/lustre/suny/[YourUsername]` (on Alpha) and `/ddn/scratch/suny/[YourUsername]` (on Beta)  
- Quotas are 5TB and do NOT get charged to the group's service units  
- There is a 30-day purge policy on this scratch filesystem.  **Any data not accessed in 30 days is automatically deleted.**  

**==NO DATA ON EMPIRE AI SYSTEMS IS BACKED UP!==**


### Data Transfer

**Globus**  
The Globus data transfer service provides the fastest and most secure data transfer speeds. Please refer to [Empire AI's Globus documentation](https://empireai.freshdesk.com/en/support/solutions/articles/157000374523-transfer-data-with-globus) for information on authentication and connection to their collections.  If you'd like to transfer between Empire AI and CCR, refer to CCR's [Globus documentation](../hpc/data-transfer.md#globus-transfers) for information on how to use the web interface and search connect to CCR's collections.  

**SFTP**  
Secure FTP is also an option for moving data to the EAI cluster.  You can initiate transfers via the command line or using a SSH client that provides a GUI, such as FileZilla or CyberDuck.  Refer to [CCR's data transfer documentation](../hpc/data-transfer.md#secure-shell-copy) for guidance, substituting the EAI login node with CCR's where appropriate. 

## Software

Some software is installed by EAI administrators.  You can see what is available using the command `module avail`  To load software, you specify the full name with the `module load` command.  For example, to load FFTW, you would run: `module load fftw3/openmpi/gcc/64/3.3.10`  

If software can be installed in a non-standard, alternate location and without administrative priviledges, install it in your home directory, not your scratch directory.

## Containers

CCR **HIGHLY** recommends utilizing [NVIDIA containers](https://catalog.ngc.nvidia.com/containers) for use with our GPUs, as does Empire AI and our NVIDIA tech support partners.  By using the same pre-built containers on CCR, EAI, and your personal workstations, you can easily transition from one system to the next.  CCR provides detailed documentation on best practices for using [Python](../howto/python.md) and [containers](../howto/containerization.md) as well as a self-paced ["Using Python at CCR" course](https://ublearns.buffalo.edu/d2l/le/discovery/view/course/288741) in UB Learns that covers these topics in detail.  For an example workflow of how to use the NVIDIA containers, see [CCR's GPU container example](../howto/containerization.md#example-gpu-container-workflow). Refer to the [Scaling Up at CCR](#scaling-up-at-ccr) section for more information.     

### Apptainer & Singularity - Alpha

Empire AI provides [Singularity/Apptainer](../howto/containerization.md#apptainer) as a module for users to run containers on the **alpha nodes**.  Unlike CCR, you'll need to load the module in order to use this software.  Once loaded, you can use with the `singularity` or `apptainer` command:  

```
module load apptainer
which singularity
alias singularity='apptainer'
        /cm/local/apps/apptainer/current/bin/apptainer
```

### Enroot/Pyxis - Beta

The NVL72 system uses NVIDIA's Enroot tool for containers.  Please refer to the [Empire AI documentation](https://empireai.freshdesk.com/support/solutions/articles/157000373786-getting-started-on-the-nvidia-gb200-nvl72#pyxis-intro) for usage information.  To prepare for the EAI Beta cluster, you will want to use the `ARM64` containers and CCR's `arm64` partition.

### NVIDIA Resources

The [NVIDIA catalog](https://catalog.ngc.nvidia.com) includes [pre-built containers](https://catalog.ngc.nvidia.com/containers) for AI/ML, metaverse, and HPC applications and are performance-optimized, tested, and ready to deploy on CCR's GPUs.  NVIDIA also provides hundreds of [pre-trained models](https://catalog.ngc.nvidia.com/models) for computer vision, speech, recommendation, and more.  The NVIDIA [developer program](https://developer.nvidia.com/) offers hundreds of courses 

## Scaling Up at CCR

CCR's academic (`UB-HPC`) cluster has a mix of compute nodes from various generations of hardware with a variety of GPU types in them. Most of these compute nodes have either 1 or 2 GPUs in them; one node has 12 A16 GPUs. Though you could request multiple nodes with GPUs, our GPU nodes are under heavy demand and wait times can be long, even when only requesting a single GPU. This, combined with the long wait times on the EAI cluster, can make scaling your work more difficult. CCR provides a detailed listing of its resources in [CCR's hardware specification documentation](../hpc/clusters.md#ub-hpc-detailed-hardware-specifications).

To help with preparing to migrate your workflow to Empire AI, CCR has several options for research groups to test on:

- **Scavenger partitions:**  
  Idle compute nodes in both the `UB-HPC` and `Faculty` clusters, including those reserved for industry customers, are available to CCR users. You may run on these idle nodes until a user with a higher priority (the compute node owner or business customer) submit jobs to run on them. All allocations to the "UB-HPC academic partitions" resource have access to scavenger partitions in both the UB-HPC and Faculty clusters. See [CCR's scavenger documentation](../hpc/jobs.md#scavenging-idle-cycles) for details on utitlizing these partitions.

- **EAI partition:**  
  This is a test partition for Empire AI projects that are able to scale beyond the GPUs available in CCR's general-compute partition. Once you're ready for access to this partition, please submit a ticket to [CCR Help](../help.md) and include Grafana charts of recent jobs showing the GPU usage. It's important to be aware that the nodes in this partition are shared with that of the `industry-dgx` partition. These nodes were purchased with economic development money; therefore, industry customers get first access to them. This means jobs submitted to the `eai-test` partition may be preempted, just as if using the [`scavenger` partition](../hpc/jobs.md#scavenging-idle-cycles).

- **ARM64 partition:**  
  Any research group may [request an allocation](../portals/coldfront.md#request-an-allocation) for the `ARM64` partition in ColdFront. This partition contains NVIDIA Gracehopper nodes with 2 GH200 GPUs and 72 ARM64 Neoverse CPUs per node. These are similar to the next iteration of Empire AI equipment ("Beta"). This partition will be an important part of your testing as you prepare to migrate your workflow to Beta in the coming months. NVIDIA containers for this architecture are named with the suffix `-igpu` in the container library. See the [container section below](#containers) for more information on these.

  The high demand and pre-emptibility make using these partitions challenging.  To make more resources more accessible to more users, we ask that you:
 
* Request only the walltime you need.  When testing on the `arm64` partition, please do not request 72-hour interactive jobs as much of this time will leave the GPU idle and prevent other jobs from running.  
* If you need to compile codes or download and test containers on the `arm64` architecture, you can request CPU-only jobs on the `arm64` partition, allowing the GPUs to be left available for other jobs.  
* Monitor your jobs for usage and request only what your job requires.  CCR provides multiple tools for job monitoring as well as [documentation ](https://docs.ccr.buffalo.edu/en/latest/hpc/jobs/#monitoring-jobs)and a [recorded workshop](https://www.youtube.com/watch?v=6DIkXhuYPoY\&t=1s) on the topic.  It’s important to understand that if you request all of the CPUs or RAM (memory) on an `eai-test` compute node without using all of the GPUs, other jobs can’t run.  Monitoring using Grafana will help you understand exactly what resources your job can use so future requests align better with your actual needs.  
* At most, you may submit 4 jobs per user per partition.  If you’re submitting interactive requests, please limit this to one job at a time to prevent resources from sitting idle.

  

!!! Tip  
    When running jobs on the `arm64` partition, please be aware of additional [environment setup](../software/march.md#neoverse-v2) required.



## Acknowledging CCR & EAI

We would appreciate you including acknowledgements of CCR and EAI resources, when appropriate, in publications.  See [CCR's acknowledgement FAQ](https://docs.ccr.buffalo.edu/en/latest/faq/#how-do-i-acknowledge-the-use-of-ccr-resources) for CCR's acknowledgement wording and [EAI's acknowledgement documentation](https://empireai.freshdesk.com/en/support/solutions/articles/157000359451-acknowledging-use-of-empire-ai-in-a-paper-or-presentation) for Empire AI's.
