# Getting Started

The Center for Computational Research (CCR) at the University at Buffalo is a high-performance computing center offering faculty, staff, students, and local businesses access to supercomputing environments, high-end visualization services, an on-premise research cloud environment, and experienced staff to help you move your research forward.

!!! Note  
    CCR provides UB's research computing resources.  All other IT services and support at UB is provided by [UBIT](https://buffalo.edu/ubit)  

If you are unfamiliar with CCR and what services and resources we provide, please take a look at our detailed website: [https://buffalo.edu/ccr](https://buffalo.edu/ccr)    

This 20 minute presentation given by the CCR Director in 2020 provides a succinct overview.  We will not cover that information here as this site is dedicated to documentation for using our resources  
![type:video](https://youtube.com/embed/ryBqdeqTO4o)  

## What do you want to do?  

- If you don't already have a CCR account, see  
     - [Getting Access](getting-access.md)  
     - [Frequently Asked Questions about CCR](faq.md)  
- If you're an experienced HPC user and ready to log onto a cluster, you probably want to know:
     - What [clusters](hpc/node-types.md) are available  
     - What [software is available](software/about.md) and how [environment modules](software/modules.md) work  
     - How to [submit jobs](hpc/jobs.md)  
     - How the [file system](hpc/storage.md) is organized
- If you're new to HPC or would like additional technical background information, you can  
    - Peruse our [virtual workshops on YouTube](https://www.youtube.com/playlist?list=PL4Z5ac7PLRb1Su9J9BXs_TUXNG_RxOcgM)  
    - Read about how to connect to our HPC systems with SSH
    - Learn more about [data transfer](hpc/data-transfer.md) to CCR systems
    - Read this great [Introduction to Linux systems](https://docs.alliancecan.ca/wiki/Linux_introduction) from Compute Canada  
    - Check out our Linux & Slurm Cheat Sheet
- If you want to use software or develop services that aren't conducive to traditional HPC systems, please read about our [on-premise research cloud](cloud/lake-effect.md)  

## Computing Resources at CCR

**High Performance Computing (HPC)**  
*What do you need to know?*  

- HPC resources are available through a cluster environment  
- Users submit batch jobs to a scheduler to run on servers (nodes) within the cluster  
- The UB-HPC cluster is available for academic & industry users    
- CCR also manages a separate cluster for privately purchased faculty nodes   
- [Visualization servers](../hpc/viz) are available for graphically-intense scientific software  
- Users login using a [SSH client](../hpc/login) or the [OnDemand web portal](../portals/ood)  
- There is no cost for cluster compute time for UB faculty groups (students must be sponsored by faculty)  
- Storage is shared among the clusters. More [details on storage options](../hpc/storage)  


**Research Cloud**  
*What do you need to know?*  

- Researchers utilize the on-prem cloud for projects not suited for the HPC environment  
- Examples of cloud uses: database warehouses, websites, container orchestration, software development projects, and other non-HPC scientific applications  
- Cloud compute time is billed by CPU hour & storage is sold in increments of 1TB  
- Billing info can be found [here](lake-effect.md)  

!!! Note  
    You must be on an active allocation for the resource(s) you want to use.  [More info here](getting_access.md)  

**What Resources Should I Use?**
This question is difficult to answer because of the range of needs we serve, disciplines we support, and resources we offer.  If the descriptions above were not sufficient, please contact CCR Help to discuss.  

In order to identify the best resource to use, we may ask specific questions, such as:

- What software do you want to use?
- Does the software require a commercial license?
- Can the software be used non-interactively? That is, can it be controlled from a file prepared prior to its execution rather than through the graphical interface?
- Can it run on the Linux operating system?
- How much memory, time, computing power, accelerators, storage, network bandwidth and so forth --- are required by a typical job? Rough estimates are fine.
- How frequently will you need to run this type of job?
You may know the answer to these questions or not. If you do not, our technical support team is there to help you find the answers. Then they will be able to direct you to the most appropriate resources for your needs.


## Application Software Available on the CCR Clusters

There are many scientific, engineering, bioinformatics, and visualization software applications already installed on the clusters.  You are welcome to install software for your own use in your home or project directories, if it doesn't require elevated privileges.   If it does, submit a help ticket to request the installation of the software package and, if it is possible, we will install it for you.  More information about available software and how to install your own can be [found here](software/about.md)  
