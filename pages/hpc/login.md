# Logging In

**This page specifically refers to logging in to access the HPC clusters and shared storage resources.**  If you are looking for login information for portals that handle accounts, allocation management, cloud, and other services, please see the 'Gateways & Portals' section of the documentation.  Having trouble with your two factor authentication?  [See this page](../2fa.md)  

To get started with using CCR's clusters and shared storage you need the following:

- A CCR user account - Don't have one?  [See here](../getting-access.md)  
- An active allocation for the resource in ColdFront - No allocation?  [See here](../getting-access.md#requesting-an-allocation-in-coldfront)
- Two-factor authentication enabled - Not enabled yet?  [See here](../2fa.md)  
- A SSH client or web browser  

!!! Warning  
    Access to most CCR resources is restricted to UB and Roswell Park networks (either on campus or connected to their VPN services).  Users without access to UB or RPCI accounts should [contact CCR Help](../help.md) for VPN access.  

## Getting an account & access  

UB faculty, staff, students, those with a UB volunteer appointment, and those with Roswell Park email addresses, can create their own CCR account using the CCR identity
management portal, [following these instructions](../portals/idm.md#create-a-ccr-system-account).  Once an account is created, users must be added to an active allocation for one of the CCR clusters in order to access a login node.  Access is managed in CCR's resource and allocation management system, [ColdFront](https://coldfront.ccr.buffalo.edu).  Please refer to [these instructions for more information](../getting-access.md#requesting-an-allocation-in-coldfront).

## Using OnDemand for Web-Based Cluster Access  

[Open OnDemand](https://ondemand.ccr.buffalo.edu) provides access to CCR's clusters, storage, visualization servers, and interactive apps.  CCR's OnDemand portal offers Linux desktops for GUI-based applications, software applications like MatLab, RStudio Desktop, and Jupyter Notebook, and vscode, an interactive development environment.  OnDemand can be used in any browser from almost any device.  More information about OnDemand can be [found here](../portals/ood.md).  

[See here for info on using two factor authentication to login](../2fa.md)  


## Command Line SSH Login  

Users accessing CCR's HPC environment using SSH or SFTP will be connected to a login node. A login node is a outward facing server at CCR that users can connect to from their local machines. Once on a login node, users can perform a limited number of tasks:

- Edit files  
- Transfer Data  
- Submit & monitor batch jobs  
- Access storage resources  

!!! Note  
    Login nodes should not be used for resource-intensive tasks such as running software or compiling code. For those tasks, users should submit batch or interactive jobs to reserve a node in the cluster.   

### Command Line SSH Key Setup  

Access to most CCR resources is only available through SSH or the OnDemand portal.  If you do not use the OnDemand portal, you must use a SSH client on your computer.  Furthermore, users must use SSH keys to connect to CCR servers using SSH/SFTP/SCP.  Passwords are not accepted.  

SSH key pairs allow us to login without a password using SSH to CCR's login nodes. We keep our private key on our local machine and upload the matching public key to our CCR account. Once uploaded, we can login to any CCR server that supports SSH logins.  Please [follow these instructions to upload your public SSH key](../portals/idm.md#ssh-keys) to the CCR identity management portal before attempting to connect to CCR's servers.  

### SSH Agent  

Running a SSH agent process on your machine allows you to load your SSH private key one time and it will be used for every SSH login attempt.  This allows you to skip specifying the key in the login command.  On Linux and MacOS, you can start the SSH agent with:  
`eval 'ssh-agent'`  
and add your private key by specifying it's full path and file name:  
`ssh-add /path/to/key/keyname`  

!!! Tip  
    If you set a passphrase when generating your SSH keypair, you will be prompted to enter it each time you login or just once when adding your key to the SSH agent.  This is NOT your CCR account password.  

To list the SSH keys currently loaded in your running SSH agent:  
`ssh-add -L`

See [below for Windows SSH agent](#using-the-mobaxterm-ssh-agent) setup using MobaXterm.  

### SSH Host Keys

The first time you log into a CCR login node you will be asked to verify the
host key.  It's a scary looking message and one you should not accept unless you know for sure the host has not been compromised:  

    The authenticity of host 'vortex (128.205.41.13)' can't be established.
    Are you sure you want to continue connecting (yes/no)?

To avoid having to accept the key for every CCR server you login to, you can add our certificate to the known_hosts file in your .ssh directory on your local machine:  

    @cert-authority *.ccr.buffalo.edu ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCjpY9sffG1O2xqrtRr+FZN73UNTrLtMO6uNMhymX4heJu8SLuMT69a4lkwLxuYfDm0IeM0JiOjCuiSWKIr34Iqj7wo3ksn46Mfa/B8V7EuOXu5HJ/w4pPefLvxH+gZBF1FRTQHfe5LVZh1ue2RPBose5rl0Y0/H6oLEfJW3O/1Vd2opPP7uFR416Ba94r2f5dJCUyPS+21lDti1fwVoz6yEGZzJ8WfoawDTRGGoRvO2lYOomq0tF2GkHhRDwe+UszlsYzhj+TpWG1cPKiygEJ0ey+cwjidkZPVfvDgtHGm9Q0CXc4mPcGiJhyl4MYtp4N4FhYLkTeDIb8t1F8lmhEDlu5cV0cB+B1cPgjVP4z9m1CYe+2TgkzCI3JStGlI9SCCXuSry4xZn3CZAB8dyQ/Iffw4BaZMisH+RALATvHoBfGS47t+SYbPKuB5663nhJrA7aj0wEA2FiYLheLiHr3picU9NBpX9cQ8OKD4KxMxghKbxxoErWA31tqDUsqQngOl8VN5XqhudqCmUToAlg/7W6cfZH/MK4h5SW17xEMkVQ11TId8pBf1gWmMAjSDTDLRGNx3LCK8snDmJvEkpxD/ADBuicve1HIZ2le/9655eD6IioM59MB30be6aLG6COSv4kBu5q3cohEFetAXiahnxyzuuKE1gIgff4osepbwUQ==  

### Logging in using MacOS

Logging in with a Mac requires no extra installation on your local machine.  Simply utilize the terminal application that is pre-installed with your operating system to access CCR resources.

Under “File” open a new finder window. Navigate to the “Applications” folder, then the “Utilities” folder. Open a terminal window and type the command:  
`ssh -i keyname username@vortex.ccr.buffalo.edu`

where `keyname` is the name and location of your SSH private key and `username` is your CCR username.  Press `Enter`.

To use a key loaded in a running SSH agent when logging in, use the following command:  
`ssh -A username@vortex.ccr.buffalo.edu`  

### Logging in from Linux

Linux machines require no additional software to access CCR.  Simply utilize the your Linux terminal that is pre-installed with youroperating system to access CCR resources.

Open a terminal window and type the command:  
`ssh -i keyname username@vortex.ccr.buffalo.edu.edu`

where `keyname` is the name and location of your SSH private key and `username` is your CCR username.  Press `Enter`.  

To use a key loaded in a running SSH agent when logging in, use the following command:  
`ssh -A username@vortex.ccr.buffalo.edu`  

### Logging in from Windows

There is no SSH client pre-installed in Windows so CCR users will need to install one.  CCR recommends [MobaXterm](https://mobaxterm.mobatek.net/) for command line and
simple file transfer access and [FileZilla](https://filezilla-project.org/) for more advanced file transfers.   

#### Setting up MobaXterm Session  

Follow [these instructions](../portals/idm.md#special-ssh-key-info-for-windows-users) for creating a SSH key pair using MobaXterm and upload the public key to your CCR account using the identity management portal.  Then setup MobaXterm to use the matching private key when connecting to CCR's login node.  

Launch MobaXterm again and create a new session following these steps:  

1. Click the Session button, then click the SSH icon

See the highlighted sections in the screenshot below to make sure you enter all the correct info.

2. Enter remote host (server name)  
`vortex.ccr.buffalo.edu`

3. Click the "specify username" checkbox and enter your CCR username

4. Ensure the port is 22

5. Make sure the "X11 Forwarding" box is UNCHECKED  

6. Click the "Use private key" box and browse to where you saved your private key ending in .ppk to select it

7. Click the "Bookmark settings" tab and enter a session name which allows you to save all these settings for easy launch in the future.  

![Moba](../images/mobasession.PNG)

Click OK and this will launch the session.  You should be logged into the system without having to enter your password.  

!!! Tip  
    If you set a passphrase when generating your SSH key pair, you will be prompted to enter it when starting the session.  This is NOT your CCR password.  

To re-connect in the future, you only need to double click on the session name or right-click on it and choose `Execute`  If you need to change any settings, right-click on the session name and choose `Edit session`  

#### Using the MobaXterm SSH Agent  

Rather than entering your SSH key passphrase every time you login, you can use the MobaXterm agent to load the private key once and use it for all SSH connections.  In MobaXterm, click on the `Settings` menu, select `Configuration` then click on the `SSH` tab.  

See the highlighted sections in the screenshot below to make sure you enter all the correct info.

1.  Check the box for `SSH keepalive`  
2.  Uncheck the boxes for `X11 forwarding` and `Forward SSH agents`  
3.  Check the box for `Use internal SSH agent "MobAgent"`  
4.  Click the plus symbol to browse to the location of your SSH private key and select it to add to the MobaXterm Agent.  If you set a passphrase when generating your SSH key pair, you'll be asked to enter it now.  

![Moba](../images/mobaagent.PNG)
