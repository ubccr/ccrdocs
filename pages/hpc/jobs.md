# Running Jobs

Our HPC system is shared among many researchers and CCR manages usage of the systems through jobs. Jobs are simply an allotment of resources that can be used to execute processes. CCR uses a program named Slurm, the Simple Linux Utility for Resource Management, to create and manage jobs.

In order to run a program on a cluster, you must request resources from Slurm to generate a job. Resources are requested from a login node. You then provide commands to run your program on those requested resources (compute nodes).


## Running applications with Jobs

There are two types of jobs, interactive and batch. Interactive jobs, allow you to type in commands while the job is running. Batch jobs are a self-containted set of commands in a script which is submitted to the cluster for execution on a compute node.

### Interactive Job Submission

Slurm interactive jobs allow users to interact with applications on the compute node. With an interactive job, you will request time and resources. Once available, you will be logged into the assigned node and the job will be ended when you log out or your reqested time limit is reached.  This is different compared to a batch job where you submit your job for execution with no user interaction.  

**Example Interactive Job**

To submit an interactive job to the general-compute partition for a single node with 32 Intel cores and 50GB of memory for 5 hours and 20 minutes, use the salloc command and the appropriate options as shown here:  

```
salloc --qos=general-compute --partition=general-compute  --job-name "InteractiveJob" --nodes=1 --ntasks=32 --mem=50G -C INTEL --time=05:20:00
```

To complete/end this job, we would type `exit` on the command line.

### Batch Job Submission

Batch jobs are the most common type of job on HPC systems. Batch jobs are resource provisions that run applications on compute nodes and do not require supervision or interaction. Batch jobs are commonly used for applications that run for long periods of time and require no manual user input.

**Example Job Scripts**

Below is an explanation of the SBATCH options used in our samples. These are Slurm directives and should be understood before submitting a job.  For more information on Slurm directives, partitions, and QOS, [see here](#slurm-directives-partitions-qos).

```
#!/bin/sh
#
# 	How long the job will run once it begins. If the job runs longer than what is
# 	defined here, it will be cancelled by Slurm.
# 	If you make the expected time too long, it will
# 	take longer for the job to start.
# 	Format:	dd:hh:mm:ss

#SBATCH --time=00:01:00

#	Define how many nodes you need. We ask for 1 node

#SBATCH --nodes=1

# 	You can define the number of tasks with --ntasks-per-node

#SBATCH --ntasks-per-node=1

# 	How much memory do you need.
# 	This will define memory (in MB) this job requires.

#SBATCH --mem=10000

# 	Give your job a name, so you can recognize it in the queue

#SBATCH --job-name="example-debug-job"

# 	Tell slurm the name of the file to write to

#SBATCH --output=example-debug-job.out

# 	Tell slurm where to send emails about this job

#SBATCH --mail-user=myemailaddress@institution.edu

# 	Tell slurm the types of emails to send.
# 	Options: NONE, BEGIN, END, FAIL, ALL

#SBATCH --mail-type=end

# 	Tell Slurm which cluster, partition and qos to use to schedule this job.

#SBATCH --partition=debug
#SBATCH --qos=debug
#SBATCH --cluster=ub-hpc

```

Below are several sample scripts which can be submitted to Slurm using the `sbatch` command. Batch scripts should be submitted to from a login node and the commands within the script will be excuted on a compute node.  We use some of the Slurm directives as described above.

To submit to the **debug partition on the ub-hpc cluster**, the slurm script would look like:

```
#!/bin/sh
#
#SBATCH --time=00:01:00
#SBATCH --nodes=1
#SBATCH --ntasks-per-node=1
#SBATCH --mem=10000
#SBATCH --job-name="example-debug-job"
#SBATCH --output=example-debug-job.out
#SBATCH --mail-user=myemailaddress@institution.edu
#SBATCH --mail-type=end
#SBATCH --partition=debug
#SBATCH --qos=debug
#SBATCH --cluster=ub-hpc

#Let's start some work
echo "Hello world from debug node: "`/usr/bin/uname -n`
#Let's finish some work
```

To submit to the **general-compute partition on the ub-hpc cluster**, the slurm script would look like:

```
#!/bin/sh
#
#SBATCH --time=00:01:00
#SBATCH --nodes=1
#SBATCH --ntasks-per-node=1
#SBATCH --mem=10000
#SBATCH --job-name="example-general-compute-job"
#SBATCH --output=example-general-compute-job.out
#SBATCH --mail-user=myemailaddress@institution.edu
#SBATCH --mail-type=end
#SBATCH --partition=general-compute
#SBATCH --qos=general-compute
#SBATCH --cluster=ub-hpc

#Let's start some work
echo "Hello world from general-compute node: "`/usr/bin/uname -n`
#Let's finish some work

```

To submit to the privately owned **ub-laser partition on the faculty cluster**, the slurm script would look like:
```
#!/bin/sh
#
#SBATCH --time=00:01:00
#SBATCH --nodes=1
#SBATCH --ntasks-per-node=1
#SBATCH --mem=10000
#SBATCH --job-name="example-faculty-cluster-job"
#SBATCH --output=example-faculty-cluster-job.out
#SBATCH --mail-user=myemailaddress@institution.edu
#SBATCH --mail-type=end
#SBATCH --partition=ub-laser
#SBATCH --qos=ub-laser
#SBATCH --cluster=faculty

#Let's start some work
echo "Hello world from faculty cluster node: "`/usr/bin/uname -n`
#Let's finish some work

```

!!! Note "Caution: Maintenance Downtimes"
    Jobs on the faculty cluster are allowed to run up until the downtime starts. Please ensure your jobs checkpoint and can restart where they left off OR request only enough time to run your job prior to the 7am cutoff on maintenance days.  See the [schedule here](https://ubccr.freshdesk.com/support/discussions/forums/5000296650)

To submit to the **scavenger partition on the ub-hpc cluster**, the slurm script would look like:

```
#!/bin/sh
#
#SBATCH --time=00:01:00
#SBATCH --nodes=1
#SBATCH --ntasks-per-node=1
#SBATCH --mem=10000
#SBATCH --job-name="example-general-compute-scavenger-job"
#SBATCH --output=example-general-compute-scavenger-job.out
#SBATCH --mail-user=myemailaddress@institution.edu
#SBATCH --mail-type=end
#SBATCH --partition=scavenger
#SBATCH --qos=scavenger
#SBATCH --cluster=ub-hpc

#Let's start some work
echo "Hello world from ub-hpc cluster scavenger node: "`/usr/bin/uname -n`
#Let's finish some work

```

[Learn more](#scavenging-idle-cycles) about scavenging idle cycles.  

### Job Arrays  

A job array is a group of nearly identical jobs submitted with 1 SLURM script.  Use the `--array=<indexes>` Slurm directive within your batch script.  See the [Slurm documentation](https://slurm.schedmd.com/job_array.html) for more information    

This example submits 16 jobs:  
```
#SBATCH <array flag>
--array=1-16
```

This example submits 16 jobs, with a limit of 4 jobs running simultaneously:  
```
#SBATCH --array=0-15%4
```

**Job Array Job Number:**  `%A` - job array master job ID

**Job Array Index Number:** `%a` - individual job index number  

## Useful Slurm Commands

#### sbatch

To submit a batch script to Slurm for processing:

````
sbatch slurm.script
````
For more information, [visit the Slurm docs on sbatch](https://slurm.schedmd.com/sbatch.html)

#### squeue

To see all of your jobs across all CCR clusters:
````
squeue -M all -u $LOGNAME
````
For more information, [visit the Slurm docs on squeue](https://slurm.schedmd.com/squeue.html)

#### scancel
To cancel a job you have submitted:
````
scancel <job_id>
````
For more information, [visit the Slurm docs on scancel](https://slurm.schedmd.com/scancel.html)

!!! Tip "Slurm Default Cluster"
    Slurm commands default to the UB-HPC cluster.  To specify the faculty cluster use either the `-M faculty` or `--clusters=faculty` option.  

For additional Slurm commands, [visit the Slurm command manual](https://slurm.schedmd.com/quickstart.html)

## Slurm Directives, Partitions & QoS

Slurm allows the use of flags to specify resources needed for a job. Below is a table describing some of the most common Slurm resource flags, followed by tables describing available partitions and Quality of Service (QoS) options.

| Type               | Description                                         | Flag                       |
| :----------------- | :-------------------------------------------------- | :------------------------- |
| Clusters          | Specify a cluster (ub-hpc or faculty) | --clusters=cluster |
| Partition          | Specify a partition | --partition=partition |
| Quality of service | Specify a QoS (usually same as partition or priority boost) | --qos=qos               |
| Sending email      | Receive email at beginning or end of job completion | --mail-type=type           |
| Email address      | Email address to receive the email                  | --mail-user=user           |
| Number of nodes    | The number of nodes needed to run the job           | --nodes=nodes              |
| Number of tasks    | The ***total*** number of processes needed to run the job | --ntasks=processes   |
| Tasks per node     | The number of processes you wish to assign to each node | --ntasks-per-node=processes |
| Total memory       | The total memory (per node requested) required for the job. <br> Using --mem does not alter the number of cores allocated <br> to the job, but you will be charged for the number of cores <br> corresponding to the proportion of total memory requested. <br> Units of --mem can be specified with the suffixes: K,M,G,T (default M)| --mem=memory |

| Wall time          | The max amount of time your job will run for        | --time=wall time           |
| Job Name           | Name your job so you can identify it in the queue   | --job-name=jobname         |

These are the partitions available on the UB-HPC cluster:

| Partition | Default Wall Time | Wall Time Limit | Default # CPUS | Job Submission Limit/User     |
| :-------- | :---------------- | :-------------- | :------------- | :---------------------------- |
| debug     | 1 hour            | 1 hour          | 1              |   4        |
| general-compute     | 24 hour            | 72 hour          | 1              |   1000        |
| industry     | 24 hour            | 72 hour          | 1              |   1000        |
| scavenger     | 24 hour            | 72 hour          | 1              |   1000        |
| viz     | 24 hour            | 24 hour          | 1              |   1        |

**Faculty Cluster Partitions**   
There are over 50 partitions in the faculty cluster all have with a default of 1 CPU, default wall time of 24 hours and a maximum number of jobs per user of 1000.  The maximum wall time of these partitions range from 72 hours to 30 days.  To view details about a particular partition use the `scontrol` command, for example:  `scontrol show partition ub-laser -M faculty`

**Priority Boosts**  
Supporters of CCR are provided access to the `supporters` QOS which provides a bump in priority to all jobs run by the group.  To find out how to qualify for this boost, please [visit our website](https://www.buffalo.edu/ccr/support/ccr-help/accounts.html#boost).  PIs that were part of the 2019 NIH S10 award and the 2017 NSF MRI award that helped to purchase new equipment are also granted priority boosts for their group.  These allocations have been added to your ColdFront project and are active for a period of 5 years.  The allocations can not be renewed.  Group members should utilize the `mri` or `nih` QOS values to take advantage of the priority boost.  NOTE:  All of these QOS values are only available on the UB-HPC cluster.

## Job Priority  

Factors that Determine Job Priority:  
:  **Age** - the amount of time the job has been waiting in the queue  
:  **Job Size** - number of nodes requested by the job  
:  **Partition** - priority for a given partition  
:  **Fairshare** - priority contribution based on compute resources used by members in a research group within the last 30 days. The more jobs that have run on the cluster the lower the priority.  The fewer number of jobs that have run the higher the priority.  
:  **Quality of Service (QOS)** - supporters of CCR are given a priority boost for their group's jobs.  [Find out how to become a CCR supporter](https://www.buffalo.edu/ccr/support/ccr-help/accounts.html#boost)  
:  **TRES** -  Each TRES Type has its own priority factor for a job, which represents the amount of TRES Type requested/allocated in a given partition. The more a given TRES Type is requested/allocated on a job, the greater the job priority will be for that job.  CCR weights memory and GPU requests and provides a slightly higher priority for these to allow for proper scheduling of our heterogenous nodes.  

See the Slurm documentation for more details about [SLURM Multifactor Priority Calculations](https://slurm.schedmd.com/priority_multifactor.html) and [Fairshare](https://slurm.schedmd.com/priority_multifactor.html#fairshare)

**Job Priority Formula:**  
```
Job_priority =
(PriorityWeightAge) * (age_factor) +
(PriorityWeightFairshare) * (fair-share_factor) +
(PriorityWeightJobSize) * (job_size_factor) +
(PriorityWeightPartition) * (partition_factor) +
(PriorityWeightQOS) * (QOS_factor)
```

**Weights assigned to Priority Factors for UB-HPC cluster:**  
```
PriorityWeightAge       = 50000
PriorityWeightAssoc     = 0
PriorityWeightFairShare = 80000
PriorityWeightJobSize   = 200000
PriorityWeightPartition = 1000000
PriorityWeightQOS       = 50000
PriorityWeightTRES      = CPU=0,Mem=.01,GRES/gpu=30000
```

**To View Fairshare:**  
```
sshare <flag>  
--accounts=group_name  
--all --accounts=group_name  (Shows fairshare for members of the group)  
```

**Show Job Priority:**  
```
sprio <flag>
-j jobid
-u username
```

**To show Job Priority sorted from highest to lowest:**  Use the `sranks` command  


## Monitoring Jobs

### Active Jobs monitoring via OnDemand
CCR offers a detailed view into what is happening on the node(s) where your job is running.  You can view the graphs from OnDemand but you do NOT need to submit the jobs from within OnDemand.  Even jobs submitted from the command line using 'sbatch' are available in your list of Active Jobs.

In OnDemand, click on the arrow next to one of your current jobs and at the bottom you will see two graphs for each node your job is running on.  One graph shows CPU metrics and the other memory (RAM) usage.


### Grafana Charts

You can access Grafana charts of your completed jobs, like the Active Jobs available in OnDemand, but you need to query Slurm for the appropriate start and end times and get the node list.  To do this, we provide a script that can be run in the terminal that creates the Grafana URL for your job. 

````
[ccruser@vortex]$/util/common/metrics/ccr-jobview-url [jobid] [cluster]


[ccruser@vortex]$ /util/common/metrics/ccr-jobview-url 10457965 ub-hpc
````

Then you would paste the outputed link into your browser. For example:

[Click here for example Grafana output](https://dashboard.ccr.buffalo.edu/grafana/d/Vi3oi5gohz/hpc-job-metrics?orgId=1&theme=light&from=1669820527000&to=1669820600000&var-cluster=ub-hpc&var-host=cpn-k08-34-01&var-jobid=10457965)

### Slurm Accounting
Slurm account information is also available and useful depending on what information you're looking for regarding your jobs.  

**Show job account information for a specific job:**  
If the job is currently running, you will get node information.  If it has completed, you will not. 
````
sacct -j jobid --format=User,JobID,Jobname,partition,state,time,start,end,elapsed,nnodes,ncpus,nodelist
````
or `slist jobid`  

**Show all job information starting from a specific date for a specific user:**   
````
sacct -S start-date -u username
````


### Metrics OnDemand
For metrics about job performance and node usage after your job completes, please use the [UBMoD portal](https://ubmod.ccr.buffalo.edu/). Job data is usually available 24 hours after a job completes. [More details about UBMod.](../portals/metrics.md)  

## Scavenging Idle Cycles  

In an effort to maximize the use of all available cores within our center, we provide access to all compute nodes whenever they are idle.  This means that academic UB-HPC users will have access to idle nodes on the industry partition as well as nodes in the faculty cluster.  These idle nodes are available through the scavenger partitions on the UB-HPC and faculty clusters and jobs are allowed to run on them when there are no other pending jobs scheduled for them.  Once a user with access to the partition submits a job requesting resources, jobs in the scavenger partition are stopped and re-queued.  This means if you're running a job in the scavenger partition on the industry cluster and an industry user submits a job requiring the resources you're consuming, your job will be stopped.  

*  **Requirements for using the scavenger partitions:**  
    * Your jobs MUST be able to checkpoint otherwise you'll lose any work when your jobs are stopped and re-queued.    
    * You must be an advanced user that understands the queuing system, runs efficient jobs, and can get checkpointing working on your jobs independently.  CCR staff can not devote the time to helping you write your code.  
    * If your jobs are determined to cause problems on any of the private cluster nodes and we receive complaints from the owners of those nodes, your access to the scavenger partitions will be removed.  
