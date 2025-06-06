# Information for External Collaborators and Industry Customers  

Though the majority of our documentation applies to all users of our systems, there are a few topics that are specific to external collaborators or business customers of CCR.  Here we address those topics and provide direct links to information about using our systems.  

## Accounts & Access  

Any accounts for external collaborators or industry customers need to be created manually by CCR staff.  

** UB Faculty Collaborators:**
If you are a UB faculty member with an existing CCR account, it may be possible to provide your external collaborator with access to CCR's HPC environment.  If you only need to share data, please use [Globus](../hpc/data-transfer.md#guest-collections-globus-shared-endpoints). Collaborator accounts should be requested through [this form](https://ubuffalo.teamdynamix.com/TDClient/55/Portal/Requests/ServiceDet?ID=386) by the UB faculty member wishing to sponsor the account.  You will need to login to the client portal to access the form.  Please provide the full name, email address, and organization or company your collaborator is affiliated with.  You must also provide the location where your collaborator currently resides, and will be using the UB VPN service from.  


**Industry Customers:**  
You or someone from your organization will have worked with CCR's economic development coordinator to develop a Cooperative Use Agreement between your organization and the University at Buffalo.  After that agreement is signed by all parties, the coordinator will let you know you're free to contact [CCR Help](../help.md) to request access.  Accounts can not be shared so all employees that need access to CCR should request an account.  It's preferrable that one person be the primary point of contact for your group who requests account additions and deletions, manages storage purchases, and renews the group's allocations on an annual basis.  A CCR staff member will create accounts for your group and communicate with you on how to complete the setup of those accounts.  

## UB VPN  

Because CCR resources are behind the University at Buffalo firewall, external users will need to use the University's VPN service to connect to the UB network.  As part of the account onboarding process CCR staff will provide your VPN and CCR account names and download links for the VPN software.  

**1. Downloading the VPN software:**  
External collaborators and industry customers will need to download and install the UB VPN software, Cisco AnyConnect.  The link to download the software will be provided by CCR staff.  You will not be able to download the software from UBIT's website.

**2. Enabling Two Step Authentication for VPN account:**  
VPN accounts are provided by the University at Buffalo's central IT service.  CCR customers will be provided with credentials for a VPN account from CCR staff.  However, you will be required to setup Duo Two Step authentication using the Duo Mobile app on a smartphone or tablet.  
**The external customer VPN accounts do not support any other method for using Duo so please ignore other options listed on UBIT's website.**

!!! Tip "Install Duo Mobile first!"
    Please ensure you have the Duo Mobile app installed on your smartphone or tablet before continuing.

[Go here for Duo Two Step Enrollment](https://twostep.buffalo.edu/)

NOTE:  For authentication here you need to enter the prefix `itorg\` to the username provided to you by CCR.  For example, if CCR told you your VPN username is `uccr.smith` then enter this username to authenticate for the setup of Duo:  `itorg\uccr.smith`

For detailed documentation about setting up Duo for the UB VPN account, please see [UBIT's website](https://www.buffalo.edu/ubit/duo).  If you run into issues with the setup of your VPN account, please contact [CCR Help](../help.md) first and if we're unable to assist, we will engage UBIT support on your behalf.  

**3. Install VPN software:**  
Once you've downloaded the Cisco AnyConnect VPN software, install it on your computer.  Documentation can be found [here](https://www.buffalo.edu/ubit/service-guides/connecting/vpn.html)  

**4. Connect to the VPN:**  
Once installed, launch the Cisco AnyConnect software and **select "CCR" from the "Group" drop down list**.  When prompted, enter the credentials provided by CCR staff (username will be in the form of `uccr.yourCCRusername`).  Do NOT use the `itorg` part of the username as you did in the previous step.  

When prompted, enter "1" to send a push notification to the Duo app.  Touch the "Allow" button in Duo and then you'll be connected to the UB VPN.  For more information on connecting to our departmental VPN, please see [here](https://www.buffalo.edu/ubit/service-guides/connecting/departmental-vpn.html)  

**IMPORTANT VPN USAGE NOTES:**  

- The UB VPN allows connections for up to 24 hours.  Idle connections will be disconnected after 3 hours.  
- The UB VPN can not be used anywhere in the world:  
    - For industry customers, prior to signing of the Cooperative Use Agreement your organization was provided with a list of countries the VPN software should not be used in.  
    - If you're an external collaborator, you provided a country of residence to the UB faculty member requesting your account.  This is the only country the UB VPN should be accessed from.  If you need to update this information, please contact [CCR Help](../help.md).  
  **Please adhere to these guidelines or we risk the University revoking the account access.**  
- Please contact [CCR Help](../help.md) with any questions or issues regarding your VPN account.  If we're unable to solve them, we will contact UBIT on your behalf.  

## Login to CCR  

There are two methods for logging into CCR's HPC resources: the [Open OnDemand portal](../portals/ood.md), accessible from any web browser, or using a [SSH client](../hpc/login.md) and the Linux command line interface.  

NOTE: You must first be connected to the UB VPN before attempting to login to CCR's HPC resources 

We recommend all new users begin with the [Getting Started Guide](../getting-started.md).  


## Roswell Park Researchers  

RPCI researchers have access to CCR's HPC environment through an agreement between UB & RPCI.  We do not provide UB VPN accounts for Roswell-affiliated staff.  CCR's resources are available to you from the Roswell Park employee and VPN networks or, if you're dual appointed at UB, you may utilize your UB account to connect to the UB VPN.  

### Creating a CCR account  

All members of the research group must have their own CCR account.  Please follow [these directions](../getting-access.md) to create yourself an account using your Roswell Park or UB (if applicable) email address.  Principal investigators leading research groups will need to have their account upgraded to `PI` status.  Once your account is created, please login to CCR's allocation management portal, [ColdFront](https://coldfront.ccr.buffalo.edu), click on your name at the top right, then click on `User Profile`.  Click the `Upgrade Account` button and CCR staff will respond back to you once your account has been upgraded.  Please note this is for faculty leading research groups only.  Staff, students, and research assistants fall under the PI who will add them to their project after their account has been upgraded to a PI in our system.  

### Resource Allocation Management Portal  

PIs: Once your CCR account is upgraded, you will need to create a project in [ColdFront](https://coldfront.ccr.buffalo.edu) and request access to the resource(s) you'd like to utilize.  For more information about ColdFront [see here](../portals/coldfront.md).  

Once a project is created, you need to request allocations for the resources.  The resources available to RPCI groups are detailed out below.  Once your group members have created their CCR accounts, add them to your project in ColdFront as described [here](../portals/coldfront.md#add-or-remove-users).  You'll have the ability to select which allocations you want the users added to at this time.


!!! Tip "How does the allocation process work?"  
    Groups must have an active allocation for every resource they want to use at CCR.  PIs should request allocations for the resources they want to use, CCR staff will activate them, and then PIs will be required to renew the allocations annually.  Emails are automatically sent to remind PIs that their allocations are coming up for renewal beginning at 30 days, then again at 14 and 7 days prior to expiration.  If the PI does not request renewal before the allocations expire, the group's access to that resource is removed.


### Compute Resources  

CCR's HPC resources that RPCI research groups have access to consist of:

- Compute nodes in the `rpci` partition of the Faculty cluster, containing a variety of CPU counts and memory configurations.  Please request an allocation for the `RPCI partition` in ColdFront.  To see what type of hardware is available in this partition, use this command on the [login node](../hpc/clusters.md) or a compute node:  `snodes all faculty/rpci`  
Compute nodes are accessible through:
[Slurm batch scripts](../hpc/jobs.md) and via [OnDemand](../portals/ood.md) using the "UB-HPC & Faculty Cluster Desktop" app and interactive apps: make sure to choose the Faculty cluster and RPCI partition from the drop down menus.
- Faculty who have a dual appointment at UB (can not be a 'volunteer' appointment) may request an allocation to the `UB-HPC academic partitions (cluster partition)` resource. See [here](../hpc/clusters.md) for details on the UB-HPC cluster.
- RPCI researchers who have **active NIH funding** may request an allocation to the `UB-HPC Academic partitions (cluster partition)` resource and the `NIH boost (cluster partition)` resource.  This will allow your group to run on the UB-HPC cluster nodes and gives a slight priority boost to your group's jobs when running on the UB-HPC academic partitions.  **You must list your NIH grant in ColdFront in order to qualify for this access.**  We do NOT bill your grant funds for this use.

### Storage

**Project directories:**  RPCI research groups are provided a shared directory and portion of the RPCI storage quota that can be found in `/projects/rpci/[YourGroupName]`.  Please request an allocation for the `Project Storage` resource in ColdFront.  Roswell provides an initial quota of 500GB per research group.  If you require additional storage, please use the [Allocation Change Request] feature in ColdFront and provide a justification.  We're required to get approval from RPCI IT for storage increases.  

!!! Danger  
    **RPCI DIRECTORIES ARE NOT BACKED UP BY CCR!**

**Global scratch directories:**  Research groups may request an allocation for 10TB of global scratch storage, used for storing temporary data during job runs.  For more details about global scratch storage, see [here](../hpc/storage.md#global-scratch).  Please review the [global scratch policy](../policies/misuse.md#scratch-usage-policies) prior to use.  

### Data Transfer  

Both CCR and RPCI provide access to the Globus data transfer service which will allow you to securely transfer data between the two sites, as well as share data with collaborators.  Refer to our [Globus documentation](../hpc/data-transfer.md#globus-transfers) for more details.



