# Getting access to CCR

## Requirements for accessing CCR's resources  
CCR resources are available to all UB faculty members and their research groups.  However, access is not automatically provided via your UBIT account.  This section discusses the various statuses of users and what is required to be granted and maintain access to CCR's systems.    

### UB Faculty
Faculty act as the principal investigator for their research groups and courses in CCR's systems, and therefore are responsible for maintaining an up-to-date project, renewing their allocations, and monitoring their group's usage.  Staff, student, and collaborator accounts must be sponsored by a UB faculty member.  When a user is done working for your group, the PI should remove them from the allocations and project, thus preventing undesired access to the CCR systems and group's shared storage.  Please refer to our [account and data retention policy](policies/accounts.md#faculty) for more details.

While there is no cost for UB faculty groups to use CCR high performance computing resources, [queue priority](hpc/jobs.md#job-priority) is based on [contribution level](#supporters-priority-boost).   At a minimum, faculty using CCR resources are required to:

1. **Acknowledge CCR support in publications** - see [here](faq.md#how-do-i-acknowledge-the-use-of-ccr-resources) for recommended wording   
2. Include a **percent recognition credit to CCR (at least a 5%)** on the Sponsored Programs Approval Form (though this can be larger for grants requiring significant CCR resources - see [below](#supporters-priority-boost)).  NOTE:  Clicking the "use CCR" box on the Sponsored Programs Approval Form is not the same as including a percent recognition credit to CCR.  
3. Communicate with CCR about the nature of your research, publications and any funding that you have.  The ability to provide this information to us is handled by the [resource allocation management portal](portals/coldfront.md), [Coldfront](https://coldfront.ccr.buffalo.edu), and you will be required to update this info once per year.  

#### UB Faculty Account Application Process  

!!! Note "Off-campus Access Requires VPN"  
    CCR's resources are accessible from UB and Roswell Park networks only.  If off-campus, you must connect to the [UB VPN](http://www.buffalo.edu/ubit/service-guides/connecting/vpn.html) first.

**Faculty account creation is a three step process:**  

1. Create a CCR system account and enable two factor authentication.  Step-by-step instructions are [below](#setting-up-access).  
2. Using the ColdFront allocations portal, go to your [user profile](https://coldfront.ccr.buffalo.edu/user/user-profile/) and request an upgrade to PI status by clicking on the `Upgrade Account` button.  This will initiate a request to CCR staff who will verify your status at the university and contact you once your account has been upgraded.  
3. Once you hear back from CCR letting you know that your status is upgraded to 'PI,' you must create a new project in the allocation management portal, [Coldfront](https://coldfront.ccr.buffalo.edu), and request an allocation to the resources (clusters, storage, cloud, etc) you want access to. Please follow these instructions to [create a project](portals/coldfront.md#create-a-project), [request allocations](portals/coldfront.md#request-an-allocation), and [add users](portals/coldfront.md#add-or-remove-users), if desired.  If you're unsure what to request access to, please see [this list](available-resources.md) of currently available resources.  

NOTE: Students utilizing CCR's resources for class work are required to complete the "Intro to CCR" course in UB Learns prior to receiving access to the course allocations.  They will receive a certificate of completion which should be verified by faculty prior to adding them to your allocations.  This is not a requirement for graduate student research assistants, but it is highly recommended.  Please see [below](#intro-to-ccr-course-requirement) for more information.  

!!! Tip "Adding Users to Your Project"  
    Faculty can add users to their project and allocations at any time.  Please ensure they have created themselves a CCR account prior to attempting to add them in ColdFront.  


### Students

UB students must be working for a UB faculty member that will sponsor them for a CCR account or be taking a class that requires use of the CCR resources.  If you qualify for an account, follow the instructions [below](#setting-up-access) to create yourself an account and enable two factor authentication.  Once you've completed the account creation process, please contact the faculty member or course instructor who is sponsoring your account.  They should utilize the allocation management portal, [Coldfront](https://coldfront.ccr.buffalo.edu), and add you to their project.  CCR's systems sync once per day at 5pm with ColdFront, which updates your account to provide you with access to your group's allocations, allowing you to login to the systems.  Please refer to the student section of the [account and data management policy](policies/accounts.md#students) for detailed information.    

NOTE: Students utilizing CCR's resources for class work are required to complete the "Intro to CCR" course in UB Learns prior to receiving access to the course allocations.  Please see [below](#intro-to-ccr-course-requirement) for more information.  

### Staff  
UB staff accounts should be added to the research group's project and allocations by the principal investigator.  If you have not yet created a CCR system account, proceed to the [next section](#setting-up-access) to complete this step.  Once you've completed the account creation process, please contact the faculty member or course instructor who is sponsoring your account.  They should utilize the allocation management portal, Coldfront, and add you to their project.  CCR's systems sync once per day at 5pm with ColdFront, which updates your account to provide you with access to your group's allocations, allowing you to login to the systems.  


### External Users
External users are granted access either by being sponsored by a UB faculty member or through a signed agreement between your company and UB.  If you are affiliated with a UB faculty member, they will request an account on your behalf.  Your account will need to be manually created by CCR staff, after which you'll be contacted with setup instructions.  Please refer to the non-UB collaborators section of the [account and data management policy](policies/accounts.md#non-ub-collaborators) for more information.    

## Setting up Access  

CCR offers a variety of resources for researchers to use in their own projects.
To get started with CCR resources you need the following:

- [UB or Roswell Park VPN](#vpn-access)
- [A CCR user account](#creating-a-ccr-user-account)
- [Enable Two Factor Authentication](#enable-two-factor-authentication)
- [An active allocation to the resources you want to use](#allocation-requests)

### VPN Access

Access to all CCR resources, including creating accounts is restricted to UB
and Roswell Park networks. You must be either on campus or connected to
[UBVPN](https://www.buffalo.edu/ubit/service-guides/connecting/vpn.html) or
Roswell Park VPN. For more information on connecting to UBVPN [see here](https://www.buffalo.edu/ubit/service-guides/connecting/vpn/computer.html).
If you do not have a UBIT account or a Roswell Park user account please
[contact CCR Help](help.md) to inquire about VPN access.

### Creating a CCR user account

CCR resources are freely available to the UB and Roswell Park research
communities. You must create an individual CCR account and enable two factor
authentication if you wish to access any CCR resources. Please note that CCR
user accounts are separate from your UBIT or Roswell Park accounts.

A CCR user account can be created quickly and easily by [filling out the
form here](https://idm.ccr.buffalo.edu/signup) using your UB or Roswell Park
email address. Once your account is created you will need to verify your email
address and enable two factor authentication.

### Enable Two Factor Authentication

CCR requires all user accounts to have two factor authentication enabled. We
support OTP, which stands for One-Time Passcodes and is a common form of two
factor authentication (2FA). OTP is also known as app based authentication,
software tokens, or soft tokens where an app on your phone will generate unique
numeric passcodes as a second factor to provide increased account security.

To enable two factor authentication on your account, follow these easy steps:

1. Install an authenticator app on your phone. Authentication apps like Authy,
   Google Authenticator, and Duo are supported. We recommend Duo as it's also used by UBIT.

2. Login to CCR IDM portal [here](https://idm.ccr.buffalo.edu/) and click on
   [OTP Tokens](https://idm.ccr.buffalo.edu/otp) in the side menu.

3. Click on the "New Token" button and follow the directions to scan the QR
   code using your authenticator app. Enter the six digit passcode generated by the app.

For more details on two factor authentication [see here](2fa.md).

!!! Warning "Faculty accounts and PI status"
    If you are a Faculty member or PI, an additional step is required after
    you have enabled 2FA. You will also need to login to ColdFront
    and request that your account be upgraded to "PI Status" so you can request
    allocations. Go to your user profile
    [here](https://coldfront.ccr.buffalo.edu/user/user-profile/) and click
    on the `Upgrade Account` button.

## Intro to CCR Course Requirement  
==NEW: As of Fall 2024 Semester==  

All students (graduate and undergraduate) that require the use of CCR's resources for coursework and all undergraduate students working in research groups are required to complete the "[Intro to CCR](https://ublearns.buffalo.edu/d2l/le/discovery/view/course/285151)" course in [UB Learns](https://ublearns.buffalo.edu/) prior to using CCR's systems.  Once completed, students receive a certificate of completion that they can share with their instructor or research advisor.  **Faculty members should not add students to their allocations without verifying they have completed the "Intro to CCR" course.**  We reserve the right to deny support to students requesting assistance from CCR help without having completed the "Intro to CCR" course first.

Though faculty members, graduate students, and post docs working in research groups are not required to take the "Intro to CCR" course, it is HIGHLY recommended.  Many of you may have extensive HPC experience already but each HPC center does things a little differently.  This course will step you through CCR's resources and policies making onboarding your research group much faster and hopefully a pain free experience. We also provide many recordings of pertinent topics on our [YouTube channel](https://youtube.com/@ubccr). 

The "[Intro to CCR](https://ublearns.buffalo.edu/d2l/le/discovery/view/course/285151)" course is available on UB Learns for open enrollment.  Anyone at UB may enroll in the course.  Students taking the "Intro to CCR" course will be added to allocations that give them access to CCR's UB-HPC cluster for the current semester.  Use of the cluster with these allocations should be limited to only this course material.  Once the course is completed, you'll be removed from these allocations and should notify your course instructor or research advisor to request that they add you to their allocations.  Should you need an extension on your "Intro to CCR" allocation period, please contact [CCR Help](help.md)  

## Allocation Requests

Access to CCR resources is managed using allocations. ColdFront is the allocations management system CCR uses to manage resource allocations for the
entire center. In order to access CCR resources you must be on an active allocation.

- __Faculty members__ (Principal investigators) can use
  [ColdFront](https://coldfront.ccr.buffalo.edu) to create projects, add group
  members, and request allocations to resources.  Once an allocation is
  activated, users on that allocation will be able to access the resource.
  More details about ColdFront can be found [here](portals/coldfront.md#request-an-allocation).

- __Students and postdocs__ can contact the faculty member (PI) who is
  sponsoring your account to request that they add you to their project and
  allocations.

- __External Collaborators__ the faculty member you're working with needs to
  request a CCR account and VPN access by [contacting CCR Help](help.md)

- __Industry customers__ please [contact CCR Help](help.md) to request access.  

## Supporters Priority Boost  

In order to receive a priority boost for your jobs, you must have a funded grant that meets the [criteria above](#ub-faculty) AND includes **direct funds** to CCR or you may pay an annual supporters fee.  At minimum, you should budget $2,600 per year.  This is approximately 40 hours/year of CCR staff time at the UB Financial Services approved rate of $65/hour for typical projects.  Higher amounts are appropriate for projects that are expected to more heavily utilize CCR services.  Note that these rates are generally updated annually, so please contact us or UB Financial Services for current rates.  Boosting your group's priority will substantially increase your job throughput.  Please update your project in Coldfront and submit an [allocation request](howto/purchases.md#supporters-priority-boost) for the Supporters Boost resource so we can provide you with the boost in queue priority.  If you did not add CCR to your grant but have funding you'd like to use for this purpose, please use the allocation request process and we will initiate a purchase for you.  

Before you submit a grant, we are happy to work with you on the budget to help ensure that we can best support your project. We provide a [CCR Facility Description for PIs](https://www.buffalo.edu/content/dam/www/ccr/pdfs/CCRFacilityDescriptionPIs.pdf) document as reference material for your proposals.  Also, if you would like a letter of support for your proposal, please complete [this form](https://ubuffalo.teamdynamix.com/TDClient/55/Portal/Requests/ServiceDet?ID=388).

Acknowledging CCR in publications and grant proposals is important because it provides a metric by which the university can gauge the utility and impact that CCR resources (hardware, software, and personnel) have on externally funded research at UB.  See [here](faq.md#how-do-i-acknowledge-the-use-of-ccr-resources) for our recommended format.

**Thank you for your support!**