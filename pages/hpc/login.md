# Login Node

Users accessing CCR's HPC resources will be connected to a login node. A login
node is a outward facing node within CCR's HPC environment that users can connect
to from their local machines. Once on a login node, users can perform a limited
number of tasks:

- Edit files
- Transfer Data
- Submitting Jobs
- Access storage resources

This page covers connecting to a login node using SSH (Secure Shell Protocol).
When you connect via SSH, you authenticate using a private key file on your
local machine. For more information about SSH, see [Secure Shell](https://en.wikipedia.org/wiki/Secure_Shell)
on Wikipedia. You can also connect to CCR's login nodes using a web browser with the [OnDemand Portal](../portals/ood.md).

!!! Note  
    Login nodes should not be used for resource-intensive tasks such as running
    software or compiling code. For those tasks, users should submit batch or
    interactive jobs to reserve a node in the cluster.   

To get started connecting to CCR's HPC clusters and shared storage you need the
following:

- A CCR user account with two factor authentication enabled and an active
  allocation to HPC resources. For more information see our [getting access](../getting-access.md) guide.
- [An SSH Key added to your account](#generate-new-ssh-key)
- An SSH client. Linux & MacOS include a terminal app. For Windows users, we recommend using [Git Bash](https://gitforwindows.org/)

!!! Warning "VPN Required"
    Access to CCR login nodes is restricted to UB and Roswell Park networks
    (either on campus or connected to their VPN services). [See here](../getting-access.md#vpn-access)

CCR login nodes hostnames:

- `vortex.ccr.buffalo.edu` - production login nodes
- `vortex-future.ccr.buffalo.edu` - includes new features and serves as a preview of the next deployment of production login nodes

## Connecting with SSH

Using the SSH protocol, you can connect and authenticate to CCR login nodes without supplying your password. To set up SSH, you will need to generate a new SSH key pair that contains a private key (stored only on your personal computer) and a public key (uploaded to your CCR account using the IDM portal).  During the login process the CCR servers attempt to match the public key that you've uploaded to your CCR account with the private key you have stored on your computer.  If they match, the login is successful.  

## Generate new SSH key

Prior to using SSH to connect to CCR's login servers, you'll need to generate a new SSH key pair on your local machine. If you connect to CCR from multiple devices, we recommend generating a separate SSH key pair for each device.  After you generate
the key pair(s), you must add the public key(s) to your account using [CCR's IDM portal](https://idm.ccr.buffalo.edu/sshkey).

Follow these easy steps:

1. Open your terminal or Git Bash if you're on windows

2. Run the following command, substituting in your email address:
    ```bash
    $ ssh-keygen -t ed25519 -C "myemailaddress@institution.edu"
    ```

3. At the prompt, type a secure passphrase

4. Copy the contents of the public key to your clipboard. The file is located here:
    ```bash
    ~/.ssh/id_ed25519.pub
    ```
5. Login to the [CCR IDM portal](https://idm.ccr.buffalo.edu) and click on [SSH Keys](https://idm.ccr.buffalo.edu/sshkey) in the left nav menu

6. Click on the "New SSH Key" button, paste the contents of your public key in the text box, and click "Add".

!!! Warning "Initial Wait Period"  
    After uploading your SSH key to the CCR portal, it will take 20-30 minutes to propagate our systems and allow you to login.   


## Using the SSH Agent  

Running an SSH agent process on your local machine allows you to load your SSH private key one time and it will be used for every SSH login attempt.  This
allows you to skip entering your SSH key passphrase each time you login and you will not have to specify your private key in the SSH login command.  Follow these steps to add your key to the ssh-agent:

1. Open your terminal or Git Bash if you're on windows

2. Start the ssh-agent in the background:

    ```bash
    $ eval "$(ssh-agent -s)"
    > Agent pid 12345
    ```

3. Add your SSH private key to the ssh-agent using the command below. If you
   created your key with a different name or location, use the correct path and
   filename to your private key. You will be prompted to enter your passphrase
   for the key.  NOTE: The SSH key passphrase is NOT your CCR password.  This
   is the passphrase you set when [creating your SSH key pair](#generate-new-ssh-key):  

    ```bash
    $ ssh-add ~/.ssh/id_ed25519
    ```

4. List the SSH keys currently loaded in your running SSH agent:  
    ```bash
    $ ssh-add -L
    ```

!!! Tip "Restarting the SSH Agent"  
    If you restart your computer, the SSH agent may not automatically restart.
    This varies by operating system so we recommend searching for online
    documentation on how to set this up.  You will need to supply the private
    key passphrase each time the agent restarts.  


## Logging in

Once you've uploaded your SSH public key to your CCR account you will be able to use the SSH protocol to connect to CCR's login nodes.  Follow these steps:

1. Open your terminal or Git Bash if you're on Windows and, if you're running a SSH agent as [described above](#using-the-ssh-agent), enter the following:  
    ```bash
    ssh [CCRusername]@vortex.ccr.buffalo.edu
    ```
   
    !!! Warning "Not using ssh-agent?"
        If you're not running a SSH agent [(see above)](#using-the-ssh-agent) you
        will need to specify the location and filename of your PRIVATE key using
        the `-i` option in the SSH command and you'll be prompted for your SSH key
        passphrase. This is NOT your CCR password. This is the passphrase you
        set when [creating your SSH key pair](#generate-new-ssh-key). For example:  
        ```bash
        ssh -i /path-to-key/id_ed25519 [CCRusername]@vortex.ccr.buffalo.edu
        Enter passphrase for key 'id_ed25519':
        ```

2. When logging into CCR's login nodes, you may see a warning message similar
   to this.  Verify the fingerprint in the message you see matches [CCR's
   public key fingerprint](../fingerprints.md).
   If it does, then type `yes`.  

    ```
    The authenticity of host 'vortex.ccr.buffalo.edu (128.205.41.24)' can't be established.
    ED25519 key fingerprint is SHA256:qYT1DzrHv8yTlHiNGV2td29309oXPHdN4OPj/KptFYg.
    Are you sure you want to continue connecting (yes/no/[fingerprint])?
    ```  

3.  If your login was successful, you should now be at a shell prompt on the
    login node:  

    ```
    CCRusername@login:~$
    ```

!!! Tip "First Login - Additional Setup"  
    On first login your home directory will be created automatically.  You
    will see a message indicating this has been done and an SSH key pair gets
    generated for use on the cluster.

## OnDemand for Web-Based Cluster Access  

[Open OnDemand](https://ondemand.ccr.buffalo.edu) provides access to CCR's
clusters, storage, visualization servers, and interactive apps.  CCR's OnDemand
portal offers Linux desktops for GUI-based applications, software applications
like MatLab, RStudio Desktop, Jupyter Notebook, and vscode, an interactive
development environment.  OnDemand can be used in any browser from almost any
device.  More information about OnDemand can be [found here](../portals/ood.md).  
