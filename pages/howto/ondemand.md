# Open OnDemand Features & Customizations  

Version 3.0 of Open OnDemand introduced many new features that CCR users now have access to.  We've also changed how we offer resources and the apps you might be used to.  Here we'll cover those changes, some of the new features, and how you can customize your portal experience. Our primarly OnDemand documentation can be [found here](../portals/ood.md)  

!!! Warning "Important Environment Info!"  
    This version of OnDemand uses CCR's new software modules automatically.  You do not have to do anything to utilize these modules.  You will not have access to the old modules in /util. Please refer to the [software module documentation](../software/modules.md) as there are lots of new features available! 

## New Features

### Pre-configured Selections  

All the desktop and interactive apps now have select menus that get pre-populated.  Depending on which cluster you choose, some of the available options, like partitions and QOS, will change.  The forms also pre-populate the Slurm account information based on the logged in user.  It's important to note that you may see some options that you don't have access to or aren't permitted to use through the OnDemand apps.  This is a new feature and still a bit buggy.  For the `UB-HPC` cluster, users should not select the options `scavenger, viz, or normal` in either the partition or QOS drop down menus.  You will see the `industry` partition; however, if you do not have the `industry` QOS in your drop down menu, this means you don't have access to it.  Similarly, for the `Faculty` cluster, users will see all the partitions listed; however, you will only have access to a partition if the associated QOS is listed in your drop down menu.  We're working to improve this experience to make it less confusing.  

### Recently Used Apps  

The `Recently Used Apps` section on the OnDemand dashboard is a new feature of OnDemand 3.0.  This will list the last 3 applications you launched in OnDemand.  When you click on one, it immediately launches a new session with the same options you last selected.  This saves you time from having to select all the options repeatedly.  This is a one-click easy button for re-launching desktops or interactive apps.

### Quick Launch App  

The `Quick Launch UB-HPC Desktop` app provides a one click easy button for launching a desktop session on the UB-HPC cluster with all the defaults.  This means your job will get 1 CPU, 2.8GB of RAM, 24 hours of walltime and run on the `general-compute` partition.  You can't change any of the options for this quick launch app.  If you require different settings, use the `UB-HPC & Faculty Cluster Desktop` app which provides many options.  

### Desktop Apps  

Previously, CCR provided separate desktop apps for the UB-HPC and Faculty clusters.  Now there is one app for both and users are able to select which cluster to submit to.  Though users will see all partitions listed in the Faculty cluster, they will only be able to use the one(s) that match the QOS values shown in their drop down menu.  For example, to use the `ub-laser` partition in the faculty cluster, you must select the `ub-laser` QOS.  

!!! Tip "Missing Something?"  
    If you think the drop down options for account or QOS are wrong, check [ColdFront](https://coldfront.ccr.buffalo.edu).  These values match up to allocations for resources in ColdFront.  You must be on an active allocation for the resource in order to access it.  


### Job Card Formating

There are additions to the job cards in OnDemand including a link to submit a help ticket that links directly to the job for easier review by the CCR IT staff.  You'll notice the verbage has changed with respect to actions you can take on a job.  A running or queued job has the `cancel` option which cancels the job and removes it from the queue.  Once a job has been completed, you can `delete` it which removes it from your list of most recent jobs.  This does NOT delete the job data in your home directory so you will need to periodically clean up data you no longer want.  The session ID link will take you directly to the subdirectory where the job's data and output files are stored.  

!!! Note "Managing your OnDemand Disk Usage"
    To clear up disk space in your home directory, you can remove directories for completed jobs when you're done retrieving the job output data.  You can find these in subdirectories under: `/user/username/ondemand/data/sys/dashboard/batch_connect/sys`  

### Submit a Help Ticket

There are two ways to submit a CCR help ticket directly from OnDemand.  The first is by clicking on the `Submit support ticket` on the job card.  This will include job specific information useful for the IT staff.  Please fill out the form including your email address, anyone you'd like to CC, a subject line, and a description.  Please be as descriptive as possible to speed up our response to you.  If there are any screenshots you'd like to include that will better explain your issues, you may attach up to 3. You can include the full path of your job output in your ticket; however the session ID itself is not useful to IT staff.  If you have a more general issue that's not related to a specific job, you can submit a ticket by going to the `Help` menu and clicking on `Submit support ticket.`  This form has all the same options as what was just described except it doesn't include job specific information.  These forms get submitted to CCR's help desk and you will receive an automated email indicating the request has been submitted along with a ticket number.  You can reply to that email with updated information or access the ticket through [CCR's help portal](https://ubccr.freshdesk.com).  

### Files App

You can now add links to OneDrive and UB Box in the Files app!  You will need to use the command line to setup authentication with your UB Box and/or OneDrive account(s).  We provide information about using `rclone` to do that [here](../hpc/data-transfer.md#rclone) with an example of setting up a OneDrive link.  Once this authentication is setup, you'll see the links in the OnDemand Files app.  If you've done this setup after logging into OnDemand, you may need to restart the OnDemand web service to see the changes.  To do so, under the `Help` menu click on `Restart Web Server`  

**OneDrive**
Follow [these instructions](../hpc/data-transfer.md#using-rclone-with-onedrive) to complete the initial connection with OneDrive using RClone.

**UB Box**  
Follow [these instructions](https://rclone.org/box/) to complete the initial connection with UB Box using RClone.  

**Globus**
Coming very soon!  


## Customization  

### Building your own interactive app
Coming soon!


