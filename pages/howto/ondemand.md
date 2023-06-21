# Open OnDemand Features & Customizations  

Version 3.0 of Open OnDemand introduced many new features that CCR users now have access to.  We've also changed how we offer resources and the apps you might be used to.  We'll cover those changes, some of the new features here as well as how you can customize your portal experience.  

## New Features

### Pre-configured Selections  

All the desktop and interactive apps now have select menus that get pre-populated.  Depending on which cluster you choose, some of the available options, like partitions and QOS, will change.  The forms also pre-populate the Slurm account information based on the logged in user.

### Recently Used Apps  

The "Recently Used Apps" section on the OnDemand dashboard is a new feature of OnDemand 3.0.  This will list the last 3 applications you launched in OnDemand.  When you click on one, it immediately launches a new session with the same options you last selected.  This saves you time from having to select all the options repeatedly.  This is a one-click easy button for re-launching desktops or interactive apps.

### Quick Launch App  

The "Quick Launch UB-HPC Desktop" app provides a one click easy button for launching a desktop session on the UB-HPC cluster with all the defaults.  This means your job will get 1 CPU, 2.8GB of RAM, 24 hours of walltime and run on the general-compute partition.  You can't change any of the options for this quick launch app.  If you require different settings, use the "UB-HPC & Faculty Cluster Desktop" app which provides many options.  

### Desktop Apps  

Previously, CCR provided separate desktop apps for the UB-HPC and Faculty clusters.  Now there is one app for both and users are able to select which cluster to submit to.  Though users will see all partitions listed in the Faculty cluster, they will only be able to use the one(s) that match the QOS values shown in their drop down menu.  For example, to use the "ub-laser" partition in the faculty cluster, you must select the "ub-laser" QOS.  

!!! Tip "Missing Something?"  
    If you think the drop down options for account or QOS are wrong, check [ColdFront](https://coldfront.ccr.buffalo.edu).  These values match up to allocations for resources in ColdFront.  You must be on an active allocation for the resource in order to access it.  


### Files App

You can now add links to Globus, OneDrive, and UB Box in the Files app!  

**OneDrive**
Follow [these instructions](../hpc/data-transfer.md#using-rclone-with-onedrive) to complete the initial connection with OneDrive using RClone.

**UB Box**  
Follow [these instructions]() to complete the initial connecting with UB Box using RClone.  

**Globus**



## Customization  

### Building your own interactive app



