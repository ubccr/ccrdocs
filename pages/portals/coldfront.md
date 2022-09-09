# ColdFront

ColdFront is an open source resource allocation management tool built for high performance computing centers that allows the management of Center resources and user allocations to those resources.  CCR developed this tool to allow our users the opportunity to request and manage the access they and their students or collaborators have to the many resources in CCR's data center.  In order to obtain access to any CCR services, you must be on an active allocation for the resource.  Research faculty principal investigators and teaching faculty are able to create projects in ColdFront and request allocations to CCR resources for themselves and their group members or students.  

## Login to ColdFront

https://coldfront.ccr.buffalo.edu  

!!! Warning  
    You must be on the UB campus or connected to the [UB VPN](https://buffalo.edu/ubit) from off campus in order to access CCR's portals  

Two factor authentication must be enabled on your CCR account in order to access CCR's OnDemand portal.  If you do not, you will get the error ``You don't have access to this resource`` when attempting to login.  

If you get the error ``invalid login`` you are entering your password, one-time token from your authentication app, or both incorrectly.  

Having trouble with 2FA?  Watch this 50 second video!  
![type:video](https://www.youtube.com/embed/g6hWYooFKWE)

[More information on two factor authentication](../2fa.md)  

## Project Setup  

New faculty users must create a project before they can request allocations.  See our ["Getting Access" information](../getting-access.md) to ensure you've setup your account and status correctly.  After logging into ColdFront, you should see the `Add a project` button.  If you already have a project or are a member of a colleague's project, and would like to create a new one, click on the `Projects` link.  This will display the projects you are a member of and here you can click on the `Add a project` button to create a new one.  

You'll be prompted to add a project title (for your reference), a description for use in CCR's reporting to UB administration, and a field of science.  If this project supports multiple works please select a field of science that applies to the majority of your work.  Then click the `Save` button.  

### Project Detail  

The Project Detail page encapsulates all project information in one place.  There is the project description, status, date created, PI name, users associated with the project, allocations for resources, project attributes, grant info, publications, research output, and any notifications from CCR staff.  

#### Users  
To add a user to your project they must already have a CCR account.  Please direct them to [these instructions](../getting-access.md).  Click the `Add Users` button and search using their UB username or change the option and search for first or last name or email address.  To remove a user from your project, click the `Remove Users` button and use the checkbox to select the user(s) you'd like removed.  

**Manager Access** - the PI on the project can change the role of any user to 'Manager' and this person will have the same permissions as the PI to add/remove users, request/renew allocations, add/remove project info such as grants, publications, and research output.  Managers may also complete the annual project review.  To change a user's role, click on the `Edit` button next to the user's name under the Actions column.  Change the role from User to Manager and click the `Update` button.    

**Notifications** - all users on a project will receive notifications about allocations including reminders of upcoming expiration dates and status changes.  Users may uncheck the box next to their username to turn off notifications.  Managers and PIs on the project are not able to turn off notifications.  

#### Allocations  
Allocations provide access to resources.  CCR provides resources such as clusters, storage, cloud, and software licenses.  Some of these resources are available for all PIs to request access to; others are restricted to private groups or users.  If you're unsure what to request an allocation for, please check out our [Getting Started page](../getting-started.md).  

#### Project Attributes  
This feature is coming soon to CCR's ColdFront portal.    

#### Grants  

We encourage all faculty members to provide information about all active grants they've received.  This helps show the level of funding CCR resources help to enable.  If your grant provides a percent credit and/or direct funds to CCR there are fields to indicate the amounts.  Providing funds to CCR may qualify your group for a priority boost.  Please see our website for more information on becmoing a [CCR Supporter](https://www.buffalo.edu/ccr/support/ccr-help/accounts.html#boost).

!!! Tip  
    Coming soon: Support for importing grant and publication info from ORCID!

**Adding Grants**  

Click the `Add Grant` button and fill in all fields pertaining to your grant (anything with an asterisk* is required) and click the `Save` button.  Descriptions of the fields are as follows:  

- **Title** - enter the full title of the grant provided by the funding agency  
- **Grant number from funding agency** - enter grant number provided by the funding agency.  If this grant is still pending, enter 0000  
- **Role** - choose from PI, Co-PI, or SP (senior personnel)  
- **Grant PI Full Name** - if you're not the PI, please enter the PI's full name.  We use this to ensure that we're not counting the same grant multiple times  
- **Funding agency** - select from list.  If it is not in the list, choose Other and enter the name in the next field  
- **Other funding agency** - enter the agency's name if not found in the list  
- **Other award number** - enter if there are several numbers given to the grant  
- **Grant start date** - select from the calendar when the grant begins  
- **Grant end date** - select from the calendar when the grant ends  
- **Percent credit** - this is the number listed on the UB Sponsored Projects form for a grant submission as financial credit to the department/unit in the credit distribution section.  If you listed a percent of the grant to give to CCR, enter that here.  If not, enter 0  
-  **Direct funding** - funds budgeted specifically for CCR services, hardware, software, and/or personnel support.  If none, enter 0  
- **Total amount awarded** - total amount you were awarded in the grant.  We use this to show how much CCR is supporting in research dollars.  
- **Status** - choose from active, archived, or pending
- Click the `Save` button  

**Editing Grants**  
You can edit existing grant information by clicking on the pencil icon under the Actions column.  Make changes to any fields you need to and then click the `Save` button.  

**Deleting Grants**  
You can delete a grant by clicking on the `Delete Grants` button.  You will be presented with a list of all grants associated with the project, both active and past (expired).  Click the checkbox next to the grant(s) you'd like deleted and then click the `Delete selected grants from project` button.  

#### Publications
We ask faculty to upload their publication information that acknowledges CCR or in which the information contained directly relates to work done at CCR.  You are welcome to add all your publications to this list, if you'd like.  

**Adding Publications**
To add publications, click on the `Add Publication` button on the Project Detail page.  You'll be presented with a box to enter your DOI.  Copy and paste the full DOI number and then click the `Search` button.  If the search yields the correct result, click the `Add Publication to Project` button.  You will then be redirected to the project detail page where you'll see your publication listed.  You will also see a label indicating the last time you updated publications on the project.  

**Deleting Publications**
You can delete publications off of your project list by clicking on the `Delete Publications` button.  You will be presented with a list of all the publications on the project and from there you select the one(s) you wish to delete.  Then click on the `Delete Selected Publications from Project` button.   

#### Research Output  
Research output is anything you'd like to capture in your project that's been developed as part of the project or created as a result of the research.  Some examples of items to enter here are: software applications (include links to opensource repos, for example), presentations done (not captured by publications), and media appearances or news articles.  This is an open text field so you can include anything you'd like here.  Though an edit feature is not yet available, you can delete items that you no longer want captured on the project.  


#### Notifications from Center Staff  
The Notifications section at the bottom of the project detail page includes any messages applied by the system administrators that might be important for all project users to see.  

### Annual Project Review  

CCR requires the annual review of all projects.  We ask that PIs or project managers update project description and field of science, if necessary, and remove any users that should no longer have access.  During this review we ask that you update your grant and publication information to ensure it is up-to-date.  This information is used in reports CCR provides to UB's adminsitration demonstrating the research and work CCR's resources enable each year.

When your project review is required, you will see a banner at the top of the project detail page that includes a link to the project review process along with `You need to review this project`

!!! Warning  
    New allocation requests and allocation renewals are not accepted until the project review has been submitted.  
