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

CCR staff provide a suite of software that is standard for high performance computing environments.  This include compilers, Cuda, Python, and some engineering packages such as Gromacs, NAMD, Matlab, and LAMMPS.

Software that does not require root level (administrative) access should be installed in a user's home directory or a group's project directory.  [More information on installing your own software](../software/building.md)  

If your software does require root privileges to be installed or you feel it would benefit other CCR users, you can submit an issue on [CCR's GitHub software repository](https://github.com/ubccr/software-layer/issues) requesting the software be installed.  Minimum requirements for software installation on the clusters:

1. Must run under Linux operating systems

2. Must be free to use in an academic environment (for the UB-HPC cluster).  

3. If a license is required the software needs to be installed in the group's project directory.  The cluster can only support a floating license, not a node-locked license.  

4. Preferably has an Easy Build recipe available.  [Search for one here](https://github.com/easybuilders/easybuild-easyconfigs/tree/develop/easybuild/easyconfigs) and include in your GitHub issue.  

If your software meets these requirements, please submit a GitHub issue to request the install and provide any installation files or download links you have for the software.  Once evaluated by CCR staff you will receive a decision about whether or not we can support the installation and an estimate for completing the installation.  Some installations are straight-forward and can be done within a matter of days; others can be quite time-consuming.  If you require software to meet a deadline, please ensure your request is submitted with plenty of lead time.  Our current staffing levels don't allow for much individualized software installations but we can often help users through the process via help tickets.  

## Hardware Purchase & Installation Policy  

CCR maintains custom servers and compute nodes for faculty research groups, in addition to our large production clusters and visualization hardware, which are freely available to UB and affiliated researchers. The machine room space, cooling, and networking available at CCR along with the technical expertise in system administration and programming allow UB researchers to devote their time to important research rather than cluster/systems maintenance.

[External Co-Location Policy and Fees for business tenants of CBLS](https://ubccr.freshdesk.com/solution/articles/13000060901-external-co-location-policy)  

CCR is able to provide the following options to faculty groups:

1.  Dedicated compute nodes:  
    - Great for users who want dedicated compute cluster resources built into the existing SLURM batch scheduler environment  
    - NO wait time! (aside from the time it takes to schedule and launch a job)  
    - Longer wall time than academic cluster (up to 30 days)  
    - Access to same infrastructure as academic cluster (home and project directories and high speed scratch storage)  
    - One-time fee charged to cover cost sharing of infrastructure used to house and support your equipment  
    - Give back to the UB research community by providing idle compute cores to other users for their research use  

2. Lake Effect Infrastructure-as-a-Service (IAAS) research cloud:  
    - Great for research groups that require special software, databases, or websites or that want to control their own servers and software installation  
    - Do-it-yourself cloud instances (virtual machines) – faculty group is responsible for operating system and software installation, system maintenance and security.  
    - The low cost and great flexibility of this option makes it desirable to many research groups.  
    - Consumption based pricing – only pay for what you use  
    - Access to various hardware, memory and storage combinations without the expense of having to purchase dedicated machines  
    - Compatible with Amazon Web Services (AWS) giving researchers the ability to scale to AWS, if desired.  

**Comparing the Options:**  

- Dedicated compute nodes  
    - Cost: One time co-location fee **PLUS the cost of the compute node** ==(see rate info below)==
    - PI responsibility: None, except facilitating the compute node purchase and delivery with your department  
    - CCR responsibility: Physical hardware install/maintenance/repairs, operating system and software install, updates, security
    - Pros/Cons:  Same setup as compute nodes in UB academic cluster, access to CCR’s network attached storage (home & project directories, high speed scratch space), no long term storage on local disks, no local software installations, maximum job runtime of 30 days, maintenance downtimes every 30 days, no local hardware backups, no administrative access  

- Lake Effect IAAS Research Cloud  
    - Cost: - Usage based subscription, optional fees for additional storage and consulting ==(see rate info below)==
    - PI responsibility: Faculty group is entirely responsible for OS & software install, setup, updates & security    
    - CCR responsibility: Responsible for cloud infrastructure only  
    - Pros/Cons:  No backups provided, no maximum run time, 1-2 annual maintenance downtimes, full administrative access, NO access to CCR’s network attached storage (home & project directories, high speed scratch space)    

==**Rates are based on the type of account they're paid out of:**==  

- Rack fee: $315/u*, if paying with internal State, RF, UBF, or FSA accounts. If paying with other internal funds, rate is $362.07/u (includes GUSF fee imposed by UB).  External rate is $590/u  
- Cloud subscriptions - purchased in packs ([more info here](../cloud/lake-effect.md#subscriptions))  
- Consulting fee:  $63/hr, if paying with internal State, RF, UBF, or FSA accounts. If paying with other internal funds, rate is $72.41/hour (includes GUSF fee imposed by UB).  **Purchased in 8 hour increments.**  External rates - contact [CCR Help](../help.md) for quote.  

**The fine print and specifics for each option:**  

_**Dedicated Compute Nodes:**_  
Dedicated resources (nodes) for a faculty group or research lab built into the existing SLURM batch cluster environment


-  **Purchasing:**  
    - CCR staff will consult with you to determine your computing needs, provide specs for equipment that align with our data center technical requirements, and contact vendors for competing quotes. Based on 20 years of HPC experience, we have a list of vendors to recommend for not only their quality hardware but also their exemplary support.  
    - Once a satisfactory quote is received, the PI will submit that to their department to purchase and have the equipment delivered to CCR's data center.  
    - **NOTE:** We reserve the right to refuse to house hardware from vendors that we have had difficulty working with in the past.  

- ***Infrastructure (co-location) fee:**  
    - CCR charges a one-time fee for the infrastructure to run your compute node (rack space, cables, Ethernet network switches, electricity and cooling).
    - The co-location per rack "u" fee is based on the standard slot of a compute rack. If machines purchased are more than 1 “u”, the infrastructure charge is multiplied. For example, if the machine you purchase takes up 2 “u” in rack space, the infrastructure charge is $630 (if paying with internal State, RF, UBF, or FSA funds).
    - This one-time charge goes towards cost-sharing of the infrastructure used to house and support your equipment (rack, network switches, cabling, physical installation and maintenance).    

- **Support:**  
    - CCR staff provide support during regular business hours, Monday through Friday 8am-5pm excluding University at Buffalo holidays. No weekend support is provided.
    - Emergency support is provided off-hours for critical infrastructure outages only (i.e. storage, networking, batch scheduler, cooling, electric, and cloud infrastructure [not instances]).  
    - Requests for support are to be submitted to [CCR help](../help.md) and are handled on a first come, first served basis. We strive to respond within 2 business days to all requests for help. Though hardware and software installations and configurations may take longer, they are usually completed within one week.  

- **Warranty Requirements & Maintenance Policy:**  

    - The minimum warranty we require is 3 years, next-business day, on-site parts & service. We **strongly recommend** purchasing a 5 year, next-business day, on-site parts & service warranty for all equipment as this is the standard for computing equipment purchases at UB.  
    - _**The maximum age of hardware CCR will support is 7 years.**_  When equipment reaches this age, it is decommissioned and recycled. We do not guarantee we will be able to support your equipment for 7 years.  Technology changes rapidly and there are times when equipment that is no longer covered under warranty but is less than 7 years old can no longer be supported in CCR's data center. 
    - For hardware failures that are off warranty but less than 7 years old, CCR will provide basic troubleshooting and diagnostics to determine the cause of any errors.  The cost to troubleshoot and repair hardware outside of warranty is billed per hour with a minimum of 4 hours, pre-paid via interdepartmental invoice (IDI).  The faculty owner is responsible for the ordering and cost of replacement parts once off warranty.  There is no guarantee CCR staff will be able to repair failed aging hardware; however, we will make our best effort to do so.  

- **Installation and configuration:**  
    - Compute nodes are installed with the same image used by CCR for all compute nodes.  You will not have the ability to choose your operating system or additional software installed on the compute nodes.
    - Compute nodes have access to CCR’s internal network attached storage (project & home directories) and high speed scratch storage.  
    - Compute nodes are not backed up.  No permanent data storage is permitted on the local hard drives of compute nodes.  Users must use the network attached storage systems for storing data.  
    - No system administrative (elevated) privileges are given to the hardware owner or group members on compute nodes.  

- **Access to compute nodes:**
    - You control who has exclusive access to your nodes through the [Coldfront allocation management portal](../portals/coldfront.md).  Users of the CCR academic cluster will be permitted to run on your nodes when they are idle. We refer to this as "scavenging" nodes and it allows idle processors to work when they otherwise would sit inactive. Users who scavenge nodes run jobs that are able to be stopped and restarted. As soon as a user in your group with access to your nodes requests them, any scavenger jobs that may be running are terminated and your jobs begin with NO WAIT TIME.  
    - Compute nodes are not accessible to the external network; they can be reached only through the Slurm batch scheduler from the cluster login node.  We can not open up ports or provide access outside the CCR network.  
    - Maintenance downtimes are required every 30 days on dedicated compute nodes for software and operating system updates.  Emergency downtimes may occur as needed for critical security patches.  


_**Lake Effect IAAS Research Cloud:**_  
Cloud environment that provides researchers the ability to launch fully customizable instances (virtual machines) when they’re needed and only pay for what is consumed.  

- **Installation, Configuration & Maintenance:**
    - CCR provides support for the hardware and network infrastructure that backs the cloud  
    - Users of the cloud (faculty project leaders & their groups) are responsible for all operating system and software installations, as well as updates and security on their cloud instances. Faculty must comply with UB server security requirements and should consult with UBIT for specifics and assistance.  
    - Cloud users (faculty project leaders & those they permit in their groups) have full administrative access to their instances (virtual machines)  
    - Operating systems currently supported in the research cloud are CentOS and Ubuntu.  Windows is not currently supported due to the complex Microsoft licensing requirements but may be in the future.  Contact us for information on uploading your own images to the cloud.  
    - Cloud instances do not have access to CCR’s internal network attached storage (project & home directories) or high speed scratch storage.  
    - Cloud instances are not backed up.  It is the users’ responsibility to backup all data in the research cloud.  
    - Maintenance downtimes twice annually may be required on the cloud infrastructure for software and operating system updates.  Emergency downtimes may occur as needed for critical security patches.  

- **Support:**  
    - CCR staff provide support during regular business hours, Monday through Friday 8am-5pm excluding University at Buffalo holidays. No weekend support is provided.
    - Emergency support is provided off-hours for critical infrastructure outages only (i.e. storage, networking, batch scheduler, cooling, electric, and cloud infrastructure [not instances]).
    - Requests for support are to be submitted to [CCR help](../help.md) and are handled on a first come, first served basis. We strive to respond within 2 business days to all requests for help. Though hardware and software installations and configurations may take longer, they are usually completed within one week.  

- **Access:**  
    - Accounts & access to your group’s cloud project in the Openstack GUI is granted to CCR account holders only.  You control this through the Coldfront allocation management portal.  
    - Once your instance is launched, you control who can login to it using standard Linux account management.  
    - Cloud instances are available outside the UB networks.  It is imperative cloud users utilize security standards to lock down their instances (i.e. firewall policies, cloud security groups)  

- **Pricing:**  
    -  Pricing information can be [found here](../cloud/lake-effect.md#subscriptions).
