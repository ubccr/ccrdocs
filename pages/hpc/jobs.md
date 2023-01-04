# Running Jobs

!!! todo

    write me

## Monitoring running Jobs

To view all the queued & running jobs submitted by your user account to any SLURM cluster:

    vortex1$ squeue -M all -u $LOGNAME
    CLUSTER: faculty
                 JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON)
              12747970 compbio  TM_P4269    myuser PD       0:00      1 (Priority)
              12743691 compbio  CF_Q6P0Q    myuser R  1-10:53:42      1 cpn-m22-35
    
    CLUSTER: ub-hpc
                 JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON)
              10736295 general-c SanDiaD-   myuser PD       0:00     80 (Resources)
              10737675 general-c parate     myuser R     3:10:23      8 cpn-h22-29,cpn-h23-[11-13,15-16,32,34]
    vortex1$ 

The "ST" column shows the job state - commonly this is either "PD" for a queued
job and "R" for a running job.



If you only use the default "up-hpc" cluser you can shorten this to:

    vortex1$ squeue -u $LOGNAME
    CLUSTER: ub-hpc
                 JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON)
              10736295 general-c SanDiaD-   myuser PD       0:00     80 (Resources)
              10737675 general-c parate     myuser R     3:10:23      8 cpn-h22-29,cpn-h23-[11-13,15-16,32,34]
    vortex1$

For only the "faculty" cluser jobs:

    vortex1$ squeue -M faculty -u $LOGNAME
    CLUSTER: faculty
                 JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON)
              12747970 compbio  TM_P4269    myuser PD       0:00      1 (Priority)
              12743691 compbio  CF_Q6P0Q    myuser R  1-10:53:42      1 cpn-m22-35
    vortex1$ 


To get futher info on the running job 10737675 in the default "ub-hpc" cluster:

    vortex1$ scontrol show job 10737675
    JobId=10737675 JobName=paratec
       UserId=myuser(123456) GroupId=myuser(123456) MCS_label=N/A
       Priority=196325 Nice=0 Account=mygroup QOS=general-compute
       JobState=RUNNING Reason=None Dependency=(null)
       Requeue=0 Restarts=0 BatchFlag=1 Reboot=0 ExitCode=0:0
       RunTime=03:27:07 TimeLimit=1-12:00:00 TimeMin=N/A
       SubmitTime=2022-12-29T09:52:56 EligibleTime=2022-12-29T09:52:56
       AccrueTime=2022-12-29T09:52:56
       StartTime=2022-12-29T10:49:34 EndTime=2022-12-30T22:49:34 Deadline=N/A
       PreemptEligibleTime=2022-12-29T10:49:34 PreemptTime=None
       SuspendTime=None SecsPreSuspend=0 LastSchedEval=2022-12-29T10:49:34 Scheduler=Backfill
       Partition=general-compute AllocNode:Sid=srv-p22-13:160705
       ReqNodeList=(null) ExcNodeList=(null)
       NodeList=cpn-h22-29,cpn-h23-[11-13,15-16,32,34]
       BatchHost=cpn-h22-29
       NumNodes=8 NumCPUs=320 NumTasks=320 CPUs/Task=1 ReqB:S:C:T=0:0:*:*
       TRES=cpu=320,mem=1496000M,node=8,billing=320
       Socks/Node=* NtasksPerN:B:S:C=40:0:*:* CoreSpec=*
       MinCPUsNode=40 MinMemoryNode=187000M MinTmpDiskNode=0
       Features=IB DelayBoot=00:00:00
       OverSubscribe=OK Contiguous=0 Licenses=(null) Network=(null)
       Command=/vscratch/grp-mygroup/paratec/WFN/job40
       WorkDir=/vscratch/grp-mygroup/paratec/WFN
       StdErr=/vscratch/grp-mygroup/paratec/WFN/slurm.out
       StdIn=/dev/null
       StdOut=/vscratch/grp-mygroup/paratec/WFN/slurm.out
       Power=
       MailUser=myuser MailType=END
    
    vortex1$ 


To get futher info on the queued job 12747970 in the "faculty" cluster:

    vortex1$ scontrol -M faculty show job 12747970
    JobId=12747970 JobName=CF_Q07283-F1_model1
       UserId=myuser(123456) GroupId=myuser(123456) MCS_label=N/A
       Priority=1006771 Nice=0 Account=mygroup QOS=compbio
       JobState=PENDING Reason=Priority Dependency=(null)
       Requeue=0 Restarts=0 BatchFlag=1 Reboot=0 ExitCode=0:0
       RunTime=00:00:00 TimeLimit=3-00:00:00 TimeMin=N/A
       SubmitTime=2022-12-29T10:45:36 EligibleTime=2022-12-29T10:45:36
       AccrueTime=2022-12-29T10:45:36
       StartTime=Unknown EndTime=Unknown Deadline=N/A
       SuspendTime=None SecsPreSuspend=0 LastSchedEval=2022-12-29T14:40:47 Scheduler=Main
       Partition=compbio AllocNode:Sid=cpn-m22-24:12178
       ReqNodeList=(null) ExcNodeList=(null)
       NodeList=(null)
       NumNodes=1-1 NumCPUs=1 NumTasks=1 CPUs/Task=1 ReqB:S:C:T=0:0:*:*
       TRES=cpu=1,mem=32000M,node=1,billing=1
       Socks/Node=* NtasksPerN:B:S:C=1:0:*:* CoreSpec=*
       MinCPUsNode=1 MinMemoryNode=32000M MinTmpDiskNode=0
       Features=(null) DelayBoot=00:00:00
       OverSubscribe=OK Contiguous=0 Licenses=(null) Network=(null)
       Command=/panasas/scratch/grp-mygroup/alphafold/CF_Q07283-F1_model1.pl
       WorkDir=/scratch/12747970/CH_Q07283-F1_model1
       StdErr=/panasas/scratch/grp-mygroup/alphafold/err_CF_Q07283-F1_model1
       StdIn=/dev/null
       StdOut=/panasas/scratch/grp-mygroup/alphafold/out_CF_Q07283-F1_model1
       Power=
       
    
    vortex1$ 

The SLURM schduler will try to estimate hte start time of the job - see "StartTime=" in the above output, however it is not always possible to estimate this, particularly if you have multiple queued jobs or there is a downtime scheduled soon and the requested job duration would overrun the start of the downtime.


## Troubleshooting completed and failed Jobs
