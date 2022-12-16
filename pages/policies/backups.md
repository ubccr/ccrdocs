# Data Backup Policy

Backups of CCR systems are done for disaster recovery purposes only.  We can not guarantee backups complete in a certain time period (i.e. within 24 hours).   We make a best effort to back up all file changes daily but the more files that change on our systems on a given day, the longer that process takes.

We highly recommend users backup their data offsite for additional protection.  Options include: UB Box or Microsoft OneDrive - provided by UBIT, your personal computer or other personal cloud options  

##  What is backed up?  

Home directories ``/user/[username]`` and project directories in ``/projects/academic`` on the core storage system are backed up to an offsite storage system by UB's Enterprise Infrastructure Services team.  

###  Backup Details  
- Incremental backups occur daily  
- Backups are retained for 30 days  

## What is NOT backed up?  

**NO OTHER DIRECTORIES EXCEPT WHAT IS LISTED IN THE ABOVE SECTION ARE BACKED UP!**

This includes, but is not limited to:

- Data residing in ``/tmp`` or ``/scratch`` on ANY server or compute node  
- The global scratch directories - ``/panasas/scratch``  
- Anything in the Lake Effect research cloud or any instances (virtual machines) running in the cloud  
- Industry cluster client directories located in ``/projects/industry`` are NOT backed up unless it is specified in the company's Cooperative Use Agreement to do so.  

!!! WARNING
    By agreement with Roswell Park **/projects/rpci** and subdirectories within this space are **NOT backed up**

## Limits of the backup service

CCR is unable to backup user or project directories with more than 50 million files in them.  Any directory that reaches this limit will be excluded from the daily backups.  We will notify the faculty member/PI of the group before the directory is removed from backups.  However, it is the PI's responsibility to notify his/her group of this exclusion.  You can check how many files are in your directory using the iquota command:

```
iquota -u username  
iquota -p /projects/academic/YourGroupName
```

##  Requesting a data restore

Every effort will be made to retrieve requested data files from the backups, however we do not guarantee that the data can be recovered.  As stated above, we strongly recommend you keep copies of your important data on your personal machine, external disk, or cloud service.  

To request a file or directory be restored from backup tape, please [contact CCR help](../help.md) providing the following information:  

- Full file location to be restored,  
- Name of file(s)/directory(ies) to be restored  
- Date of last known time it was in this location  

!!! Note
    Remember, if it's over 30 days, it will no longer be available for restore.
