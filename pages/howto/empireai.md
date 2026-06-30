# Empire AI Cluster Information

The alpha+ and beta systems of the Empire AI Consortium are in production.  System specifications for both the clusters are in the [Empire AI Alpha+ Beta announcement](https://empireai.freshdesk.com/a/solutions/articles/157000363466).

This page provides information specific to University at Buffalo users of the Empire AI systems.  Please refer to the [Empire AI documentation](https://empireai.freshdesk.com/support/solutions) for all technical usage and general policy information.

## Support

All requests for help should be emailed to `help` `@` `empire-ai.org`.  A subset of CCR staff assist with supporting UB researchers and their group members with non-system related questions on Empire AI clusters.  If we're able, we will respond to your ticket.  If you are having a system issue, we will help facilitate a resolution with the Empire AI system administrators but do not have elevated privileges on the Empire AI clusters.  

If you are using CCR's systems to prepare to onboard to Empire AI and need assistance with that, please submit a ticket to [CCR Help](../help.md).  

## Call for Allocation Proposals

Access to Empire AI resources is done via allocations and is organized under collaborating institutions.  UB's allocations fall under the SUNY umbrella.  Requests for proposals for access to Empire AI resources are currently CLOSED for early 2026.  We anticipate another round of allocation RFPs to be initiated later this year.  This will be communicated to UB Principal Investigators (PIs) from the VPR's office.  

## Allocations

Currently, the process of awarding SUNY allocations is reviewed by SUNY following campus recommendations.  UB's Empire AI allocation committee has reviewed all proposal applications for the Fall 2025 call for proposals and SUNY has selected which projects across the institution are to be awarded with allocations on the Empire AI Alpha+ and Beta clusters.  Applicants have been notified by the UB allocations committee as to the results of the review process.  

It is the intention that CCR staff will work with all research groups on preparing to onboard to Empire AI or to help enhance future allocation proposals.  All PIs awarded allocations have been contacted by CCR staff regarding the steps to take to test their workflows and get onboarded to the alpha cluster.  If you require additional assistance, please request a meeting with CCR's research computing & data science facilitators by completing the [CCR Consultation form](https://ubuffalo.teamdynamix.com/TDClient/55/Portal/Requests/ServiceDet?ID=486).  We highly encourage research groups to work with CCR to prepare your workflow for the Beta cluster.  Please refer to the [Preparing for Onboarding](#preparing-for-eai-onboarding) section for more information.

### Unsuccessful Proposals

If you were not awarded an allocation in this round, don't be discouraged!  There were many more proposals than the system can support.  It is the intention of the teams at CCR and the [Institute for Artificial Intelligence & Data Science (IAD)](https://www.buffalo.edu/ai-data-science.html) to help you and your research group prepare for the next round of proposals.  In the coming months, your group should work to enhance your workflow in CCR's HPC environment so that you will be better prepared for the next call for Empire AI proposals.  If your research group does not have access to CCR, please start by [creating up your accounts](../getting-access.md).  The PI of the group should then [create a project and request allocations](../getting-access.md#requirements-for-accessing-ccrs-resources) in the CCR allocations portal, [ColdFront](https://coldfront.ccr.buffalo.edu).  After access is granted, we recommend reviewing the many [training and documentation resources](../getting-started.md) provided by the CCR support team.  To request a meeting with CCR's research computing & data science facilitators to discuss your group's computing needs, please fill out the [CCR Consultation form](https://ubuffalo.teamdynamix.com/TDClient/55/Portal/Requests/ServiceDet?ID=486).

## Preparing for EAI Onboarding

The best way for a research group to prepare for onboarding to Empire AI's clusters is to test and scale up their workflows in CCR's HPC environment first.  If your research group does not have access to CCR, please see the ["Unsuccessful Proposals" section above](#unsuccessful-proposals) for account setup information.   For those groups that already have access to CCR, we've provided tips for [scaling up your workflows at CCR](#scaling-up-at-ccr).  The EAI Beta cluster contains ARM64 processors so we encourage groups to [request allocations for CCR's `arm64` partition](../portals/coldfront.md#request-an-allocation).  This will allow you to test your containers prior to moving them to EAI.  To request a meeting with CCR's research computing & data science facilitators to discuss your group's computing needs, please fill out the [CCR Consultation form](https://ubuffalo.teamdynamix.com/TDClient/55/Portal/Requests/ServiceDet?ID=486).

## Project Onboarding

CCR staff are equipped to create accounts on the Empire AI cluster for approved PIs and members of their research groups.  Please submit a ticket to [Empire AI](#support) to request account creation for your group.  

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

Empire AI will begin enforcing allocations on September 1, 2026.  To prepare for this, please review their [documentation](https://empireai.freshdesk.com/support/solutions/articles/157000363467-service-units-and-allocations-for-alpha-beta) on service unit calculations and usage.  UB research groups have access to a share of the SUNY allocation.

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

## Storage

Each user is provided a home directory in `/mnt/home/[YourUsername]`  

**There are 100GB quotas on home directories.**

In addition to this, each user has a directory in the global scratch storage.  You'll find yours under `/mnt/lustre/suny`  

For more information on storage on Alpha, please see [EAI's Alpha cluster storage documentation](https://empireai.freshdesk.com/en/support/solutions/articles/157000175046-empire-ai-alpha-storage).  There are no **shared ** project or scratch directories on alpha, like we offer at CCR. Instructions for sharing files on Alpha can be found in [EAI's file sharing documentation](https://empireai.freshdesk.com/en/support/solutions/articles/157000010953-how-can-i-share-data-with-other-users-).

Project directories will be available on Beta.  With the implementation of allocations for Beta, there will be quotas on these directories as well and allocations will be charged for storage usage.  More information on this will be provided by the Empire AI team prior to implementation.

### Data Transfer

**Globus**  
The Globus data transfer service provides the fastest and most secure data transfer speeds. Refer to CCR's [Globus documentation](../hpc/data-transfer.md#globus-transfers) for information on how to use the web interface and search for "Empire AI Alpha" to find the EAI Globus servers.  You'll be prompted to enter your EAI username and password for access to their Globus collection.  

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

### Scaling Up at CCR

CCR's academic (`UB-HPC`) cluster has a mix of compute nodes from various generations of hardware with a variety of GPU types in them. Most of these compute nodes have either 1 or 2 GPUs in them; one node has 12 A16 GPUs. Though you could request multiple nodes with GPUs, our GPU nodes are under heavy demand and wait times can be long, even when only requesting a single GPU. This, combined with the long wait times on the EAI cluster, can make scaling your work more difficult. CCR provides a detailed listing of its resources in [CCR's hardware specification documentation](../hpc/clusters.md#ub-hpc-detailed-hardware-specifications).

To help with preparing to migrate your workflow to Empire AI, CCR has several options for research groups to test on:

- **Scavenger partitions:**  
  Idle compute nodes in both the `UB-HPC` and `Faculty` clusters, including those reserved for industry customers, are available to CCR users. You may run on these idle nodes until a user with a higher priority (the compute node owner or business customer) submit jobs to run on them. All allocations to the "UB-HPC academic partitions" resource have access to scavenger partitions in both the UB-HPC and Faculty clusters. See [CCR's scavenger documentation](../hpc/jobs.md#scavenging-idle-cycles) for details on utitlizing these partitions.

- **EAI partition:**  
  This is a test partition for Empire AI projects that are able to scale beyond the GPUs available in CCR's general-compute partition. Once you're ready for access to this partition, please submit a ticket to [CCR Help](../help.md) and include Grafana charts of recent jobs showing the GPU usage. It's important to be aware that the nodes in this partition are shared with that of the `industry-dgx` partition. These nodes were purchased with economic development money; therefore, industry customers get first access to them. This means jobs submitted to the `eai-test` partition may be preempted, just as if using the [`scavenger` partition](../hpc/jobs.md#scavenging-idle-cycles).

- **ARM64 partition:**  
  Any research group may [request an allocation](../portals/coldfront.md#request-an-allocation) for the `ARM64` partition in ColdFront. This partition contains NVIDIA Gracehopper nodes with 2 GH200 GPUs and 72 ARM64 Neoverse CPUs per node. These are similar to the next iteration of Empire AI equipment ("Beta"). This partition will be an important part of your testing as you prepare to migrate your workflow to Beta in the coming months. NVIDIA containers for this architecture are named with the suffix `-igpu` in the container library. See the [container section below](#containers) for more information on these.
  
  

!!! Tip  
    When running jobs on the `arm64` partition, please be aware of additional [environment setup](../software/march.md#neoverse-v2) required.



## Acknowledging CCR & EAI

We would appreciate you including acknowledgements of CCR and EAI resources, when appropriate, in publications.  See [CCR's acknowledgement FAQ](https://docs.ccr.buffalo.edu/en/latest/faq/#how-do-i-acknowledge-the-use-of-ccr-resources) for CCR's acknowledgement wording and [EAI's acknowledgement documentation](https://empireai.freshdesk.com/en/support/solutions/articles/157000359451-acknowledging-use-of-empire-ai-in-a-paper-or-presentation) for Empire AI's.
