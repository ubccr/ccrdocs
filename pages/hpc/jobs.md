# Running Jobs

Our HPC system is shared among many researchers and CCR manages usage of the
systems through jobs. Jobs are simply an allotment of resources that can be
used to execute processes. CCR uses a program named Slurm, the Simple Linux
Utility for Resource Management, to create and manage jobs.

In order to run a program on a cluster, you must request resources from Slurm
to generate a job. Resources are requested from a login node. You then provide
commands to run your program on those requested resources (compute nodes).  

Watch this virtual workshop to learn more about batch computing at CCR:  
![type:video](https://youtube.com/embed/ZU2sQ5MnN0Y)  

## Requesting cores and nodes

When running jobs with Slurm, you must be explicit about requesting CPU cores
and nodes. The three options `--nodes or -N`, `--ntasks or -n`, and
`--cpus-per-task or -c` can be a bit confusing at first but are necessary to
understand when running applications that use more than one CPU.

!!! Tip
    If your application references threads or cores but makes no mention of MPI,
    only use `--cpus-per-task` to request CPUs. You cannot request more cores than
    there are on a single compute node where your job runs.  You still need
    to tell your application to utilize these cores, but you can use the Slurm
    environment variable \$SLURM_CPUS_PER_TASK, e.g., for OpenMP codes:
    ```bash
    export OMP_NUM_THREADS=$SLURM_CPUS_PER_TASK
    ```

Using these options will depend on the type of parallelism you are using, i.e.
distributed or shared memory. Here's some simple guidelines to follow:

- `--ntasks=#`: Number of "tasks" (use with distributed parallelism).

- `--ntasks-per-node=#`: Number of "tasks" per node (use with distributed parallelism).

- `--cpus-per-task=#`: Number of CPUs allocated to each task (use with shared memory parallelism).

If an application is able to use multiple cores, it usually achieves this by
either spawning threads and sharing memory (multi-threaded) or starting entire
new processes (multi-process). In this case use `--cpus-per-task` to guarantee
that the CPUs you expect your program to use are all accessible.

For example, suppose you need 16 cores, here are some possible scenarios:

- you want one process that can use 16 cores for multithreading: `--ntasks=1 --cpus-per-task=16`
- you want 4 processes that can use 4 cores each for multithreading: `--ntasks=4 --cpus-per-task=4`
- you use mpi and do not care about where those cores are distributed: `--ntasks=16`
- you want to launch 16 independent processes (no communication): `--ntasks=16`
- you want 16 cores to spread across distinct nodes: `--ntasks=16 --ntasks-per-node=1 or --ntasks=16 --nodes=16`
- you want 16 cores to spread across distinct nodes and no interference from other jobs: `--ntasks=16 --nodes=16 --exclusive`
- you want 16 processes to spread across 8 nodes to have two processes per node: `--ntasks=16 --ntasks-per-node=2`
- you want 16 processes to stay on the same node: `--ntasks=16 --ntasks-per-node=16`

## MPI

Some applications are written to use the Message Passing Interface (MPI)
standard to run across many compute nodes. These applications can scale
computation in a way not limited by the number of cores on a single node. MPI
applications can leverage high speed network transports such as InfiniBand to
increase performance. If you're running MPI applications it's important to
understand the various network topologies available and how to request the
nodes most appropriate for your specific job.

CCR's network topology consists of a core Ethernet network where all nodes are
fully connected. A subset of nodes also support InfiniBand and are grouped into
three disjointed InfiniBand networks (islands): 

| IB Network             | Nodes   | Speed              |
| ---------------------- | ------- | ------------------ |
| **CASCADE-LAKE-IB**    | 128     | HDR 100G           |
| **ICE-LAKE-IB**        |   99     | HDR 100G           |
| **SAPPHIRE-RAPIDS-IB** |   85     | NDR 200G           |
| **EMERALD-RAPIDS-IB**  |   48     | NDR 200G           |

If you plan on running a multi-node MPI job which leverages InfiniBand you must
run on exactly ONE of the above fabrics. The easiest way to do this is to add
the following constraint to your job:

```
#SBATCH --constraint="[SAPPHIRE-RAPIDS-IB|ICE-LAKE-IB|CASCADE-LAKE-IB|EMERALD-RAPIDS-IB]"
```

The above will ensure your job runs on a set of nodes in exactly one of the
above InfiniBand networks. You can also request a specific InfiniBand fabric:

```
#SBATCH --constraint="CASCADE-LAKE-IB"
```

By default, Slurm schedules jobs based on CCR's hierarchical Ethernet network
topology using leaf switches and a best-fit algorithm. Because ALL compute
nodes are connected to the Ethernet network but only a subset support
InfiniBand, if you don't specify the above constraint it's possible your job
could be placed on nodes in different disconnected InfiniBand networks
resulting in the nodes being unable to communicate.

!!! Warning
    Use of the `--constraint=IB` is now deprecated because this only ensures
    your job runs on nodes supporting InfiniBand, however your job still could
    be placed on a set of nodes spanning disjointed InfiniBand networks
    resulting in communication failure. The `--constraint=IB` will be removed
    in the future.

MPI translates what Slurm calls tasks to separate workers or processes. For
control over how Slurm lays out your job, you can add the `--nodes` and
`--ntasks-per-node` flags. Note that the following must be true:

```
ntasks-per-node * nodes >= ntasks
```

!!! Tip
    For Intel MPI (part of the `intel` toolchain, the `foss` toolchain instead uses OpenMPI), it is 
    necessary in a Slurm job to set the environment variable \$I_MPI_PMI_LIBRARY to the right Slurm library:
    ```bash
    export I_MPI_PMI_LIBRARY=/opt/software/slurm/lib64/libpmi.so
    ``` 

In some cases, MPI programs are also multi-threaded, so each process can use
multiple CPUs. Only these applications can use `--ntasks` and `--cpus-per-task`
to run faster.

## Running applications with Jobs

There are two types of jobs, interactive and batch. Interactive jobs, allow you
to type in commands while the job is running. Batch jobs are a self-contained
set of commands in a script which is submitted to the cluster for execution on
a compute node.

### Interactive Job Submission

Slurm interactive jobs allow users to interact with applications on the compute
node. With an interactive job, you will request time and resources. Once
available, you will be able to log into the assigned node and the job will be ended
when you log out and cancel it or your requested time limit is reached.  This is different
compared to a batch job where you submit your job for execution with no user
interaction.  

!!! Note "Job Environment Propogation"  
    Because CCR's clusters contain a mix of CPU architectures for which environments may
    differ, we recommend you utilize the `--no-shell` option when requesting interactive
    jobs.  Then use the `srun` command to login to the allocated node.   

This example requests an interactive job using the `salloc` command on the general-compute partition for 1 node, a single
process with 32 cores and 50GB of memory for 1 hour.  Once the requested node is available, use the `srun` command as shown
to login to the compute node:    

```
$ salloc \
   --partition=general-compute \
   --qos=general-compute \
   --mem=50G \
   --nodes=1 \
   --time=1:00:00 \
   --ntasks-per-node=1 \
   --cpus-per-task=32 \
   --no-shell
# above command will output the jobid
$ srun --jobid=JOBID_HERE --export=HOME,TERM,SHELL --pty /bin/bash --login
```  
Once you're done with the node, use the `exit` or `logout` command and then release your job's allocated resources using the command `scancel $JOBID` If you don't cancel the job, Slurm will release the allocated resources when the time requested for the job expires and you'll be automatically logged out of the compute node.  

### Batch Job Submission

Batch jobs are the most common type of job on HPC systems. Batch jobs are
resource provisions that run applications on compute nodes and do not require
supervision or interaction. Batch jobs are commonly used for applications that
run for long periods of time and require no manual user input.

Below is an explanation of the SBATCH options used in our samples. These are
called "Slurm directives" and should be understood before submitting a job.  For more
information on clusters, partitions, and QOS options, see [here](#slurm-directives-partitions-qos).

```
#!/bin/bash -l

# 	Tell Slurm which cluster, partition and qos to use to schedule this job

#SBATCH --cluster=cluster-name
#SBATCH --partition=partition-name
#SBATCH --qos=qos-name

# 	Tell Slurm which account to run this job under 
#   If not specified, your default account will be used  
#   Use the `slimits` command to see what accounts you have access to

#SBATCH --account=SlurmAccountName  

# 	How long the job will run once it begins. If the job runs longer than what is
# 	defined here, it will be cancelled by Slurm.
# 	If you make the expected time too long, it will
# 	take longer for the job to start.
# 	Format:	dd:hh:mm:ss

#SBATCH --time=00:01:00

#	Define how many nodes you need. We ask for 1 node

#SBATCH --nodes=1

# 	You can define the number of Cores with --cpus-per-task

#SBATCH --cpus-per-task=32

# 	Specify the real memory required per node.  Default units are megabytes.  
#   Different units can be specified using the suffix  [K|M|G|T]  

#SBATCH --mem=20G

# 	Give your job a name, so you can recognize it in the queue

#SBATCH --job-name="example-debug-job"

# 	Tell slurm the name of the file to write to

#SBATCH --output=example-debug-job.out

# 	Tell slurm where to send emails about this job

#SBATCH --mail-user=myemailaddress@institution.edu

# 	Tell slurm the types of emails to send.
# 	Options: NONE, BEGIN, END, FAIL, ALL  

#SBATCH --mail-type=end


```

!!! Warning "Using Slurm's Email Directive"  
    Please be cautious using the email directive and specifying which types of emails you'd like to receive.  Normally, receiving an email at the end of a job is more than sufficient.  If you're running many very short jobs, please do not use this at all as this looks like a spam attack to the receiving email server and CCR's email servers get blocked.  



Below are several sample scripts which can be submitted to Slurm using the
`sbatch` command. Batch scripts should be submitted from a login node and
the commands within the script will be executed on a compute node.  We use some
of the Slurm directives as described above.

To submit to the **debug partition on the ub-hpc cluster**, the slurm script would look like:

```bash
#!/bin/bash -l
#
#SBATCH --cluster=ub-hpc
#SBATCH --partition=debug
#SBATCH --qos=debug
#SBATCH --time=00:01:00
#SBATCH --ntasks-per-node=1
#SBATCH --job-name="example-debug-job"
#SBATCH --output=example-debug-job.out
#SBATCH --mail-user=myemailaddress@institution.edu
#SBATCH --mail-type=end


#Let's start some work
echo "Hello world from debug node: "`/usr/bin/uname -n`
#Let's finish some work
```

To submit to the **general-compute partition on the ub-hpc cluster**, the slurm
script would look like:

```bash
#!/bin/bash -l
#
#SBATCH --cluster=ub-hpc
#SBATCH --partition=general-compute
#SBATCH --qos=general-compute
#SBATCH --time=00:01:00
#SBATCH --nodes=1
#SBATCH --ntasks-per-node=1
#SBATCH --mem=10G
#SBATCH --job-name="example-general-compute-job"
#SBATCH --output=example-general-compute-job.out
#SBATCH --mail-user=myemailaddress@institution.edu
#SBATCH --mail-type=end

#Let's start some work
echo "Hello world from general-compute node: "`/usr/bin/uname -n`
#Let's finish some work

```

To submit to the privately owned **ub-laser partition on the faculty cluster**,
the slurm script would look like:

```bash
#!/bin/bash -l
#
#SBATCH --cluster=faculty
#SBATCH --partition=ub-laser
#SBATCH --qos=ub-laser
#SBATCH --time=00:01:00
#SBATCH --nodes=1
#SBATCH --ntasks-per-node=1
#SBATCH --mem=10G
#SBATCH --job-name="example-faculty-cluster-job"
#SBATCH --output=example-faculty-cluster-job.out
#SBATCH --mail-user=myemailaddress@institution.edu
#SBATCH --mail-type=end

#Let's start some work
echo "Hello world from faculty cluster node: "`/usr/bin/uname -n`
#Let's finish some work

```

!!! Warning "Caution: Maintenance Downtimes"
    Jobs on the faculty cluster are allowed to run up until the downtime
    starts. Please ensure your jobs checkpoint and can restart where they left
    off OR request only enough time to run your job prior to the 7am cutoff on
    maintenance days.  See the [schedule
    here](https://ubccr.freshdesk.com/support/discussions/forums/5000296650)

To submit to the **scavenger partition on the ub-hpc cluster**, the slurm
script would look like:

```bash
#!/bin/bash -l
#
#SBATCH --cluster=ub-hpc
#SBATCH --partition=scavenger
#SBATCH --qos=scavenger
#SBATCH --time=00:01:00
#SBATCH --nodes=1
#SBATCH --ntasks-per-node=1
#SBATCH --mem=10G
#SBATCH --job-name="example-general-compute-scavenger-job"
#SBATCH --output=example-general-compute-scavenger-job.out
#SBATCH --mail-user=myemailaddress@institution.edu
#SBATCH --mail-type=end

#Let's start some work
echo "Hello world from ub-hpc cluster scavenger node: "`/usr/bin/uname -n`
#Let's finish some work

```

[Learn more](#scavenging-idle-cycles) about scavenging idle cycles.  

### Job Arrays  

A job array is a group of nearly identical jobs submitted with 1 SLURM script.
Use the `--array=<indexes>` Slurm directive within your batch script.  See the
[Slurm documentation](https://slurm.schedmd.com/job_array.html) for more
information    

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
| Account    | Specify which Slurm account you'd like to run the job under.  Use `slimits` to see your account(s).  If not specified, your default Slurm account will be used | --account=SlurmAccountName               |
| Sending email      | Receive email at beginning or end of job completion | --mail-type=type           |
| Email address      | Email address to receive the email                  | --mail-user=user           |
| Number of nodes    | The number of nodes needed to run the job           | --nodes=nodes              |
| Number of tasks    | The ***total*** number of processes needed to run the job | --ntasks=processes   |
| Tasks per node     | The number of processes you wish to assign to each node | --ntasks-per-node=processes |
| Total memory       | The total memory (per node requested) required for the job. <br> Using --mem does not alter the number of cores allocated <br> to the job, but you will be charged for the number of cores <br> corresponding to the proportion of total memory requested. <br> Units of --mem can be specified with the suffixes: K,M,G,T (default M)| --mem=memory |
| GPU requests         | Requesting the GPU on a node, requesting specific features<br> of the V100 GPUs, or requesting a specific slot of the GPU(S:0-1) <br> To specify type of GPU (A40, A100, H100, V100) use [--constraints](#node-features) <br>To use all cores on a node w/more than 1 GPU you <br>must [disable CPU binding](https://docs.ccr.buffalo.edu/en/latest/faq/#how-do-i-request-all-cpus-on-a-node-with-more-than-one-gpu)     | --gpus-per-node=1 (or gpu:2) <br>  --gpus-per-node=tesla_v100-pcie-32gb:1 <br> --gpus-per-node=tesla_v100-pcie-16gb:1 <br> --gpus-per-node=tesla_v100-pcie-16gb:1(S:0) or (S:1) <br>--gres-flags=disable-binding      |
| Wall time          | The max amount of time your job will run for        | --time=wall time           |
| Job Name           | Name your job so you can identify it in the queue   | --job-name=jobname         |


**UB-HPC cluster partitions, defaults, and limits:**  

| Partition | Valid QOS options | Default Wall Time | Wall Time Limit |  Job Submission Limit/User     |
| :-------- | :---------------- | :---------------- | :-------------- |  :---------------------------- |
| arm64     | arm64 | 24 hours            | 72 hours          |    4        |
| class     | class | 24 hours            | 72 hours          |    4        |
| debug     | debug, supporters | 1 hour            | 1 hour          |    4        |
| general-compute     | general-compute, supporters, nih, nihsupporters | 24 hours            | 72 hours          |    1000        |
| industry     | industry | 24 hours            | 72 hours          |    1000        |
| industry-dgx     | industry | 24 hours            | 72 hours          |    10        |
| industry-hbm     | industry | 24 hours            | 72 hours          |    10        |
| scavenger     | scavenger | 24 hours            | 72 hours          |    1000       |
| viz     | Only accessible through OnDemand | 24 hours            | 24 hours          |    1        |

**Additional Default Values**  
All UB-HPC partitions have a default of 1 CPU per job and a default RAM (memory) value of 2800mb (2.8GB).  If you require more, these will need to be specified in your resource request.  

**Faculty Cluster Partitions**   
There are over 50 partitions in the faculty cluster all of which have a default of 1 CPU, wall time of 24 hours and a maximum number of jobs per user of 1000.  The maximum wall time of these partitions ranges from 72 hours to 30 days.  To view details about a particular partition use the `scontrol` command; for example:  `scontrol show partition ub-laser -M faculty`

**Priority Boosts**  
Supporters of CCR are provided access to the `supporters` QOS which provides a bump in priority to all jobs run by the group.  To find out how to qualify for this boost, please [visit our website](https://www.buffalo.edu/ccr/support/ccr-help/accounts.html#boost).  PIs that were part of the 2019 NIH S10 award that helped to purchase new equipment were granted priority boosts for their group that lasted 5 years.  These allocations were added to your ColdFront project and expired on February 1, 2025.  At this time, any faculty with current NIH funding may apply for the NIH priority boost. This will be available until the hardware is retired.  Please enter your NIH grant information in your ColdFront project and request an allocation for the NIH priority boost.  Once the allocation is activated, your group members should utilize the `nih` QOS value to take advantage of the priority boost.  Those faculty that have active NIH funding and are current CCR supporters will have access to the `nihsupport` QOS value.  NOTE:  These QOS values are only available on the UB-HPC cluster.

**Other Limits**  
Some Slurm accounts have limitations on them.  For example, accounts associated with courses will have a limit of 1 GPU per job.  The Intro to CCR UB Learns course does not require the use of GPUs; therefore, the `introccr` Slurm account has a limit of 0 GPUs.  Jobs using this account to request GPUs will be blocked in the queue.  [See here](../faq.md#why-am-i-seeing-the-job-status-assocmaxgresperjob-on-my-pending-job) for further information.

## Node Features    

Users do not need to specify much information if they do not care where their job runs or on what hardware.  Slurm uses the default information from your account, the cluster, and the partition to run a job.  If you need more than the default, you can specify hardware requirements using the Slurm `--constraint` directive in a batch script or using the `Node Features` field in OnDemand app forms.  You can specify CPU type such as `INTEL` or `AMD` or more specific CPU models such as `CPU-Gold-6230`.  GPU types can be specified with `A40`, `A100`, `H100`, `GH200`, or `V100`.  [High speed interconnect](#mpi) networks can be also be requested.  Additional node features include machine room rack locations and funding sources (i.e. NIH and MRI).  To specify more than one feature, use the `&` sign between them (i.e. `--constraint=INTEL&ICE-LAKE-IB` will request nodes with Intel CPUs and the ICE-LAKE-IB Infiniband high speed network).  To request a node with one feature or another, use the `|` symbol between them (i.e. `--constraint=CPU-Gold-6330|CPU-Gold-6230` will request nodes with either the Intel 6230 or 6330 CPU, but not a node with the 6130 CPU).  

!!! Tip  
    The less you specify, the sooner your job is likely to run because you are not narrowing your pool of compute nodes to run on with specific criteria.  

The best way to see all the Slurm features offered and what is currently available, is by running the `snodes` command in the terminal on one of the cluster login servers.   

```` 
CCRusername@login:~$ snodes --help
==============================================================
Display information about one or more nodes, possibly filtered
by partition and/or state.

If no node arg or 'all' is provided, all nodes will be
summarized. Similar behavior exists for the partition and
state(s) args

Usage:   snodes [node1,node2,etc.] [cluster/partition] [state(s)]

==============================================================
CCRusername@login:~$ snodes all ub-hpc/general-compute |grep gpu
cpn-h22-29    mix      56   2:28:1   48/8/0/56       3.10     512000   gpu:a100-pcie-40gb:2                general-compute*   INDUSTRY,AVX512,CPU-Gold-6330,INTEL,h22,IB,A100
cpn-h22-31    mix      56   2:28:1   48/8/0/56       3.06     512000   gpu:a100-pcie-40gb:2                general-compute*   INDUSTRY,AVX512,CPU-Gold-6330,INTEL,h22,IB,A100
cpn-h22-33    mix      56   2:28:1   48/8/0/56       2.99     512000   gpu:a100-pcie-40gb:2                general-compute*   INDUSTRY,AVX512,CPU-Gold-6330,INTEL,h22,IB,A100

CCRusername@login:~$ snodes all ub-hpc/industry |grep IB
cpn-h22-04    alloc    56   2:28:1   56/0/0/56       56.16    1000000  (null)                              industry           INDUSTRY,AVX512,CPU-Gold-6330,INTEL,h22,IB
cpn-h22-05    alloc    56   2:28:1   56/0/0/56       56.18    1000000  (null)                              industry           INDUSTRY,AVX512,CPU-Gold-6330,INTEL,h22,IB
cpn-h22-06    mix      56   2:28:1   48/8/0/56       168.08   1000000  

CCRusername@login:~$ snodes all faculty/scavenger |grep idle
cpn-f11-03    idle     24   2:12:1   0/24/0/24       0.01     256000   (null)                              scavenger          FACULTY,AVX2,CPU-E5-2650v4,INTEL
cpn-f11-04    idle     24   2:12:1   0/24/0/24       0.02     256000   (null)                              scavenger          FACULTY,AVX2,CPU-E5-2650v4,INTEL
cpn-f11-05    idle     24   2:12:1   0/24/0/24       0.05     256000   (null)                              scavenger          FACULTY,AVX2,CPU-E5-2650v4,INTEL

````
The format of the Slurm features (last column) in snodes command output is:  `CLUSTER, CPU_ARCHITECTURE, CPU_MODEL, CPU_MANUFACTURER, RACK,[FUNDING SOURCE, INTERCONNECT, GPU_MODEL]`  Anything in `[ ]` is optional and may be dependent on what hardware is in the node. 

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
--all --accounts=[YourSlurmAccount]  (Shows fairshare for members of the group)  
```

!!! Tip "Slurm Account Name"  
    Slurm account names are listed on your allocations for cluster resources in [ColdFront](https://coldfront.ccr.buffalo.edu) or you can view on the command line using the `slimits` command.     

**Show Job Priority:**  
```
sprio <flag>
-j jobid
-u [CCRusername]
```

**To show Job Priority sorted from highest to lowest:**  Use the `sranks` command  


## Monitoring Jobs

Watch this virtual workshop to learn more about monitoring your jobs:  
![type:video](https://youtube.com/embed/ZsXnoH2UQ4E)  

### Active Jobs Monitoring - command line  
If your job is currently running, you can login to the compute node(s) it's running on to inspect your program's progress, view output logs, and investigate the node's system status.  You will only be able to login to a compute node where you have a running job.  For instructions on how to login, please see [here](login.md#compute-node-logins). Once on the compute node, you may use Linux commands to view system status such has `top`, `htop`, `cat /proc/meminfo` (for system memory/RAM information), and `cat /proc/cpuinfo` (for system processor/CPU information).  To view currently running processes under your account use `ps -ef|grep [CCRusername]` (replace [CCRusername] with your CCR username and no brackets). To cancel or kill a process running under your account use `kill -9 [pid]` (replace [pid] with the process ID).  When you're done, use the `exit` or `logout` command.  For more info on Linux commands, see the [CCR Linux & Slurm Cheatsheet]().


### Active Jobs monitoring - OnDemand
CCR offers a detailed view into what is happening on the node(s) where your job is running.  You can view the graphs from OnDemand but you do NOT need to submit the jobs from within OnDemand.  Even jobs submitted from the command line using 'sbatch' are available in your list of Active Jobs.

In OnDemand, click on the arrow next to one of your current jobs and at the bottom you will see two graphs for each node your job is running on.  One graph shows CPU metrics and the other memory (RAM) usage.


### Grafana Charts

You can access Grafana charts of your completed jobs, like the Active Jobs available in OnDemand, but you need to query Slurm for the appropriate start and end times and get the node list.  To do this, we provide a script that can be run in the terminal that creates the Grafana URL for your job. 

````
CCRusername@login:~$ ccr-jobview-url [jobid] [cluster]


CCRusername@login:~$ ccr-jobview-url 10457965 ub-hpc
````

Then you would paste the outputed link into your browser. For example:

[Click here for example Grafana output](https://dashboard.ccr.buffalo.edu/grafana/d/Vi3oi5gohz/hpc-job-metrics?orgId=1&theme=light&from=1669820527000&to=1669820600000&var-cluster=ub-hpc&var-host=cpn-k08-34-01&var-jobid=10457965)

### Slurm Accounting
Slurm account information is also available and useful depending on what information you're looking for regarding your jobs.  

**Show job account information for a specific job:**  
If the job is currently running, you will get node information.  If it has completed, you will not. 
````
sacct -j jobid --format=User,JobID,Jobname,partition,state,time,start,end,elapsed,nnodes,ncpus,nodelist,ReqMem
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
