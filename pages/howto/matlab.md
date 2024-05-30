# MATLAB on the CCR Clusters

UB has a sitewide academic license for MATLAB along with all the toolboxes and CCR provides a few versions of MATLAB on our HPC clusters.

==MATLAB use is restricted to UB faculty, staff, and students only!  External collaborators, RPCI users, and industry customers are not permitted to access UB's MATLAB license==  

There are a few different methods for running MATLAB on CCR HPC clusters and the method you choose depends on the type of MATLAB calculations you wish to run. This guide will focus on the main methods in which users should run MATLAB at CCR.
These methods include:

- Running MATLAB GUI through Open OnDemand
- Running MATLAB batch jobs on the Clusters through Slurm
- Running MATLAB interactively on the command line
- Using MATLAB Parallel Compute Server to submit jobs from within Matlab

This guide does not give information on using MATLAB itself; it is assumed that the audience is already familiar with using it. If you are looking for specific MATLAB related info their documentation is located [here](https://www.mathworks.com/help/matlab/).

## Versions of MATLAB available at CCR

Software is updated regularly at CCR so users need to know how to search the existing software repositories to find the available versions of software they're interested in running. In the MATLAB OnDemand app, the form provides a drop down menu listing the available versions of MATLAB. For those using the command line, you can search using the module spider command. First, specify a [software release](https://github.com/ubccr/ccrdocs/software/releases) version and then search for MATLAB:

```
module load ccrsoft/2023.01
module spider matlab

matlab:
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
     Versions:
        matlab/2021b
        matlab/2023b
```


## Running MATLAB GUI though OpenOndemand 

The easiest way to use MATLAB on the HPC clusters is through the [CCR OnDemand Portal](../portals/ood.md). This method provides a more interactive use of MATLAB but requires a hands on approach. If you are looking for something more automated and scripted [see below](#running-matlab-batch-jobs-on-the-clusters-through-slurm)

To begin a session, click on the "Interactive Apps" menu and then on the "Matlab GUI" menu option.  Select from the form's drop down menus the cluster you'd like to submit this job to, the partition & associated QOS, and your Slurm account.  By default, MATLAB sessions are allocated 1 CPU, 2.8GB of RAM and 24 hours wall time (run time). You can override the defaults by changing the form values; however, unless you are sure that your script has been explicitly parallelized using, for example, the [Parallel Computing Toolbox](#running-a-multi-threaded-matlab-job-with-the-parallel-computing-toolbox), leave the "Number of cores" set to 1.  To choose a specific version of MATLAB to run, select from the "MATLAB version" drop down menu.  Once the form is filled out, click the "Launch" button.  When your session starts, click the "Launch Matlab GUI" button. NOTE: the more resources you request, the longer you may have to wait for your session to be scheduled on a compute node.



## Running MATLAB interactively on the command line

You can run MATLAB interactively from the command line either by submitting an [interactive job](../hpc/jobs.md/#interactive-job-submission) through Slurm and logging in to the allocated compute node or
if you need to use MATLAB to edit and test your script you can run it on one of the CCR login nodes.  
 **NOTE:** The login nodes are a shared resource and have resource limits in place so once you hit one of the limits, your session will be terminated. This use case is only for quick testing or verification that requires very little resources and time.

!!! Warning "X11 Forwarding"
    CCR does not allow X Windows forwarding on our Compute nodes or Login nodes so the graphical MATLAB is not available with these methods.  You must use OnDemand to access the MATLAB GUI.  

### Running MATLAB using an interactive job

Here is an example of how to submit an interactive job to run MATLAB from the command line.  NOTE:  this example uses the `general-compute` partition of the `ub-hpc` cluster.  Please refer to our [Slurm documentation](../hpc/jobs.md) for more options.  
```
$ salloc --qos=general-compute --partition=general-compute --job-name "Interactive_Matlab" --cpus-per-task=1 --ntasks=1 --time=01:00:00
salloc: Pending job allocation 15395595
salloc: job 15395595 queued and waiting for resources
salloc: job 15395595 has been allocated resources
salloc: Granted job allocation 15395595
salloc: Waiting for resource configuration
salloc: Nodes cpn-i15-04 are ready for job
$ module load matlab/2023b
$ matlab -singleCompThread -nodisplay -nosplash
Opening log file:  /tmp/java.log.7975

                                                                                                           < M A T L A B (R) >
                                                                                                 Copyright 1984-2023 The MathWorks, Inc.
                                                                                            R2023b Update 4 (23.2.0.2428915) 64-bit (glnxa64)
                                                                                                             October 23, 2023
To get started, type doc.
For product information, visit www.mathworks.com.
 
>> fprintf('Hello world.\n')
Hello world.
```


## Running MATLAB batch jobs on the Clusters through Slurm

### Running a Serial MATLAB Job

A serial MATLAB job is one that requires only a single CPU-core. Here is an example of a trivial, one-line serial MATLAB program (`hello_world.m`):

```
cat hello_world.m
fprintf('Hello world.\n')
```
NOTE:  When you're done, make sure to quit MATLAB and then type `exit` to log out of the compute node and properly release the resources for other users.  
This is an example Slurm script (`matlab-sp.sh`) that can be modified to run a serial MATLAB job.  NOTE:  this example uses the `general-compute` partition of the `ub-hpc` cluster.  Please refer to our [Slurm documentation](../hpc/jobs.md) for more options.  

```
#!/bin/bash -l
#SBATCH --job-name=matlab        		# create a short name for your job
#SBATCH --qos=general-compute			# qos job will run under 
#SBATCH --partition=general-compute		# partition to run on 
#SBATCH --nodes=1                		# node count
#SBATCH --ntasks=1               		# total number of tasks across all nodes
#SBATCH --cpus-per-task=1        		# cpu-cores per task (>1 if multi-threaded tasks)
#SBATCH --mem-per-cpu=4G         		# memory per cpu-core (4G per cpu-core is default)
#SBATCH --time=00:01:00          		# total run time limit (HH:MM:SS)
#SBATCH --mail-type=all          		# send email on job start, end and fault
#SBATCH --mail-user=UBITusername@buffalo.edu 	# valid email for Slurm to send notifications

module load matlab/2023b

matlab -singleCompThread -nodisplay -nosplash -r hello_world
```

By invoking MATLAB with **-singleCompThread -nodisplay -nosplash**, the GUI is suppressed as is the creation of multiple threads. To run the MATLAB script, simply submit the job to the scheduler from a login node with the following command:

```
$ sbatch matlab-sp.sh
Submitted batch job 15390684
```

After the job completes, you can find the job's output in a file named with the job ID - for example:  `slurm-<jobid>.out`

```
$ cat slurm-15390684.out
Opening log file:  /tmp/java.log.24391

                            < M A T L A B (R) >
                  Copyright 1984-2023 The MathWorks, Inc.
             R2023b Update 4 (23.2.0.2428915) 64-bit (glnxa64)
                              October 23, 2023

 
To get started, type doc.
For product information, visit www.mathworks.com.
 
Hello world.
```

### Running a Multi-threaded MATLAB Job with the Parallel Computing Toolbox

Most of the time, running MATLAB in single-threaded mode (as described above) will meet your needs. However, if your code makes use of the Parallel Computing Toolbox (e.g., parfor) or you have intense computations that can benefit from the built-in multi-threading provided by MATLAB's BLAS implementation, then you can run in multi-threaded mode. One can use up to all the CPU-cores on a single node in this mode. 

For multi-node jobs you will need to use the [MATLAB Parallel Server](#running-multi-node-jobs-using-matlab-parallel-server).  You should always use `#SBATCH --nodes=1` for multi-threaded and serial calculations.


Here is an [example](https://www.mathworks.com/help/parallel-computing/interactively-run-a-loop-in-parallel.html) from MathWorks of using multiple cores (`for_loop.m`):

```
poolobj = parpool;
fprintf('Number of workers: %g\n', poolobj.NumWorkers);

tic
n = 200;
A = 500;
a = zeros(n);
parfor i = 1:n
    a(i) = max(abs(eig(rand(A))));
end
toc
```

This is an example Slurm script (`matlab-mp.sh`) that can be modified to run a single node, multi-threaded MATLAB job.  NOTE:  this example uses the `general-compute` partition of the `ub-hpc` cluster.  Please refer to our [Slurm documentation](../hpc/jobs.md) for more options.

```
#!/bin/bash -l
#SBATCH --job-name=matlab-mp                    # create a short name for your job
#SBATCH --qos=general-compute                   # qos job will run under 
#SBATCH --partition=general-compute             # partition to run on 
#SBATCH --nodes=1                               # node count
#SBATCH --ntasks=1                              # total number of tasks across all nodes
#SBATCH --cpus-per-task=4                       # cpu-cores per task (>1 if multi-threaded tasks)
#SBATCH --mem-per-cpu=4G                        # memory per cpu-core (4G per cpu-core is default)
#SBATCH --time=00:01:00                         # total run time limit (HH:MM:SS)
#SBATCH --mail-type=all                         # send email on job start, end and fault
#SBATCH --mail-user=UBITusername@buffalo.edu      # valid email for Slurm to send notifications

module load matlab/2023b

matlab -nodisplay -nosplash -r for_loop
```

```
$ sbatch matlab-mp.sh
Submitted batch job 15391013
```

```
$ cat slurm-15391013.out
Opening log file:  /tmp/java.log.47411

                            < M A T L A B (R) >
                  Copyright 1984-2023 The MathWorks, Inc.
             R2023b Update 4 (23.2.0.2428915) 64-bit (glnxa64)
                              October 23, 2023

 
To get started, type doc.
For product information, visit www.mathworks.com.
 
Starting parallel pool (parpool) using the 'Processes' profile ...
Connected to parallel pool with 4 workers.
Elapsed time is 31.030224 seconds.
Parallel pool using the 'Processes' profile is shutting down.
```

Note that **-singleCompThread** does not appear in the Slurm script in contrast to the serial case. One must tune the value of **--cpus-per-task** for optimum performance. Use the smallest value that gives you a significant performance boost because the more resources you request the longer your queue time may be.

By default MATLAB will restrict you to 12 worker threads. You can override this when making the parallel pool with the following line, for example, with 24 threads:

```
poolobj = parpool('local', 24);
```

!!! Note
    If you use more than one thread then make sure that your code can take advantage of all the CPU-cores. The amount of time that a job waits in the queue is proportional to the requested resources. Furthermore, your fairshare value is decreased in proportion to the requested resources. So if you are requesting the resources for a parallel execution and your code is not designed to take advantage of it, then you are wasting CPU cycles that other users can utilize as well as unnecessarily inflating your fairshare score and lowering your job priority.


## Running MATLAB on GPUs

MATLAB has support for running on GPUs. If you have a routine that requires the use of or can take advantage of a GPU, here is an example of how to get access to a GPU.


Below is a MATLAB script (`svd_matlab.m`) that performs a matrix decomposition using a GPU:

```
gpu = gpuDevice();
fprintf('Using a %s GPU.\n', gpu.Name);
disp(gpuDevice);

X = gpuArray([1 0 2; -1 5 0; 0 3 -9]);
whos X;
[U,S,V] = svd(X)
fprintf('trace(S): %f\n', trace(S))
quit;
```

With the corresponding slurm script (`matlab-gpu.sh`)

```
#!/bin/bash -l
#SBATCH --job-name=matlab-gpu           # create a short name for your job
#SBATCH --qos=general-compute           # qos job will run under 
#SBATCH --partition=general-compute     # partition to run on 
#SBATCH --nodes=1                       # node count
#SBATCH --ntasks=1                      # total number of tasks across all nodes
#SBATCH --cpus-per-task=1               # cpu-cores per task (>1 if multi-threaded tasks)
#SBATCH --mem-per-cpu=4G                # memory per cpu-core (4G per cpu-core is default)
#SBATCH --gpus-per-node=1             	# number of gpus per node
#SBATCH --time=00:01:00                 # total run time limit (HH:MM:SS)
#SBATCH --mail-type=all                 # send email on job start, end and fault
#SBATCH --mail-user=UBITusername@buffalo.edu  # valid email for Slurm to send notifications

module load matlab/2023b

matlab -singleCompThread -nodisplay -nosplash -r svd_matlab
```

In the above Slurm script, notice the new line: **#SBATCH --gpus-per-node=1**
This tells slurm to request a node with 1 GPU. See [here](../hpc/jobs.md#slurm-directives-partitions-qos) for additional Slurm directives, including how to request a specific GPU type.

For interactive MATLAB jobs as described [above](#unning-matlab-interactively-on-the-command-line), a GPU can be requested the same way.  For example, add this to your `salloc` command to request 1 GPU:  `--gpus-per-node=1`

## Running Multi-node jobs using MATLAB Parallel Server

MATLAB Parallel Server lets you scale MATLAB programs to use multiple nodes in clusters. MATLAB Parallel Server supports batch jobs, interactive parallel computations, and distributed computations with large matrices. MATLAB Parallel Server runs your programs by submitting jobs to CCR's Slurm scheduler. 


### Configuring Slurm Integration on CCR MATLAB (Command Line)

In order to use MATLAB Parallel Server you need to create a Cluster Profile.  The easiest way to do this is to log onto the CCR login nodes, start MATLAB and then run the MATLAB `configCluster` command: 

```
$ module load matlab/2023b
$ matlab -singleCompThread -nodisplay -nosplash
Opening log file:  /tmp/java.log.54427

                                                                                                           < M A T L A B (R) >
                                                                                                 Copyright 1984-2023 The MathWorks, Inc.
                                                                                            R2023b Update 4 (23.2.0.2428915) 64-bit (glnxa64)
                                                                                                             October 23, 2023

 
To get started, type doc.
Foe product information, visit www.mathworks.com.
 
>> configCluster
Complete.  Default cluster profile set to "ub-hpc".
>> 
```

This loads the default Slurm values to create an initial Cluster Profile called `ub-hpc`.

Once you have the default profile, you will want to customize the configuration with specfic user values such as user email for example.

This is accomplished right within MATLAB.

- Get a handle to the cluster
```
>> c = parcluster;
```
- Display current properties
```
>> c.AdditionalProperties

ans = 

  AdditionalProperties with properties:

             AccountName: ''
    AdditionalSubmitArgs: ''
                Clusters: 'ub-hpc'
              Constraint: ''
            EmailAddress: ''
             EnableDebug: 0
                 GPUCard: ''
             GPUsPerNode: 0
               MemPerCPU: '8gb'
               Partition: 'general-compute'
            ProcsPerNode: 0
        QualityOfService: 'general-compute'
    RequireExclusiveNode: 0
             Reservation: ''
                WallTime: ''

>> 
```
- Change user Email Address
```
>> c.AdditionalProperties.EmailAddress = 'UBITusername@buffalo.edu';
```
- Save the changes
```
>> c.saveProfile
```

This should be enough to submit a test job to CCR's HPC Clusters from MATLAB. You can create multiple Cluster Profiles with different settings so you don't have to always modify the default.

### Submitting a test Job from MATLAB to CCR Clusters

Here is an example parallel MATLAB job that is submitted to CCR's HPC Clusters:

Let’s use the following example for a parallel job, which is saved as (`parallel_example.m`)

```
function [sim_t, A] = parallel_example(iter)
 
if nargin==0
    iter = 8;
end
 
disp('Start sim')
 
t0 = tic;
parfor idx = 1:iter
    A(idx) = idx;
    pause(2)
    idx
end
sim_t = toc(t0);
 
disp('Sim completed')
 
save RESULTS A
 
end
```

From MATLAB:

```
>> c = parcluster;

>> job = c.batch(@parallel_example, 1, {16}, 'Pool',4,'CurrentFolder','.');    

additionalSubmitArgs =

    '--ntasks=5 --cpus-per-task=1 --ntasks-per-core=1 --mem-per-cpu=8gb --qos=general-compute --clusters ub-hpc -p general-compute --mail-type=ALL --mail-user=UBITusername@buffalo.edu'
```

You can check the Slurm job state from within MATLAB:
```
>> job.State

ans =

    'queued'

>> 

```
After the job is completed the state will be Finished and you can check the output:

```
>> job.State

ans =

    'finished'

>> job.fetchOutputs{:}

ans =

    8.4850

>> 

```

The job ran in 8.485 seconds using four workers.  **Note** that these jobs will always request N+1 CPU cores, since one worker is required to manage the batch job and pool of workers. 
For example, a job that needs eight workers will request nine CPU cores.

### Configuring Slurm Integration on CCR MATLAB (GUI)

Configuring the Slurm integration using the MATLAB GUI is pretty straight forward. 

- Start up MATLAB through an OnDemand session as described [here](#running-matlab-gui-though-openondemand)

- From the MATLAB Session Click on `Parallel` -> `Discover Clusters`

- Leave the check box in the `On your Network` and click `Next`

- Highlight the default `ub-hpc` cluster and click `Finish`

![](../images/matlab2.png)

You now have a default Cluster Profile that should work out of the box, but you will want to change some of the default settings such as user email settings.

To make changes to the default Cluster Profile:


- From the MATLAB Session Click on `Parallel` -> `Create and Manage Clusters`

- Click on the ub-hpc Cluster Profile and Click `Edit`

- Make your changes and click `Done`


### Configuring Remote Slurm Integration (GUI)

It is possible to configure your local MATLAB to submit jobs to CCR from your desktop or workstation. The setup is very similar to [Configuring Slurm Integration on CCR MATLAB](#configuring-slurm-integration-on-ccr-matlab-command-line) once you have the correct integration scripts.


NOTE: This procedure assumes that you have MATLAB R2023b (Currently the only supported version at CCR) installed on your local machine.

!!! Warning "SSH Key Credentials"
    Submission to the cluster requires SSH credentials.  You will be prompted for username and password or identity file (private key).  The username and location of the private key will be stored in MATLAB for future sessions.


You will need to download the MATLAB CCR Slurm integration script and place them on your local machine in the MATLAB

Download the [CCR Matlab Integration Scripts](https://g-ac407a.8c185.08cc.data.globus.org/R2023b/University-at-Buffalo.zip) and start MATLAB.  The ZIP file should be unzipped in the location returned by calling…

```
>> userpath

ans =

    '/home/[username]/Documents/MATLAB'

>> 

```
**NOTE:** This is on your local computer so the directory path will most likely be different.

Configure your local MATLAB to run parallel jobs on the cluster by using the `configCluster` cluster command.  This only needs to be run once per version of MATLAB.


```
>> configCluster
Username on UB-HPC (e.g. jdoe): >>[CCRusername]
Complete.  Default cluster profile set to "ub-hpc R2023b".
>> 

```
You will need to configure your user infomation into the Profile including the location to your private SSH key stored on your computer:

```
>> c = parcluster;
>> c.AdditionalProperties.EmailAddress = 'UBITusername@buffalo.edu'
>> c.AdditionalProperties.IdentityFile = '/home/username/.ssh/private.key'
```

**NOTE:** We recommend setting the RemoteJobStorageLocation to your group's project directory, if you have one, rather than your home directory to prevent going over quota in your home directory.  

```
c.AdditionalProperties.RemoteJobStorageLocation = '/projects/academic/[YourGroupName]/[CCRusername]/Software/MATLAB/Jobs'
```

Save the changes to the profile:

```
>> c.saveProfile
```

Submit a Parallel Test Job:

```
>> job = c.batch(@parallel_example, 1, {16}, 'Pool',4,'AutoAddClientPath',false,'CurrentFolder','.');

additionalSubmitArgs =

    '--ntasks=5 --cpus-per-task=1 --ntasks-per-core=1 --mem-per-cpu=8gb --qos=general-compute --clusters ub-hpc -p general-compute --mail-type=ALL --mail-user=UBITusername@buffalo.edu'

>> job.State                                                                                         

ans =

    'finished'

>> job.fetchOutputs{:}                                                                               

ans =

    8.6260

>> 
```

More information on MATLAB Parallel Computing can be found here: [MATLAB Parallel Computing Toolbox](https://www.mathworks.com/help/parallel-computing/)


