# Clusters

CCR maintains two clusters; *ub-hpc* and *faculty*. Within each cluster exist partitions (queues) that users can request to have their jobs run on. Not all partitions are available to all users. Below are descriptions of the clusters and the partitions. 

Compute nodes on all CCR clusters are subject to monthly downtimes. Downtime information can be found [here](https://ubccr.freshdesk.com/support/discussions/forums/5000296650)

Examples on how to run on these clusters and partitions can be found [here](https://docs.ccr.buffalo.edu/en/latest/hpc/jobs/).
 
###### UB-HPC Compute Cluster

The ub-hpc cluster contains the following partitions:

* arm64: Compute nodes with ARM64 processors & specialized GPUs  
* class: Dedicated compute nodes for faculty teaching classes  
* debug: Dedicated compute nodes to help users debug their workflows  
* general-compute: Large pool of compute nodes for academic users  
* industry: Compute nodes industry partners pay to use  
* scavenger: Preemptible jobs on all ub-hpc nodes  
* viz: Dedicated compute nodes to allow short jobs for visualization purposes  


###### Faculty Compute Cluster

This cluster contains over 50 faculty owned or project specific partitions. Access to these partitions is determined by the owner and managed via allocations in [ColdFront](../portals/coldfront.md). All idle nodes in the faculty cluster are accessible to UB-HPC users in the scavenger partition.  Scavenger jobs will be [preemptively canceled](jobs.md#scavenging-idle-cycles) when jobs are submitted by members of the group that owns the node.  

## Node types

CCR has several node types available in our clusters.  Each node type is meant for certain tasks. These node types are relatively common for other HPC centers. We will discuss each node type and its intended use below.


### Login Nodes

* _Use for_: editing scripts, moving files, small data transfers, submitting jobs  
* _Do not use for_: Heavy computations, building software or long running processes  
* 15 Minute time limit on running processes  
* Many users are typically logged into these at the same time  
* Connections are load balanced across many servers  

### Compile Nodes

* _Use for_: [Building Software](../software/building.md)   
* _Do not use for_: Heavy computations  
* Access these nodes by typing `ssh compile` from a login node

### Compute Nodes

* Where jobs are executed after being submitted to the slurm scheduler  
* Intended for heavy computation  
* When running an [interactive job](./jobs.md) will be performing tasks directly on the compute nodes  
* Only users with active jobs can log in to allocated nodes  

### Debug Nodes

* Compute nodes reserved for testing and debugging jobs  
* Accessed by submitting a debug job in slurm  
* 1 hour walltime limit on debug jobs  

### Visualization Nodes

* Compute nodes dedicated to allow access for those wanting to visualize results  
* Accessed through [Open On Demand](../portals/ood.md)  
* 24 hour walltime limit on visualization jobs


### Data Transfer Nodes

* Data Transfer Nodes (DTNs) are nodes which provide Globus [data transfer](./data-transfer.md) services at CCR
