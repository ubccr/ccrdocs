# Empire AI Cluster Information  

The first test system of the Empire AI Consortium is in production.  This system is provided and managed by the Flatiron Institute.  System specifications can be found [here](https://empireai.freshdesk.com/en/support/solutions/articles/157000007946-alpha-hardware).  This system is referred to as `alpha` and its successor `beta` is expected to be available in Fall 2025.  

Initial project applications have been submitted to consortium members, reviewed, and are being onboarded on an ongoing basis by the Empire AI director and Flatiron system administrators.  PIs will receive notifications from the Empire AI management when their project is up next for onboarding.  CCR staff provide support to UB research groups that have access to "alpha" - both in using the EAI system and in helping to prepare groups to utilize those resources efficiently.


## Support  

All requests for help should be sent to `help` `@` `empire-ai.org` or submitted through the Empire AI help desk portal [https://empireai.freshdesk.com/](https://empireai.freshdesk.com/).  CCR staff help with supporting researchers and their group members with non-system related questions.  If you are having a system issue, we will help facilitate a resolution but do not have elevated privileges on the Empire AI cluster.

## Project Onboarding  

Decisions on which projects get selected from UB for access to Empire AI is done by the VPR's office.  Once a project has been selected for onboaring, the PI will be notified by the EAI director and will be asked to complete a form.  Once that's submitted, the PI's information is forwarded to the alpha system administrators for account creation.  You will hear directly from one of them when your account is ready and they'll provide additional account setup instructions.   

## Accounts for Research Group Members  

Once the PI of the project has access to alpha, they may request additional accounts for their students and collaborators.  **DO NOT SHARE ACCOUNTS.**  Submit a ticket to the [EAI support desk](#support) and a CCR staff member will facilitate the account setup.  New users will be asked to complete a form and then the user information is passed to the EAI system administrators for account creation.

## Logging In  

You must use an SSH client to login to alpha.  The hostname is:  
`alpha.empire-ai.org`  

If your username on alpha is not the same as on your computer, you will need to specify it as part of the ssh command.  For example:  

`ssh [YourUsername]@alpha.empire-ai.org`  

Your username on alpha will most likely be the same as your UBIT & CCR username.  

## First Login  

PLEASE CHANGE YOUR PASSWORD ON FIRST LOGIN! 
On account creation, you will be sent your initial password via an insecure method.  Please change your password when you login using the `passwd` command.  

## Two Factor Authentication

You will be required to enable two factor authentication on your account.  Further information can be found [here](https://empireai.freshdesk.com/en/support/solutions/articles/157000161230-google-authenticator-mfa-2fa-). 

Once 2FA is enabled, when logging in you'll be prompted to enter your password first and then your second factor which is the 6 digit code from your authentication app.  

We have seen issues with MobaXterm not presenting the prompt for the second factor and then failing to allow the login.  If you are not getting prompted for your second factor, please try another SSH client.  

## Storage  

Each user is provided a home directory in `/mnt/home/[YourUsername]`  

In addition to this, each user has a directory in the global scratch storage.  You'll find yours under `/mnt/lustre/suny`  

For more information on storage on alpha, please see [here](https://empireai.freshdesk.com/en/support/solutions/articles/157000175046-empire-ai-alpha-storage)

At this time there are no quotas on these filesystems; however, we've been told to expect that this will be coming soon.  There also is no automatic clearing of the scratch directories but the system administrators expect this to be necessary in the future.  Any changes to these policies will be disseminated to all users in advance.

There are no shared project or scratch directories, like we offer at CCR.  Instructions for sharing files on alpha can be found [here](https://empireai.freshdesk.com/en/support/solutions/articles/157000010953-how-can-i-share-data-with-other-users-).

## Using the Cluster  

The EAI alpha cluster uses the same job scheduler, Slurm, as CCR uses.  This should make your transition easier.  

### Partitions  

UB users have access to the `suny` partition.

### Priority Week  

