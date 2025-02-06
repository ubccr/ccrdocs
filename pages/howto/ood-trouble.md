# OnDemand Troubleshooting  

When you're using OnDemand for your computing, you're running jobs on the CCR clusters.  Though OnDemand makes this task simple with a few clicks in the browser, it's important to understand how to monitor your jobs, how to find your output files, and how to troubleshoot issues that may come up.  Here are the top questions we get by users of OnDemand at CCR:  

## How to Monitor OnDemand Sessions  

Use the OnDemand `Active Jobs` app to see your queued and running jobs.  [More info here](../portals/ood.md#jobs-apps).  Since the OnDemand sessions are the same as jobs submitted through the batch scheduler, [this info](../hpc/jobs.md#monitoring-jobs) for monitoring jobs is also useful.  

## Why is my session not starting?  

OnDemand sessions are submitted as jobs to CCR's clusters.  The Slurm scheduler schedules jobs on compute nodes based on the resources requested.  Basically, your OnDemand session is in line with all the other batch jobs and OnDemand sessions submitted by all the other users of CCR.  If you are asking for resources that are in high demand, you will need to wait.  Overall, most jobs start within a few hours of being submitted to CCR's clusters.  However, some resources such as GPU nodes are limited in quantity and almost always under high demand.  This means you could wait many hours, days or potentially a week for your job to get scheduled.  Please [see here](../hpc/jobs.md#job-priority) for more info on job priority and [here for more](../faq.md#when-will-my-job-start) on how to tell when your job will start.  If your job is pending for a specific reason other than `resources` or `priority`, refer to these sections in our FAQ:  
[`reqnodenotavail` status](../faq.md#why-is-my-job-pending-with-reason-reqnodenotavail)  
[`qosmaxsubmitjobperuserlimit` status](../faq.md#why-am-i-getting-a-qosmaxsubmitjobperuserlimit-error-when-i-try-to-submit-a-job)  
[`AssocMaxGRESPerJob` status](../faq.md#why-am-i-seeing-the-job-status-assocmaxgresperjob-on-my-pending-job)  

## Why does my OnDemand desktop or app show it's starting but then it immediately ends?  

There are three common reasons why you might not be able to launch OnDemand sessions including interactive desktops and apps like Jupyter Notebook and Matlab.  

1. You are [over quota](../hpc/storage.md#checking-quotas) in your home directory.  See more on managing [OnDemand job data](../portals/ood.md#my-interactive-sessions)  
2. You have not requested enough memory for the job to run.  If not specified, a job will be allocated 2.8GB of RAM (memory).  This is enough for some basic jobs, including launching OnDemand interactive desktops.  This will not be enough for most interactive apps (Jupyter, Matlab, RStudio) or for more intense workloads in desktop sessions.  We can't tell you how much RAM your program will need.  We recommend starting low with 4 or 6GB of RAM and [monitoring your job](../hpc/jobs.md#monitoring-jobs) to determine whether it's getting used. NOTE: the OnDemand forms ask for memory to be specified in megabytes, not gigabytes.  So if you want to request 4GB of RAM, please enter 4000 in the form field.
2. The application is looking for a software module to load and can't find it. For OnDemand desktop and apps specifically, this problem might be introduced by you having a `module load` statement in your `~/.bashrc` file or if you are using a [CCR software environment](../software/releases.md) that does not contain the module the app is trying to start. [See here](../faq.md#why-am-im-getting-module-not-found-errors) for more info.  
3. You have an Anaconda environment loading in your `~/.bashrc` environment file or are loading a Python module in your `~/.bashrc` file that is interfering with the OnDemand desktop setup.  Some users load Anaconda environments or personal/group Python or Anaconda modules in their `~/.bashrc` file (found in your home directory).  These environments break OnDemand desktops and apps and prevent them from starting.  To fix this, use the OnDemand Files app to navigate to your home directory.  Click the `Show Dotfiles` checkbox, find and open the `.bashrc` file for editing.  Remove everything in this file between the two `>>> conda initialize >>>` lines.  Then save the file and close the Files app.  Click on the Help menu and choose "Restart Web Server" to refresh your OnDemand process.  Do NOT delete the `~/.bashrc` file!  Anaconda is not recommended for HPC systems and is no longer supported on CCR's systems for [these reasons](../software/modules.md#anaconda-python). Please refrain from using this software and if you need help finding an alternative for your workflow, contact [CCR Help](../help.md) for recommendations.   

## Where can I find the output files for my OnDemand sessions?  

The easiest way to find these is by clicking on the `Session ID` link on the job card as this will open the Files app and take you directly to the output directory for that job.  If the session card has been deleted, you can find all your OnDemand output files in your home directory, in sub-directories of `/user/[CCRusername]/ondemand/data/sys/dashboard/batch_connect/sys`  In each job directory, you will find, at minimum, an `output.log` file.  Though this file will contain what appears to be errors, much of this can be ignored until the end of the file.  If the job ends prematurely, you will often see the reason why it failed.  The three most frequent reasons:  
- Out of memory: You might see an error like `Detected 1 oom-kill event(s) in StepId=999999.batch. Some of your processes may have been killed by the cgroup out-of-memory handler` - Solution: Request more memory  
- Time limit reached:  You might see an error like `CANCELLED AT 2024-02-20T03:24:08 DUE TO TIME LIMIT` - Solution: Request more time.  [See here](../hpc/jobs.md#slurm-directives-partitions--qos) for more info on cluster limits.  
- Out of disk space:  You might see errors like `no space left on device` or `I/O error` - Solution: Clear up space in your home directory to allow more room for OnDemand output files.  [See here](../faq.md#why-am-i-getting-no-space-left-on-device-errors) for more info

## Understanding OnDemand Session Details  

If you submit a CCR help ticket using the OnDemand "Submit Support Ticket" feature on the job card, you will have access to detailed job session information.  To view the help ticket, login to [CCR's Help Desk Portal](https://ubccr.freshdesk.com) and view your ticket.  Not sure of your login credentials?  [See here](../help.md#sign-up-for-ccr-help-portal).  In the ticket content you'll see `Interactive Session Information` which will list out lots of job details.  You may find out for yourself what the problem with your job was.  For example, first is listed information about the OnDemand app used and the selections you made or entered on the app form:  

```
Interactive Session Information:
{
"id": "73b7bde3-232a-4433-a3d3-4934ca914c99",
"clusterId": "ub-hpc",
"jobId": "5033962",
"createdAt": "2024-02-26T14:29:20-05:00",
"token": "sys/jupyter_adv",
"title": "Jupyter Lab/Notebook Advanced Options",
"user_context": {
"jupyterlab_switch": "0",
"modules": "gcc/11.2.0 openmpi/4.1.1 pytorch/1.13.1-CUDA-11.8.0 torchvision/0.14.1-CUDA-11.8.0 tensorflow/2.11.0-CUDA-11.8.0 scipy-bundle/2021.10 ",
"cluster": "ub-hpc",
"auto_accounts": "cse999",
"auto_queues": "general-compute",
"auto_qos": "general-compute",
"bc_num_hours": "6",
"num_cores": "4",
"memory": "12",
"gpu_num": "1",
"node_type": "V100",
"email": "UBITusername@buffalo.edu",
"bc_email_on_started": "1",
"email_on_terminated": "1"
},
```

Next is information from the job scheduler that's useful to CCR's staff for helping to track down problems.  But there is also useful info for you!  Take a look at fields like `reason`, `state`, `memory` (Did you request as much as you though you did?  This is listed in megabytes, not gigabytes.), and to find your output files look at the `workdir` field:  
```
"info": {
"id": "15033962",
"status": "undetermined",
"queue_name": "general-compute",
"wallclock_time": 68,
"wallclock_limit": 21600,
"cpu_time": null,
"submission_time": "2024-02-26 14:29:20 -0500",
"dispatch_time": "2024-02-26 14:30:10 -0500",
"native": {
"account": "cse676",
"job_id": "15033962",
"exec_host": "cpn-u24-07",
"min_cpus": "4",
"cpus": "4",
"min_tmp_disk": "0",
"nodes": "1",
"end_time": "2024-02-26T14:31:18",
"dependency": "(null)",
"features": "V100",
"time_limit": "6:00:00",
"time_left": "5:58:52",
"min_memory": "12M",
"time_used": "1:08",
"reason": "OutOfMemory",
"state": "OUT_OF_MEMORY",
"work_dir": "/user/[CCRusername]/ondemand/data/sys/dashboard/batch_connect/sys/jupyter_adv/output/73b7bde3-232a-4433-a3d3-4934ca914c99",
"gres": "gres:gpu:1"
},
"gpus": 1,
```

If you're having trouble with OnDemand we highly recommend submitting a help ticket using this feature since it provides us so much useful information.  



## More frequently asking questions:  

We also have many answers to other OnDemand questions on our Frequently Asked Questions page, including:  

[Why can't I login?](../faq.md#why-cant-i-login)  
[No Home Directory Found on Login to OnDemand](../faq.md#why-am-i-seeing-a-home-directory-missing-error-on-login)  
[Blank window after starting OnDemand session](../faq.md#why-do-i-see-a-blank-window-when-starting-an-ondemand-desktop-why-are-the-desktop-icons-not-working)  
[Invalid account, partition, or QOS error](../faq.md#why-do-i-get-an-invalid-account-partition-or-qos-specification-error-when-i-try-to-run-a-job)  
[Why is my job showing `reqnodenotavail`?](../faq.md#why-is-my-job-pending-with-reason-reqnodenotavail)   
[XFCE PolicyKit Agent error](../faq.md#how-can-i-fix-the-xfce-policykit-agent-error-in-ondemand-desktop-sessions)  

