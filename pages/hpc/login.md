# Logging In

CCR offers a variety of resources for researchers to use in their own projects.
To get started with CCR resources you need the following:

- A CCR user account
- An active allocation in ColdFront
- Two-factor authentication
- An ssh client

Users accessing CCR's resources will be connected to a login node. A login node
is a outward facing node within CCR that users can connect to from their local
machines. Once on a login node, users can perform a limited number of tasks:

- Edit files
- Transfer Data
- Running Jobs
- Access storage resources

!!! note
    The login node policy states that login nodes should not be used for
    resource-intensive tasks such as running code. For all other tasks, users
    should run batch jobs, interactive jobs, or use the compile nodes.

![type:video](https://www.youtube.com/embed/g6hWYooFKWE)

## Getting an account

UB faculty, staff, and students can create a CCR account using the CCR identity
management portal.  CCR uses Globus as a trusted identity provider to verify a
potential user's identity and their status at the University at Buffalo.
Globus is a secure, reliable research data management service used by
institutions all over the world.  Globus provides a platform for application
integration and gateway development leveraging advanced identity management,
single sign-on, search and authorization capabilities.  Globus will redirect
you to login to UB's systems to make this verification.  This process is
similar to using your Facebook or Google account to login to a website, except
we are using Globus as the trusted provider.  You only need to do this one
time, when you are requesting the creation of a new CCR account.

## Logging in from a Windows Machine

Access to most CCR servers is only available through SSH or the  OnDemand
portal.  If you do not use the OnDemand portal, you must install a SSH client
on your computer.  CCR recommends the MobaXterm program for command line and
file transfer access and FileZilla for file transfers.

!!! note "VPN Required"

    You must be on the UB or Roswell Park networks to connect to most CCR
    servers.  If you are off-campus, please use the UB VPN to connect

Windows users can download [PuTTY](#) or [MobaXTerm](#) for command-line access to the
CCR servers. For graphics rendering with putty, use in conjunction with Xming.
Instructions for connecting using a PuTTY and Xming combination are available
here (Note: use the connection information below in lieu of "ctm.geo.mtu.edu"
in the example).  To check that the PuTTY/Xming combination is working
correctly: launch a putty terminal after separately launching xming as a
background task. Now type "xclock" from the putty terminal. If you get a
display error, it's not working. If a clock pops up then you know it's working
properly.

!!! tip "MobXTerm is recommended" 

    MobXTerm does not require additional software for graphics rendering and it
    is, therefore, recommended over PuTTY.


Users must use SSH keys to connect to CCR servers using SSH/SFTP/SCP.  Please
follow these instructions to upload your SSH key to the CCR identity management
portal before attempting to connect to CCR's servers.

## Logging in from a Mac

Logging in with a Mac requires no extra installation on your local machine.
Simply utilize the terminal application that is pre-installed with your
operating system to access CCR resources.

1. Ensure you have ssh keys setup

2. Under “File”, open a new finder window. Navigate to the “Applications”
  folder, then the “Utilities” folder. Open a terminal window and type ssh
  `username@vortex.ccr.buffalo.edu.edu`, where `username` is your CCR username.
  Press enter.

## Logging in from Linux

Much like with Macs, Linux machines require no additional setup to access CCR.
Simply utilize the your Linux terminal to access CCR resources.

1. Ensure you have ssh keys setup

2. Open a terminal window and type ssh `username@vortex.ccr.buffalo.edu.edu`,
   where `username` is your CCR username.

## SSH host keys

The first time you log into an CCR login node you will be asked to verify the
host key. You can refer to the keys published here to confirm that you are
connecting to a valid CCR login node.

Note that each login node may support more than one type of key, but only one
is used (or displayed) by your client at any given time.
