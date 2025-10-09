# Clusters

CCR maintains two clusters; *ub-hpc* and *faculty*. Within each cluster exist partitions (queues) that users can request to have their jobs run on. Not all partitions are available to all users. Below are descriptions of the clusters and the partitions. 

Compute nodes on all CCR clusters are subject to monthly downtimes. Downtime information can be found [here](https://ubccr.freshdesk.com/support/discussions/forums/5000296650)

Examples on how to run on these clusters and partitions can be found [here](https://docs.ccr.buffalo.edu/en/latest/hpc/jobs/).
 
## UB-HPC Compute Cluster

The ub-hpc cluster contains the following partitions:

* arm64: Compute nodes with ARM64 processors & specialized GPUs  
* class: Dedicated compute nodes for faculty teaching classes  
* debug: Dedicated compute nodes to help users debug their workflows  
* general-compute: Large pool of compute nodes for academic users  
* industry: Compute nodes industry partners pay to use  
* industry-dgx: NVIDIA DGX GPU compute nodes for industry partners (use qos `industry` to access)  
* industry-hbm: High-bandwidth memory nodes for industry partners (use qos `industry` to access)   
* scavenger: Preemptible jobs on all ub-hpc nodes  
* viz: Dedicated compute nodes to allow short jobs for visualization purposes  

Access to clusters and partitions is managed through allocations in the CCR allocations portal, ColdFront.  For more details on allocation requests and using ColdFront, see [here](../portals/coldfront.md).  


### UB-HPC Detailed Hardware Specifications  

This is a listing of available compute node types in the UB-HPC cluster.  Please keep in mind they are not all available to all users and are restricted using QOS values.  QOS access is given via allocations in ColdFront.  You can view what qos access you have using the `slimits` command.  Also note, the quantity of nodes in the following list is approximate as nodes fail and are removed from service often.

| Type of Node | Qty Nodes | Qty CPUs | Processor | GPU | RAM | Network | SLURM TAGS | Local scratch |  QOS |
| :-------- | :---------------- | :---------------- | :-------------- |  :---------------------------- |  :-------- |:-------- |:-------- |:-------- |:-------- |
| "Cascade Lake" Standard Node | 96 | 40 | Intel Xeon Gold 6230 | - | 187GB | Infiniband | CPU-Gold-6230, CASCADE-LAKE-IB | 880GB | debug, general-compute, scavenger |
| "Cascade Lake" Large Memory Node | 24 | 40 | Intel Xeon Gold 6230 | - | 754GB | Infiniband | CPU-Gold-6230, CASCADE-LAKE-IB, LM | 3.5TB | general-compute, scavenger |
| "Cascade Lake" GPU Node | 8 | 40 | Intel Xeon Gold 6230 | 2x V100 32GB (GPU memory) | 754GB | Infiniband | CPU-Gold-6230, CASCADE-LAKE-IB, V100 | 880GB |  general-compute, scavenger |
| "Cascade Lake" GPU Node | 1 | 48 | Intel Gold 6240R | 12x A16 15GB (GPU memory) | 512GB | Ethernet | Gold-6240R, A16 | 880GB |  general-compute, scavenger |
| "Ice Lake" Standard Node<sup>1<sup> | 67 | 56 | Intel Xeon Gold 6330 | - | 512GB | Infiniband | CPU-Gold-6330, ICE-LAKE-IB | 880GB |  industry, general-compute, scavenger |
| "Ice Lake" Large Memory Node<sup>1<sup> | 20 | 56 | Intel Xeon Gold 6330 | - | 1TB | Infiniband | CPU-Gold-6230, CASCADE-LAKE-IB, LM | 7TB | industry, general-compute, scavenger |
| "Ice Lake" GPU Node<sup>1<sup> | 20 | 56 | Intel Xeon Gold 6330 | 2x A100 40GB (GPU memory) | 512GB | Infiniband | CPU-Gold-6230, CASCADE-LAKE-IB, A100 | 880GB | industry, general-compute, scavenger |
| "Sapphire Rapids" Standard Node<sup>1<sup> | 81 | 64 | Intel Gold 6448Y | - | 512GB | Infiniband | CPU-Gold-6448Y, SAPPHIRE-RAPIDS-IB | 880GB | class, debug, industry, general-compute, scavenger |
| "Sapphire Rapids" Large Memory Node<sup>1<sup> | 4 | 64 | Intel Gold 6448Y | - | 2TB | Infiniband | CPU-Gold-6448Y, SAPPHIRE-RAPIDS-IB, LM | 7TB | industry, general-compute, scavenger |
| "Sapphire Rapids" GPU Node<sup>1<sup> | 8 | 64 | Intel Gold 6448Y | H100 80GB (GPU memory) | 512GB | Infiniband | CPU-Gold-6448Y, SAPPHIRE-RAPIDS-IB, H100 | 7TB | debug, industry, general-compute, scavenger, viz |
| "Emerald Rapids" Standard Node | 74 | 64 | Intel Platinum 8562Y+ | - | 512GB | HDR Infiniband | CPU-Platinum-8562Y, EMERALD-RAPIDS-IB | 880GB | class, industry, scavenger |
| "Emerald Rapids" Large Memory Node | 6 | 64 | Intel Platinum 8562Y+ | - | 2TB | HDR Infiniband | CPU-Platinum-8562Y, EMERALD-RAPIDS-IB, LM | 7TB | industry, scavenger |
| "Emerald Rapids" High Bandwidth Memory Node<sup>2<sup> | 8 | 64 | Intel Max 9462 | - | 125GB | HDR Infiniband | CPU-Max-9462, HBM | 833GB | industry-hbm |
| "Emerald Rapids" GPU Node | 10 | 64 | Intel Platinum 8562Y+ | 2x NVIDIA L40S 48GB (GPU memory) | 1TB | HDR Infiniband | CPU-Platinum-8562Y, L40S, EMERALD-RAPIDS-IB | 7TB | class, industry, scavenger |
| "Emerald Rapids" NVIDIA HGX GPU Node<sup>3<sup> | 2 | 96 | Intel Platinum 8468 |8x H100 85GB (GPU memory) | 512GB | HDR Infiniband | CPU-Platinum-8468, H100, EMERALD-RAPIDS-IB | 14TB | industry-dgx, eai-test, scavenger |
| "Grace Hopper" GPU Node<sup>4<sup> | 2 | 72 | ARM Neoverse-V2 | GH 200 | 490GB | Ethernet | CPU-Neoverse-V2 | 1.8TB | arm64 |
| Viz Node<sup>5<sup> | 1 | 48 | Intel Gold 6240R | 12x A16 15GB (GPU memory) | 512GB | Ethernet | Gold-6240R, A16 | 880GB | viz |
| Viz Node<sup>5<sup> | 2 | 64 | Intel Gold 6448Y | 2x A40 48GB (GPU memory) | 512GB | Ethernet | Gold-6448Y, A40 | 7TB | class, debug, viz |

[1]: These compute nodes are borrowed from the `industry` partition when usage is lower.  At times of higher industry usage, there will be fewer compute nodes available for the `general-compute` partition. 

[2]: The high bandwith memory nodes are available in the `industry-hbm` partition, available to all users with access to the `industry` qos.  These are not available in the `scavenger` partition to prevent issues with memory allocations in job.

[3]: The HGX GPU nodes are available in the `industry-dgx` partition, available to all users with access to the `industry` qos.  These are also available in the `scavenger` and `eai-test` partitions.

[4]: The Grace Hopper GPU nodes are available in the `arm64` partition and currently require a separate allocation in ColdFront.  Academic PIs may request an allocation following our [standard instructions](../portals/coldfront.md#request-an-allocation).

[5]: The visualization nodes are only available to access through OnDemand.  You may request the `viz` partition and QOS in the OnDemand app forms.  The `viz` partition has a maximum run time of 24 hours and is limited to 1 job per user (queued or running).



### UB-HPC Cluster Status  

Use the [Slurm dashboard](https://dashboard.ccr.buffalo.edu/slurm/ubhpc) for detailed information on current node status.  

## Faculty Compute Cluster

This cluster contains over 50 faculty owned or project specific partitions. Access to these partitions is determined by the owner and managed via allocations in [ColdFront](../portals/coldfront.md). All idle nodes in the faculty cluster are accessible to UB-HPC users in the scavenger partition.  Scavenger jobs will be [preemptively canceled](jobs.md#scavenging-idle-cycles) when jobs are submitted by members of the group that owns the node. To view hardware specifications for nodes in the faculty cluster, use the command:  `snodes all faculty/scavenger`     

!!! Warning "Caution: Maintenance Downtimes"  
    Jobs on the faculty cluster are allowed to run up until the downtime starts. Please ensure your jobs checkpoint and can restart where they left off OR request only enough time to run your job prior to the 7am cutoff on maintenance days.  See the [schedule here](../changelogs/2025-downtime-schedule.md)


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
* See detailed specs in [this list](#ub-hpc-detailed-hardware-specifications)  

### Debug Nodes

* Compute nodes reserved for testing and debugging jobs  
* Accessed by submitting a debug job in slurm  
* 1 hour walltime limit on debug jobs  
* See detailed specs in [this list](#ub-hpc-detailed-hardware-specifications)  

### Visualization Nodes

* Compute nodes dedicated to allow access for those wanting to visualize results  
* Accessed through [Open OnDemand](../portals/ood.md) 
* 24 hour walltime limit on visualization jobs   
* Select `viz` in the partition and qos drop down menus of the OnDemand apps  
* See detailed specs in [this list](#ub-hpc-detailed-hardware-specifications)  


### Data Transfer Nodes

* Data Transfer Nodes (DTNs) are nodes which provide Globus [data transfer](./data-transfer.md) services at CCR
