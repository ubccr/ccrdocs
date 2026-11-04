# Global Scratch Decommissioning

  
The `/vscratch` file system is being removed from service on **Tuesday, November 24, 2026**.  Any data you'd like to preserve should be moved or copied to your group's shared project directory.  Groups that are currently using `/vscratch` will have their project directory quotas increased on September 29, 2026 to accommodate moving their scratch data.  If your group doesn't currently have a project directory, one will be created for you. For those `/vscratch` directories with NO usage, your group's directory will be deleted and the allocation expired in ColdFront.

To prepare for this migration, please begin updating your job scripts and workflows now.  If there is data in scratch you no longer want, you can leave it there and it will be deleted automatically after 60 days.  

**Important dates to be aware of:**  

- **October 27:** During the maintenance downtime,`/vscratch` will be set to `read only` mode.  You will have 30 days to copy anything you wish to keep but **you will not be able to write any new files or update existing files** any longer.
  
- **November 24:** During the maintenance downtime, `vscratch` will be unmounted and become unavailable to all users.  Please be sure to copy any important data over to your shared project directory prior to this date. ==You will **NOT** be able to access data in `/vscratch` after 7am on this date!==

    
**What if my group needs more space?**  

By default CCR provides 1TB of free storage to all research groups.  The group's principal investigator may request increases to this quota, up to 5TB for free, but must provide valid justifications for the increase.  We ask that you request increases incrementally, as you need the space, as current usage will be evaluated when reviewing these requests.  For usage above 5TB, additional [storage can be purchased](../hpc/storage.md#purchasing-project-storage) at the current rate.
