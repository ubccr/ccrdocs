# Getting Started

The Center for Computational Research (CCR) at the University at Buffalo is a high-performance computing center offering faculty, staff, students, and local businesses access to supercomputing environments, high-end visualization services, an on-premise research cloud environment, and experienced staff to help you move your research forward.

!!! Note  
    CCR provides UB's research computing resources.  All other IT services and support at UB is provided by [UBIT](https://buffalo.edu/ubit)  

If you are unfamiliar with CCR and what services and resources we provide, please take a look at our detailed website: [https://buffalo.edu/ccr](https://buffalo.edu/ccr)    

This 30 minute presentation provides a succinct overview of what CCR does and does not provide to the UB research community and industry partners.  You can view additional information on our primary website: https://buffalo.edu/ccr  
![type:video](https://www.youtube.com/embed/lTNXUDZh5T0)  
<br>

## What do you want to do?  

- If you don't already have a CCR account, see  
     - [Getting Access](getting-access.md)  
     - [Frequently Asked Questions about CCR](faq.md)  
- If you're an **experienced HPC user** and ready to log onto a cluster, you probably want to know:
     - What [clusters](hpc/clusters.md) are available  
     - Get instructions for how to [connect to our HPC systems with SSH](hpc/login.md)
     - What [software is available](software/modules.md) and [useful module commands](software/module-commands.md)
     - How to [submit batch jobs](hpc/jobs.md)  
     - How the [file systems](hpc/storage.md) are organized  
     - How to [transfer data](hpc/data-transfer.md) to CCR systems
- If you're **new to high performance computing** or would like additional technical background information, you can:  
    - Learn more about [what resources CCR provides](#computing-resources-at-ccr)
    - Peruse our [virtual workshops on YouTube](https://www.youtube.com/playlist?list=PL4Z5ac7PLRb1Su9J9BXs_TUXNG_RxOcgM)  
    - Read about our [web-based OnDemand portal](portals/ood.md) for easy access to our systems
    - Read this great [Introduction to Linux systems](https://docs.alliancecan.ca/wiki/Linux_introduction) from Compute Canada  
    - Check out our [Linux & Slurm Cheat Sheet](https://buffalo.box.com/s/nqj3neyt2w1dtb3gix6zxqx5gcc9x30n)  
- If you want to use software or develop services that aren't conducive to traditional HPC systems, please read about our [on-premise research cloud](cloud/lake-effect.md)  

!!! Tip
    Need more assistance?  [Contact CCR Help](help.md)  

## Computing Resources at CCR

**High Performance Computing (HPC)**  
*What do you need to know?*  

- HPC resources are available through a cluster environment  
- Users submit batch jobs to a scheduler to run on servers (nodes) within the cluster  
- The UB-HPC cluster is available for academic & industry users    
- CCR also manages a separate cluster for privately purchased faculty nodes     
- Users login using a [SSH client](hpc/login.md) or the [OnDemand web portal](portals/ood.md)  
- There is no cost for UB faculty groups to use the UB-HPC cluster (student accounts must be sponsored by faculty)  
- Storage is shared among the clusters. More [details on storage options](hpc/storage.md)  


**Research Cloud**  
*What do you need to know?*  

- Researchers utilize the on-premise cloud for projects not suited for the HPC environment  
- Examples of cloud uses: database warehouses, websites, container orchestration, software development projects, proof-of-concept testing, and other non-HPC scientific applications  
- Cloud compute time is billed by CPU hour & storage is sold in increments of 1TB  
- Billing info can be found [here](cloud/lake-effect.md)  

!!! Note  
    You must be on an active allocation for the resource(s) you want to use.  [More info here](getting-access.md)  

**What Resources Should I Use?**
This question is difficult to answer because of the range of needs we serve, disciplines we support, and resources we offer.  If the descriptions above were not sufficient, please contact [CCR Help](https://ubccr.freshdesk.com) to discuss.  

In order to identify the best resource to use, we may ask specific questions, such as:

- What software do you want to use?
- Does the software require a commercial license?
- Can the software be used non-interactively? That is, can it be controlled from a file prepared prior to its execution rather than through the graphical interface?
- Can it run on the Linux operating system?
- How much memory, time, computing power, accelerators, storage, network bandwidth and so forth --- are required by a typical job? Rough estimates are fine.
- How frequently will you need to run this type of job?  
You may not know the answer to all of these questions. Please provide as much detail as you can and our technical support team will help you determine the most appropriate resources for your needs.
