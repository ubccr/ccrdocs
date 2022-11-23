# Batch Scheduler Policy

The batch scheduler is configured with a number of scheduling policies to keep in mind. The policies attempt to balance the competing objectives of reasonable queue wait times and efficient system utilization. The details of these policies differ slightly on each system.   

!!! Note
    Exceptions to the scheduler limits can not be granted as changes can adversely affect other users' jobs as well as the scheduler




## Hardware limits  
[UB-HPC cluster hardware configurations](https://www.buffalo.edu/ccr/support/research_facilities/ub-hpc.html)  
[Industry partition hardware configurations](http://www.buffalo.edu/ccr/support/research_facilities/industry_cluster.html)

Each system differs in the number of processors (cores) and the amount of memory and disk they have per node. We commonly find jobs waiting in the queue that cannot be run on the system where they were submitted because their resource requests exceed the limits of the available hardware. Jobs never migrate between clusters or partitions, so please pay attention to these limits.  CCR currently has more standard (general-compute) nodes and only a small number of large memory and GPU nodes. Your jobs are likely to wait in the queue much longer for a large memory or GPU node than for a standard node. Users often inadvertently request more memory than is available on a standard node and end up waiting for one of the scarce large memory nodes, so check your requests carefully.  

## Walltime limits per job  

Walltime limits vary per system.  The ub-hpc cluster has a maximum walltime of 72 hours, with the exception of the viz partition which has a maximum of 24 hours.  The faculty cluster partitions vary in max walltime up to a maximum of 30 days.  If your jobs require longer run times, you will need to utilize a form of checkpointing where your job can be picked up where it left off and continue its calculations.  


## Limits per user  

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


## Short jobs for debugging  

A small number of nodes are set aside in the debug partition of the ub-hpc cluster with a walltime limit of 1 hour available to academic users. Users are permitted to submit 4 jobs to the debug partition at one time.  These nodes are intended for use in testing codes and setting up job parameters to run on a larger scale.  They are not intended for users to use long-term.  If we believe this policy is being abused, the user will be warned and, if excessive use continues, access to the debug partition will be blocked.


## Scavenger Partition  

There are scavenger partitions on all CCR clusters.  These partitions provide a way for academic users to access idle nodes.  Jobs submitted to the scavenger partitions will run when there are no other pending or running jobs to run on these idle nodes.  Once a user with access to that partition submits a job requesting resources, jobs in the scavenger partition are stopped and re-queued.  This means if you're running a job in the scavenger partition on an industry node and an industry user submits a job requiring the resources you're consuming, your job will be stopped.  Use of the scavenger partition requires advanced setup and knowledge and is a privilege.  If your jobs are determined to cause problems on any of the private cluster nodes and we receive complaints from the owners of those nodes, your access to the scavenger partitions will be removed.

## Fairshare Limits  

To keep any one user or group from monopolizing the system when others need the same resources, the scheduler imposes what are known as fairshare limits. If a user or group uses large amounts of computing resources over a period of a month, any new jobs they submit during that period will have reduced priority.  More details on fairshare calculations can be [found here](../hpc/jobs.md)  

## Priority  

The priority of a job is influenced by many factors, including the processor count requested, the length of time the job has been waiting, how much other computing has been done by the user and their group over the last month (fairshare), and if the group has access to a QOS that provides a priority boost. However, having the highest priority does not necessarily mean that a job will run immediately, as there must also be enough processors and memory available to run it.  See our documentation on the [job scheduler](../hpc/jobs.md) for more info on how priority is calculated and how to check the priority of your pending job(s)  
