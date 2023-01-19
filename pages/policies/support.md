# CCR Support, Maintenance, and Installation Policies

## Support Policy  

CCR staff provide systems and user support during regular business hours, Monday through Friday 8am-5pm excluding University at Buffalo holidays.  No weekend support is provided.  

**Emergencies**  
Emergency support is provided off-hours for critical infrastructure outages only (i.e. storage, networking, batch scheduler, cooling, electric, and cloud infrastructure) that affect large numbers of users.  We are unable to provide emergency support for individual cloud instance or compute node outages.  

**Requesting Support**    
Requests for support are to be submitted through the [CCR help portal](https://ubccr.freshdesk.com) or by emailing CCR Help and are handled on a first come, first served basis.  We strive to respond within 2 business days to all requests for help.  Though hardware and software installations and configurations may take longer, they are usually completed within two weeks.  Please see the [CCR Help page for more information](../help.md).  

## System Maintenance Policies  

CCR staff strive to maintain up-to-date and secure resources for the UB research community.  In order to do this we plan regular maintenance periods for the services we provide.  
[Schedule of Planned Maintenance](https://ubccr.freshdesk.com/support/discussions/forums/5000296650)

**Cluster Maintenance**  
Regularly scheduled maintenance periods are conducted for all CCR clusters.  The clusters are offline on the last Tuesday of every month, unless otherwise noted.  The downtime starts at 7am and is usually completed by 5pm.  Jobs are held in the UB-HPC queue unless otherwise noted by CCR beforehand.  Reservations are put in place for the academic and industry partitions of the UB-HPC cluster.  This means jobs will not run prior to the downtime if they can not be completed before the downtime starts.  The faculty cluster allows jobs to run right up until the downtime.  Any running jobs are killed when the downtime starts.  Faculty cluster users should make sure their jobs are scheduled to end prior to the start of the downtime or are able to checkpoint and restart.  

!!! Note
    If you're the owner of nodes in the faculty cluster and want a reservation put on your partition prior to these maintenance downtimes, please [contact CCR Help](../help.md)

**Non-cluster Services Maintenance**  
Other CCR services may experience maintenance downtimes several times a year.  Notifications are made in our [help desk portal](https://ubccr.freshdesk.com/support/discussions/forums/5000296650) and often via email to those users affected by the outage.

**Unplanned Outages**  
[Unplanned outages are posted in our help portal as alerts](https://ubccr.freshdesk.com/support/discussions/forums/5000120071) as well as on our [Twitter account](https://twitter.com/UBCCR)  

## Software Installation Policy  

CCR staff provide a suite of software that is standard for high performance computing environments.  This include compilers, Cuda, Anaconda Python, and some engineering packages such as Gromacs, NAMD, Matlab, Abaqus, Comsol, LSDYNA, and Ansys.

Software that does not require root level (administrative) access should be installed in a user's home directory or a group's project directory.  [More information on installing your own software](../software/building.md)  

If your software does require root privileges to be installed or you feel it would benefit other CCR users, you can submit an issue on [CCR's GitHub software repository](https://github.com/ubccr/software-layer/issues) requesting the software be installed.  Minimum requirements for software installation on the clusters:

1. Must run under Linux operating systems

2. Must be free to use in an academic environment (for the UB-HPC cluster) or the user/group must purchase a license for the software.  The software installation will then be restricted for use only by that group.  (When at all possible, groups should install software in their own project directories)

3. If a license is required, the cluster can only support a floating license, not a node-locked license.  

4. Preferably has an Easy Build recipe available.  [Search for one here](https://github.com/easybuilders/easybuild-easyconfigs/tree/develop/easybuild/easyconfigs) and include in your GitHub issue.  

If your software meets these requirements, please submit a GitHub issue to request the install and provide any installation files or download links you have for the software.  Once evaluated by CCR staff you will receive a decision about whether or not we can support the installation and an estimate for completing the installation.  Some installations are straight-forward and can be done within a matter of days; others can be quite time-consuming.  If you require software to meet a deadline, please ensure your request is submitted with plenty of lead time.  Our current staffing levels don't allow for much individualized software installations but we can often help users through the process via help tickets.  

## Hardware Installation Policy  

CCR is able to provide installation and maintenance of compute nodes purchased by faculty research groups.  Please [see this page for more information](https://ubccr.freshdesk.com/en/support/solutions/articles/13000048771-hardware-installation-maintenance-and-support-policy)  
