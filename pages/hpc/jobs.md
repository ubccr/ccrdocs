# Running Jobs

Our HPC systems are shared among many researchers and CCR manages usage of the systems through jobs. Jobs are simply an allotment of resources that can be used to execute processes. CCR uses a program named Slurm, the Simple Linux Utility for Resource Management, to create and manage jobs.

In order to run a program on a cluster, you must request resources from Slurm to generate a job. Resources are requested from a login node. You must then provide commands to run your program on those requested resources.


## Running applications with Jobs

There are two types of jobs, interactive jobs and batch jobs. Interactive jobs, allow you to type in commands while the job is running. Batch jobs are a self-containted set of commands in a script which is submitted to the cluster for execution on a compute node. 

### Interactive Job Submission

Slurm interactive jobs allow users to interact with applications on the compute node. With an interactive job, you will request time and resources. Once available, you will be logged into the assigned node and the job will be ended when you log out or your reqested time limit is reached.  This is different compared to a batch job where you submit your job for execution with no user interaction.  


**Example Interactive Job**

To submit an interactive job to the general-compute partition for a single node with 32 Intel cores and has 50G of memory for 5 hours and 20 minutes, we would specify the general-compute QoS in the command below. We would then wait until a node with the resources we requested becomes available. Once it is available, we would automatically be logged into this node and we can freely complete our work.

```
salloc --qos=general-compute --partition=general-compute  --job-name "InteractiveJob" --nodes=1 --ntasks=32 --mem=50G -C INTEL --time=05:20:00
```

To complete/end this job, we would type `exit` on the command line. 

## Batch Job Submission

Batch jobs are the most common type of job on HPC systems. Batch jobs are resource provisions that run applications on compute nodes and do not require supervision or interaction. Batch jobs are commonly used for applications that run for long periods of time and require no user interaction.

##### Example Job Scripts

Below are sample script which can be sbatch'd to Slurm to run on a compute node.

Below is explanation of of the SBATCH options used in our samples. These are Slurm directives and should be understood before submitting a job.

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
# 	This will define memory this job requires. 

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

# 	Tell Slurm which cluster,partition and qos schedule this job.

#SBATCH --partition=debug
#SBATCH --qos=debug
#SBATCH --cluster=ub-hpc

```


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

To submit to the privately owned **ezurek partition on the faculty cluster**, the slurm script would look like:
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
#SBATCH --partition=ezurek
#SBATCH --qos=ezurek
#SBATCH --cluster=faculty

#Let's start some work
echo "Hello world from faculty cluster node: "`/usr/bin/uname -n`
#Let's finish some work

```
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

## Useful Slurm Commands

#### sbatch

To submit a batch script to Slurm for processing:

````
sbatch job.slurm.script
```` 
For more information, [visit the Slurm docs on sbatch](https://slurm.schedmd.com/sbatch.html)

#### squeue

To see all of your jobs in across all CCR clusters:
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

For additional Slurm commands, [visit the Slurm command manual](https://slurm.schedmd.com/quickstart.html)

## Slurm <sbatch> Job Flags
 
The `sbatch` command supports many optional flags. To review all the options, please visit the Slurm [sbatch page](http://slurm.schedmd.com/sbatch.html). Below are useful flags: 

| Type                   | Description                                         | Flag                       |
| :--------------------- | :-------------------------------------------------- | :------------------------- |
| Partitions         | Specify a partition                                 | --partition=partition_name |
| Sending email          | Receive email at beginning or end of job completion | --mail-type=type           |
| Email address          | Email address to receive the email                  | --mail-user=user           |
| Number of nodes        | The number of nodes needed to run the job           | --nodes=nodes              |
| Number of tasks        | The total number of cores needed to run the job     | --ntasks=processes         |
| Quality of service | Specify a QOS                                       | --qos=qos                  |
| Wall time              | The max. amount of time your job will run for       | --time=wall time           |
| Job Name               | Name your job so you can identify in queue          | --job-name=<jobname>       |




## Slurm Directives, Partitions & QoS

Slurm allows the use of flags to specify resources needed for a job. Below is a table describing some of the most common Slurm resource flags, followed by tables describing available partitions and Quality of Service (QoS) options.

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
Slurm account information is also available and useful depending on what information you're looking for regarding your jobs.  We provide some suggested commands [here](https://ubccr.freshdesk.com/support/solutions/articles/5000686909-how-to-retrieve-job-history-and-accounting).

### Metrics OnDemand
For metrics about job performance and node usage after your job completes, please use the [UBMoD portal](https://ubmod.ccr.buffalo.edu/). Job data is usually available 24 hours after a job completes. [More details about UBMod.](https://ubccr.freshdesk.com/support/solutions/folders/13000014875)



