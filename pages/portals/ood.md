# OnDemand

Open OnDemand is a browser based single point of access for all of CCR's clusters, shared storage, and remote visualization servers.  OnDemand provides a graphical interface to view, edit, download, and upload files, manage and create job templates for CCR's clusters, and access interactive applications such as remote desktops to cluster nodes and the visualization servers, as well as GUI-based software like Matlab, Jupyter Notebooks, RStudio Desktop, and vscode.  All of this is done through the browser on almost any device, requires no additional software to be installed, and with minimal knowledge of Linux and job scheduler commands.  

_**This product is an open source project developed by [Ohio Supercomputer Center](https://openondemand.org).**_

![type:video](https://www.youtube.com/embed/YgLEWaINFD8)  

## Login to CCR's OnDemand  

!!! Warning "VPN Required"
    Access to OnDemand is restricted to UB and Roswell Park networks
    (either on campus or connected to their VPN services). [See here](../getting-access.md#vpn-access)

Two factor authentication must be enabled on your CCR account in order to access CCR's OnDemand portal.  If you do not have 2FA enabled, you will get the error ``You don't have access to this resource`` when attempting to login.  

If you get the error ``invalid login`` you are entering your password, one-time token from your authentication app, or both incorrectly.  

Having trouble with 2FA?  Watch this 50 second video!  
![type:video](https://www.youtube.com/embed/7DcoWk57mKg)

[More information on two factor authentication](../2fa.md)  

## On Demand Features  

Once you have logged into OnDemand you will be redirected to the dashboard.  On the dashboard, CCR displays important messages in the announcement bar at the top, our message of the day (MOTD) at the bottom, pinned apps (popular applications organized into sections), and 3 types of job reports created through the metrics portal, Open XDMoD.  Along the top are tabs for the different features offered in OnDemand.

### Apps  



### Clusters (terminal window)  

This provides command line access to cluster front-end login nodes.  CCR's OnDemand portal displays links for the UB-HPC and faculty clusters but these both point to the same login pool: vortex.ccr.buffalo.edu which will login you in to one of several front end servers.  Here you can run Linux commands as you would if you were to SSH into a front end.  These front end servers provide access to the shared storage and the Slurm scheduler to submit jobs to any of the clusters.  

!!! Note  
    The default Slurm cluster on these front-ends is ub-hpc cluster so faculty cluster users will need to specify the option "-M faculty" with all Slurm commands.

### Files App  

The Files App in OnDemand allows users to easily transfer files to or from their local computers, view and edit files on the CCR systems, and other basic file management tasks.   Here users can access files in their home directory, as well as any project or global scratch directories they may have access to.  

!!! Warning  
    Do NOT transfer large files or large amounts of file using this app.  Please use the Globus service for large file transfers.  File transfer is limited to the amount of memory on the OnDemand server, the number of users currently using it, and browser limitations.  

Under the `Files` tab all users will see the `Home Directory` option.  On the systems this points to `/user/username` and has a quota of 10TB.  If you have access to a share project or global scratch directory, you will see this in the Files drop down menu. You can verify what you should have access to by viewing your [active allocations in ColdFront](coldfront.md) (https://coldfront.ccr.buffalo.edu)  

### Interactive Apps  

Interactive apps provide a way for users to launch and connect to an interactive batch job running on the cluster.  Users will either connect to the compute node in a Linux desktop environment or to the application they're launching.  CCR offers virtual desktop and Jupyter Notebook apps for both clusters as well as Matlab, vscode, and RStudio Desktop apps for the UB-HPC cluster.

#### Desktop Interactive Apps  

There are several options for desktop applications in OnDemand.  Details about each desktop are available at the top of the app form, after clicking on the interactive app menu option on the left.  Information about maximum walltime is listed here as well as any other pertinent info.  Interactive desktop sessions are limited to one node; however if you have other requirements such as number of cores (CPUs), amount of memory (RAM), or specific node features you may enter that in the form.  If you do not care what type of hardware your desktop runs on, you can leave these blank and the scheduler will allocate one CPU and 2.8GB of RAM for your session.  

#### Remote Visualization Apps  

In addition to the virtual desktop apps, which are capable enough for some GUI-based software applications, CCR also offers visualization nodes that are accessibly only through OnDemand.  The visualization servers offer graphics acceleration which is required for certain software packages.  There is one OnDemand interactive app for the visualization nodes that launches OpenGL & CUDA enabled desktops and one for those software packages that require graphics acceleration but need OpenGL disabled to start.  Users are permitted to run one app on the visualization nodes at a time and they are limited to 24 hours of run time.

### Jobs  
#### Active Jobs  
The Active Jobs menu option takes you to a list of your jobs (pending, running, and recently completed) on the CCR clusters.  You can filter by cluster and show all jobs or just your jobs.  This includes jobs you may be running outside of OnDemand.  Once the list is displayed, more details about individual jobs can be viewed by clicking on the arrow to the left of the job id.   Job information includes: Job ID, Job Name, User, Account, Partition, State (pending, running, completed, blocked), Total Nodes, Node List, Total CPUs, Time Limit, Time Used, and Memory Requested.  For jobs running via OnDemand, the full path of the output files for the job is displayed.  Below this there are buttons to open this location in either the file manager or the terminal, for easy access to view the job script, job log, and any error files that may have been created.  If you are reporting an error to CCR Help or asking for assistance with a job, please provide the full path of the OnDemand job files.  

**Job Metrics:**  
Below the detailed job information for any job currently running, you will see two graphs that display CPU and memory usage of the job.  This is a great tool for determining if your job is performing as expected.  For even more information about the performance of the node, click on the `Detailed Metrics` link which opens a new tab to CCR's Grafana dashboards.  Grafana displays an array of detailed hardware statistics for the node(s) your job is running on including CPU, RAM, network, Infiniband/Omnipath, Disk usage and I/O, and GPU information.  [More job metrics are available in the Open XDMoD metrics portal](metrics.md).  

#### Job Composer  

The Job Composer provides a template system for creating and managing batch jobs from within the OnDemand interface.  Please see the documentation provided by [Open OnDemand developers](https://osc.github.io/ood-documentation/latest/applications/job-composer.html) for more information  

### My Interactive Sessions  

This section displays your currently running sessions and those that just recently finished.  The completed jobs stay in this list for 2 days allowing you to access the link to the jobs' output files.  You can remove the links by clicking the `Delete` button.  However, this does not delete the job data directory and output files.

!!! Note  
    To clear up disk space in your home directory, you can remove directories for completed jobs when you're done retrieving the job output data.  You can find these in subdirectories under: `/user/username/ondemand/data/sys/dashboard/batch_connect/sys`  

### Develop (Sandbox)  

OnDemand allows users the ability to create their own interactive apps and run them in a 'sandbox' environment.  CCR does not turn this on by default, however.  Please [contact CCR Help](../help.md) to request this feature be enabled for your account.  Once it is, you'll find the `My Sandbox Apps (Development)` option under the `</>Develop` menu in OnDemand.  More information about app development is provided by the [Open OnDemand developers here](https://osc.github.io/ood-documentation/latest/app-development)  

### Help  

The Help menu offers links to CCR's support contact info, documentation, and the ability to restart your OnDemand web process.  Occassionally, you'll find your OnDemand session may be slow or unresponsive.  Users can choose the `Restart Web Server` option to restart the process that runs their individual OnDemand session.  Most of the time you will not need to do this unless directed to by CCR staff.  
