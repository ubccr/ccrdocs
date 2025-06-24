# Account and Data Policies  

This page includes information about account policies, including maintaining access, yearly project review, account retention, two factor authentication resets, and password requirements.  Data ownership, data retention, and data backup policies are also included here.  

## Accounts and Data Retention Policy

CCR accounts are available to UB faculty, their collaborators and students either working with them or in a class that requires access to CCR.  Account requirements and application info can be found [here](../getting-access.md#requirements-for-accessing-ccrs-resources).

### Allocations to Resources

All access to CCR resources (clusters, servers, research cloud, project storage, software licenses)  is granted and revoked via allocations.  Allocations are managed by PIs in ColdFront
(https://coldfront.ccr.buffalo.edu).  Users should login to ColdFront to see what allocations they have access to and when they expire.  Faculty should renew allocations before expiration.  If an allocation expires, any user on that allocation will be no longer be able to access that resource.  Expired allocations can't be renewed.  A new allocation request must be submitted to gain access to the resource again.  More details can be found in the ColdFront documentation.


### Yearly Project Review

Faculty are required to review their projects and verify all accounts in their group on a yearly basis.   If there is no activity for one year, all accounts in the group will be deleted and data associated with the project, including user home directories, will be deleted.

!!! danger
    Data in expired accounts will not be migrated when CCR moves to new storage systems approximately every 5 years. If you want your data, please keep your project and allocations active.


### Faculty

Account - When a faculty member leaves the University, access to the UB network will be removed as soon as your employment ends.  Unless arrangements have been made, your CCR account will be terminated at the
same time as your UB account.

Data – All data owned by your account on our systems will be deleted within 30 days of account termination.  This includes data on CCR’s network attached storage systems (user & project directories), local compute node and global scratch directories, data stored on servers owned by the faculty group (if applicable), and cloud instances and storage (if applicable).

!!! warning "Important"
    When a faculty member leaves behind students at UB, arrangements MUST be made with those students and another faculty member to take over their account sponsorship. Student accounts must be sponsored by an active faculty member, so unless prior arrangements have been made, when a faculty member leaves, any accounts sponsored by them are also terminated and data is removed.


### Students

**Class Accounts**

Account – Accounts provided for class work are valid for the semester that the class is offered in and automatically terminated at the end of the semester.  If a student requires additional time to complete coursework, the professor teaching the course must [contact CCR help](../help.md) to request an extension on the account.  Student accounts that are also sponsored by a faculty member remain active after the course ends, subject to the policies in the “faculty sponsored accounts” section below.

Data – Data in a student’s home directory created for a class account is deleted 30 days after account termination.  This includes data on CCR’s network attached storage systems (user & course project directories), local compute node and global scratch directories, and cloud instances and storage (if applicable).

Usage - Usage of the cluster by students in a class is reported back to the instructor of the class.  Requests for assistance, software installations, or other communications by students to CCR staff could potentially be shared with the instructor.


**Faculty sponsored accounts**  

Account – An account sponsored by a faculty member is terminated when a student leaves the University at Buffalo or when the sponsoring faculty member requests the student’s access to CCR be removed.  If a faculty member wants a student to continue to access CCR resources after leaving the university, the PI should request an [allocation in ColdFront](../portals/coldfront.md) for the `UBVPN Software` resource, adding just this one user to the allocation.  The account will then be moved under the “non-UB collaborator” category of accounts (see below).  The student will be contacted by CCR staff with information about VPN access.  

Data - Data stored on CCR’s network attached storage systems in the user’s home directory and local compute node scratch directories are deleted when the student’s account is terminated.  If there is data stored by the student in a faculty member’s project directory or cloud project, this data is not removed. It is up to the faculty member to manage the data in their project and global scratch spaces.

Usage - Usage of the cluster by students is reported to the faculty member sponsoring the student's account.  Requests for assistance, software installations, or other communications by students to CCR staff could potentially be shared with that faculty member as well.



### Non-UB Collaborators

Account – Accounts granted to non-UB collaborators are dependent on the sponsorship of a UB faculty member.  If at any time, the sponsor of your account wants your access to CCR resources cut off, we are required to terminate the account.

Data - Data stored on CCR’s network attached storage systems in the user’s home directory and local compute node scratch directories are deleted when the account is terminated. If there is data stored by the collaborator in a sponsor’s project directory, global scratch directory, or research cloud, this data is not removed. It is up to the sponsor (UB faculty member) to manage the data in these spaces.


### Research Cloud

All above policies apply to cloud accounts, in addition to the following:

Account - Access to the research cloud is granted through request and payment of a cloud subscription.  Users must have a CCR account to access the research cloud.  As stated in our [research cloud policies](../cloud/lake-effect.md), failure to maintain an active payment for cloud usage will result in the termination of cloud account access.

Data – If the account owner does not respond to CCR payment requests within 30 days, a final bill will be sent for the overage charges and all information/data associated with the cloud account will be deleted - this includes: instances (running & terminated), all data (including, but not limited to, S3 buckets, volumes, and snapshots), ssh keys, elastic IPs, load balancers, custom images. This is a permanent action.  Data in the cloud is not backed up and therefore, not retrievable once deleted.

!!! Warning  
    Failure to follow University at Buffalo and CCR computing policies may result in your account being removed and all data deleted.  Please [review this policy for more details](misuse.md)  


## Protected Status Data Policy  

CCR's systems fall under the same data protection policies as provided by the [University at Buffalo IT services](https://www.buffalo.edu/ubit/policies/restricted-data.html) for other computer usage and data storage.  Personally identifiable information (PII), restricted data, research data that has not been de-identified, and private data including but not limited to social security numbers, passport numbers, credit card numbers, dates of birth, passwords, and medical records, are not to be stored on CCR's systems. If you have any questions regarding data you plan to store on CCR's systems, please contact [CCR Help](../help.md) BEFORE transferring your data. 

## Data Ownership Policy

### User home directories  

CCR provides each cluster user with a home directory ``/user/[CCRusername]`` and a 25GB quota.  The data contained in the home directory is owned by the user and access to these files is under the control of the user only.

!!! Note
    We can not provide anyone with access to the home directory of another user without the user's express written consent  


### Shared project directories & global scratch directories  

These directories are accessible on all CCR servers by only your group.  Anyone in the group, by default, has access to all the files in these shared group directories, unless explicitly changed by the file owner.  Please be aware that any data in the group's project or global scratch directories is ultimately owned by the group's principal investigator (PI) or faculty group lead, regardless of the unix ownership permissions set on the file or directory.  

**We strongly encourage PIs to ask their group members to store files in these shared spaces so when they leave the university, the PI still has access to the data generated by the student while working with the group.**  

See these links for additional policy information from the University at Buffalo:  
[Protecting intellectual property](https://www.buffalo.edu/research/research-services/commercialization/protecting-your-ip.html)  
[UBIT account policy](https://www.buffalo.edu/administrative-services/policy1/ub-policy-lib/ubitname-account.html)  
[UBIT Computer and Network Use policy](https://www.buffalo.edu/administrative-services/policy1/ub-policy-lib/computer-network-use.html)  


### Roswell Park Project Directories  

RPCCC project space located in ``/projects/rpci`` is managed by RPCCC IT staff.  Please contact them for information on internal allocations/quotas and other policies related to data retention and data ownership.  


### Industry Cluster Client Data  

There should be one designated company employee responsible for management of the group's project and allocations for resources at CCR.  That user will be deemed the "owner" of the data on the systems.  Should this employee leave the company, CCR should be notified so that the CCR account can be removed and another employee can be made data owner and project manager.  Ultimately, all data generated under the company's account is owned by the company, not the individual employee.  


### Lake Effect Research Cloud Data  

As with the data in the project directories, ultimately the data stored on virtual machines in the research cloud is owned by the project PI or faculty group lead.


## Data Backup Policy

Backups of CCR systems are done for disaster recovery purposes only.  We can not guarantee backups complete in a certain time period (i.e. within 24 hours).   We make a best effort to back up all file changes daily but the more files that change on our systems on a given day, the longer that process takes.

We highly recommend users backup their data offsite for additional protection.  Options include: UB Box or Microsoft OneDrive - provided by UBIT, your personal computer or other personal cloud options  

**What is backed up?**  

Home directories ``/user/[CCRusername]`` and project directories in ``/projects/academic`` on the core storage system are backed up to an offsite storage system by UB's Enterprise Infrastructure Services team.  

**Backup Details**  
- Incremental backups occur daily  
- Backups are retained for 30 days  

**What is NOT backed up?**  

==**NO OTHER DIRECTORIES EXCEPT WHAT IS LISTED IN THE ABOVE SECTION ARE BACKED UP!**==

This includes, but is not limited to:  
- Data residing in ``/tmp`` or ``/scratch`` on ANY server or compute node  
- The global scratch directories - ``/vscratch``  
- Anything in the Lake Effect research cloud or any instances (virtual machines) running in the cloud  
- Industry cluster client directories located in ``/projects/industry`` are NOT backed up unless it is specified in the company's Cooperative Use Agreement to do so.  

!!! WARNING
    By agreement with Roswell Park **/projects/rpci** and subdirectories within this space are **NOT backed up**

**Limits of the backup service**  
CCR is unable to backup user or project directories with more than 50 million files in them.  Any directory that reaches this limit will be excluded from the daily backups.  We will notify the faculty member/PI of the group before the directory is removed from backups.  However, it is the PI's responsibility to notify his/her group of this exclusion.  You can check how many files are in your directory using the iquota command:

```
iquota -u [CCRusername]  
iquota -p /projects/academic/[YourGroupName]
```

**Requesting a data restore**  
Every effort will be made to retrieve requested data files from the backups, however we do not guarantee that the data can be recovered.  As stated above, we strongly recommend you keep copies of your important data on your personal machine, external disk, or cloud service.  

To request a file or directory be restored from backup tape, please [contact CCR help](../help.md) providing the following information:  

- Full file location to be restored,  
- Name of file(s)/directory(ies) to be restored  
- Date of last known time it was in this location  

!!! Note
    Remember, if it's over 30 days, it will no longer be available for restore.

## Password Policies

CCR maintains the same password policy as the University at Buffalo.  The [full policy can be found here](https://www.buffalo.edu/administrative-services/policy1/ub-policy-lib/ubit-password.html).  We want to specifically point out these parts:  

**Individual Accountability**  
All users of university systems are individually assigned a user-id (e.g., UBITName) and password for the purpose of accessing UB online systems.  In accordance with UB “acceptable use policies,” users are individually accountable for activities performed with their user-ids and passwords.  Passwords may not be shared with anyone, including with administrative assistants or secretaries.  UB passwords are considered to be regulated, private data.  

- Do not reveal a password over the phone to anyone  
- Do not reveal/include a password in an email message  
- Do not reveal a password to your supervisor, manager, or co-workers  
- Do not talk about a password in front of others  
- Do not fall for phishing scams that attempt to get you to reveal your password or other personal information  
- The University of Buffalo and legitimate businesses will never ask you to reveal your password in unsolicited email messages or telephone calls to you  
- Do not use the “Remember Password’ feature of applications  

**Password Security**  
Passwords for UB systems should not be identical to those used for personal/non-UB online accounts.  

**Password Strength Requirements**  
User and system passwords shall be constructed with strength and complexity that minimize the likelihood of successful password guessing or brute force attacks.  Passwords with strength and complexity must have the following characteristics:  

- Between 8 and 32 characters in length  
- Must contain at least  
- One lowercase character (a-z)  
- One uppercase character (A-Z)  
- One numeric character (0-9)  
- One non-alphanumeric character from this set: !?#$%&'()*+,-./:;@  
- Have no more than two pairs of repeating characters, such as “aa”  
- Cannot be an old password used within the past 365 days  


## Two Factor Authentication Reset Policy  

If a CCR user has lost access to the app they used to generate the time-based one-time passwords they will not be able to login to their CCR account or modify the two-factor authentication settings.  Users must contact CCR help to request the removal of this security feature.  In order to verify the account owner's identity, the user will be directed to present photo identification to a CCR staff member.  Details will be provided once you initiate [contact with CCR help](../help.md).  

Once we receive this information, we will remove the two-factor authentication setting from your account and you'll be able to login with your password.

## Preferred Name  

If you wish to change the name on your CCR account, please contact [CCR Help](../help.md).  No reason for the change is necessary.  The username for the account will remain the same.  CCR does not store pronouns in our account systems at this time.  TeamDynamix currently doesn't store this information either.If you include your pronouns in your ticket details, we will gladly use them when replying to your help tickets.  For additional information on the University at Buffalo's preferred name policy, please see [here](https://www.buffalo.edu/administrative-services/policy1/ub-policy-lib/student-preferred-name.html)  