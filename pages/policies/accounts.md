# Accounts and Data Retention Policy

CCR accounts are available to UB faculty, their collaborators and students either working with them or in a class that requires access to CCR.  Account requirements and application info can be found here:
http://www.buffalo.edu/ccr/support/ccr-help/accounts.html

## Allocations to Resources

All access to CCR resources (clusters, servers, research cloud, project storage, software licenses)  is granted and revoked via allocations.  Allocations are managed by PIs in ColdFront
(https://coldfront.ccr.buffalo.edu).  Users should login to ColdFront to see what allocations they have access to and when they expire.  Faculty should renew allocations before expiration.  If an allocation expires, any user on that allocation will be no longer be able to access that resource.  Expired allocations can't be renewed.  A new allocation request must be submitted to gain access to the resource again.  More details can be found in the ColdFront documentation.


## Yearly Project Review

Faculty are required to review their projects and verify all accounts in their group on a yearly basis.   If there is no activity for one year, all accounts in the group will be deleted and data associated with the project, including user home directories, will be deleted.

!!! danger
    Data in expired accounts will not be migrated when CCR moves to new storage systems approximately every 5 years. If you want your data, please keep your project and allocations active.


## Faculty

Account - When a faculty member leaves the University, access to the UB network will be removed as soon as your employment ends.  Unless arrangements have been made, your CCR account will be terminated at the
same time as your UB account.

Data – All data owned by your account on our systems will be deleted within 30 days of account termination.  This includes data on CCR’s network attached storage systems (user & project directories), local compute node and global scratch directories, data stored on servers owned by the faculty group (if applicable), and cloud instances and storage (if applicable).

!!! warning "Important"
    When a faculty member leaves behind students at UB, arrangements MUST be made with those students and another faculty member to take over their account sponsorship. Student accounts must be sponsored by an active faculty member, so unless prior arrangements have been made, when a faculty member leaves, any accounts sponsored by them are also terminated and data is removed.


## Students

### Class Accounts

Account – Accounts provided for class work are valid for the semester that the class is offered in and automatically terminated at the end of the semester.  If a student requires additional time to complete coursework, the professor teaching the course must [contact CCR help](../help.md) to request an extension on the account.  Student accounts that are also sponsored by a faculty member remain active after the course ends, subject to the policies in the “faculty sponsored accounts” section below.

Data – Data in a student’s home directory created for a class account is deleted 30 days after account termination.  This includes data on CCR’s network attached storage systems (user & course project directories), local compute node and global scratch directories, and cloud instances and storage (if applicable).

Usage - Usage of the cluster by students in a class is reported back to the instructor of the class.  Requests for assistance, software installations, or other communications by students to CCR staff could potentially be shared with the instructor.


### Faculty sponsored accounts:   

Account – An account sponsored by a faculty member is terminated when a student leaves the University at Buffalo or when the sponsoring faculty member requests the student’s access to CCR be removed.  If a faculty member wants a student to continue to access CCR resources after leaving the university, a request must be made to [CCR help](../help.md).  The account will then be moved under the “non-UB collaborator” category of accounts (see below).

Data - Data stored on CCR’s network attached storage systems in the user’s home directory and local compute node scratch directories are deleted when the student’s account is terminated.  If there is data stored by the student in a faculty member’s project directory or cloud project, this data is not removed. It is up to the faculty member to manage the data in their project and global scratch spaces.

Usage - Usage of the cluster by students is reported to the faculty member sponsoring the student's account.  Requests for assistance, software installations, or other communications by students to CCR staff could potentially be shared with that faculty member as well.



## Non-UB Collaborators

Account – Accounts granted to non-UB collaborators are dependent on the sponsorship of a UB faculty member.  If at any time, the sponsor of your account wants your access to CCR resources cut off, we are required to terminate the account.

Data - Data stored on CCR’s network attached storage systems in the user’s home directory and local compute node scratch directories are deleted when the account is terminated. If there is data stored by the collaborator in a sponsor’s project directory, global scratch directory, or research cloud, this data is not removed. It is up to the sponsor (UB faculty member) to manage the data in these spaces.


## Research Cloud

All above policies apply to cloud accounts, in addition to the following:

Account - Access to the research cloud is granted through request and payment of a cloud subscription.  Users must have a CCR account to access the research cloud.  As stated in our [research cloud policies](../cloud/lake-effect.md), failure to maintain an active payment for cloud usage will result in the termination of cloud account access.

Data – If the account owner does not respond to CCR payment requests within 30 days, a final bill will be sent for the overage charges and all information/data associated with the cloud account will be deleted - this includes: instances (running & terminated), all data (including, but not limited to, S3 buckets, volumes, and snapshots), ssh keys, elastic IPs, load balancers, custom images. This is a permanent action.  Data in the cloud is not backed up and therefore, not retrievable once deleted.



## Misuse of Systems

Failure to follow University at Buffalo and CCR computing policies may result in your account being removed and all data deleted.  Please [review this policy for more details](misuse.md)  
