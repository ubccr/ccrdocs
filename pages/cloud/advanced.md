# Advanced Topics



## Openstack CLI

OpenStackClient project provides a unified command-line client, which enables you to access the project API through easy-to-use commands. Also, most OpenStack project provides a command-line client for each service. For example, the Compute service provides a `nova` command-line client.

You can run the commands from the command line, or include the commands within scripts to automate tasks. If you provide OpenStack Application Credentials, you can run these commands on any computer that has access to the LakeEffect Dashboard.



Install the Openstack Command line tools

It is recommended to run the CLI from a Virtual Environment.

1. Create the Virtual Environment 

```bash
$ virtualenv ~/openstack-cli
$ source ~/openstack-cli/bin/activate
```

2. Install the Openstack Client Project

```bash
(openstack-cli) $ pip install python-openstackclient
```

3. Obtain the Openstack Application Credentials

> * Log onto the [The LakeEffect Dashboard (Horizon)](https://dashboard.cloud.ccr.buffalo.edu)
> * From the **Identity** Section on the left column click on `Application Credentials`
> * Click on `Create Application Credential`
> * Fill in the **Name** field and the rest may be left blank.
> * Click on the `Create Application Credential` button at the bottom
> * From the popup window click `Download openrc file`

!!! Warning
    The application credential secret will not be available after the popup, so you must capture it now or download it. If you lose this secret, you must generate a new application credential.

4. Source the openrc file that you just downloaded with the Application Credentials

```bash
(openstack-cli) $ source app-cred-openrc.sh
```

5. Test to make sure you can run a basic server list:

```bash
(openstack-client) $ openstack server list
+--------------------------------------+----------+--------+------------------------------------------------------+--------------------------+--------+
| ID                                   | Name     | Status | Networks                                             | Image                    | Flavor |
+--------------------------------------+----------+--------+------------------------------------------------------+--------------------------+--------+
| 2407495d-ea94-4676-8a18-18cd29cd516d | test-vm2 | ACTIVE | lakeeffect-demo-network=128.205.11.65, 192.168.1.151 | N/A (booted from volume) | c1.m4  |
| 3e22ef68-556a-4106-a56e-56674591fd8e | test-vm  | ACTIVE | ccr-public=128.205.11.52                             | N/A (booted from volume) | c1.m4  |
+--------------------------------------+----------+--------+------------------------------------------------------+--------------------------+--------+
```

The **python-openstackclient** project is a common client that supports most of the various Openstack Projects, however You may need to install an individual project’s client because coverage is not yet sufficient in the OpenStack client. For example, the **python-cinderclient** may be needed if less common cinder commands are needed. This is installed the same way as the python-openstackclient package was installed. For more information on the individual project clients go [here](https://docs.openstack.org/newton/user-guide/common/cli-install-openstack-command-line-clients.html).


## Useful Openstack Commands


List Images:

```
(openstack-client) $ openstack image list
+--------------------------------------+------------------------------------------------+--------+
| ID                                   | Name                                           | Status |
+--------------------------------------+------------------------------------------------+--------+
| f70d120e-89d7-4bef-a291-6db70406bd5b | CentOS 8-stream (x86_64) [2022-09-13]          | active |
| 78aa844e-ab92-43b1-b7e3-9f826b02e6cd | CentOS 9-stream (x86_64) [2022-09-19]          | active |
| bbc56d42-ec07-469a-b01b-33268c3040cf | Debian 10.13.4 (x86_64) [2022-10-13]           | active |
| 48d45cc8-4272-4f8f-9a93-b920056b41d0 | Fedora 36 Cloud Base (x86_64) [2022-05-04]     | active |
| f568aa5f-9b32-4182-ad9a-7afbee9e5c62 | Rocky Linux 8.6 (x86_64) [2022-07-02]          | active |
| 74c64db6-0a08-4fae-b462-469a0c15ab99 | Rocky Linux 9.0 (x86_64) [2022-08-30]          | active |
| 63754185-6872-40f1-8990-0bff66406b00 | Ubuntu 18.04 LTS (x86_64) [2022-10-14]         | active |
| cbaa2d71-7837-4322-9eba-94dfc44c2898 | Ubuntu 20.04 LTS (x86_64) [2022-10-18]         | active |
| 6b4041af-56df-4786-98ed-d3ede57ca901 | Ubuntu 22.04 LTS (x86_64) [2022-10-18]         | active |
+--------------------------------------+------------------------------------------------+--------+
```

List Volumes:

```
(openstack-client) $ openstack volume list
+--------------------------------------+------+-----------+------+-----------------------------------+
| ID                                   | Name | Status    | Size | Attached to                       |
+--------------------------------------+------+-----------+------+-----------------------------------+
| 16fec574-2f51-4c8a-9446-f146648edf31 |      | available |   20 |                                   |
| a77d9f3c-2576-4796-857d-eb70106221b1 |      | in-use    |   20 | Attached to test-vm2 on /dev/vda  |
| 61667b4e-b819-467c-8305-075678c83120 |      | in-use    |   20 | Attached to test-vm on /dev/vda   |
| 82a2e1c5-ce33-4bfe-a733-722705612363 |      | available |   20 |                                   |
+--------------------------------------+------+-----------+------+-----------------------------------+
```

Spin up a VM:

```bash
(openstack-client) $ openstack server create --flavor c1.m4 --image 'Ubuntu 22.04 LTS (x86_64) [2022-10-18]'  --network ccr-public --key-name sguercio --security-group My_Security-Group My_Test_VM
```

Upload an Image to Openstack:

```bash
(openstack-client) $ openstack image create --container-format bare --disk-format qcow2 --progress --public --file cirros-0.6.1-x86_64-disk.img 'CirrOS 0.6.1 (x86_64) [2022-11-22]'
```

## Private Networking

Creating Private Network:

```bash
    $ openstack network create my-private-net
```

Create a Subnet:

```bash
    $ openstack subnet create --network my-private-net --dns-nameserver 1.1.1.1 --gateway 192.168.10.1 --subnet-range 192.168.10.0/24 my-private-subnet
```

Create a Router:

```bash
    $ openstack router create my-private-router
```

Add the Router to the Subnet:

```bash
    $ openstack router add subnet my-private-router my-private-subnet
```

Connect the router to the public network. This is optional if you want to be able to route packets to the internet. It is outbound only.

```bash
    $ openstack router set --external-gateway ccr-public my-private-router
```

Create a new VM on the network to test.

```bash
    $ openstack server create --flavor c1.m4 --image 'Ubuntu 22.04 LTS (x86_64) [2022-10-18]' --nic net-id=my-private-net --key-name mykeypair --security-group mysecgroup --wait Test-VM-1
```

Attach a Floating IP address to the VM if you want it to have an IP address on the public network.

```bash
    $ FIP=`openstack floating ip create -f value -c floating_ip_address ccr-public`
    $ openstack server add floating ip mytestvm1 $FIP
```

Ensure the proper security groups are created for SSH access to the VM. You should now be able to SSH into this machine from the public network. This VM has access to both the public and private and will act as the login host for all other VMs on the private network only.

You can now create additional VMs on the Private network and they will all be accessable to each other over this network and have outbound Internet access if you set the --external-gateway.

**NOTE: You do not need to create security group rules for private networks.  
All traffic is allowed by default.**



```bash
    $ openstack server create --flavor c1.m4 --image 'Ubuntu 22.04 LTS (x86_64) [2022-10-18]' --nic net-id=my-private-net --key-name mykeypair --security-group mysecgroup --wait Test-VM-2
```


```bash
    $ openstack server list
    +--------------------------------------+-----------+--------+-----------------------------------------------+----------------------------------------+--------+
    | ID                                   | Name      | Status | Networks                                      | Image                                  | Flavor |
    +--------------------------------------+-----------+--------+-----------------------------------------------+----------------------------------------+--------+
    | ef2e79b8-9e95-4a80-946b-f36f3d5d2cb5 | Test-VM-2 | ACTIVE | my-private-net=192.168.10.136                 | Ubuntu 22.04 LTS (x86_64) [2022-10-18] | c1.m4  |
    | 461d98cc-f5db-4973-871e-c9f1f87aeb6b | Test-VM-1 | ACTIVE | my-private-net=128.205.11.111, 192.168.10.147 | Ubuntu 22.04 LTS (x86_64) [2022-10-18] | c1.m4  |
    +--------------------------------------+-----------+--------+-----------------------------------------------+----------------------------------------+--------+
```

```bash
Test connectivity on the Private Network:

    $ ssh ubuntu@128.205.11.111
    Welcome to Ubuntu 22.04.1 LTS (GNU/Linux 5.15.0-52-generic x86_64)
    
     * Documentation:  https://help.ubuntu.com
     * Management:     https://landscape.canonical.com
     * Support:        https://ubuntu.com/advantage
    
      System information as of Tue Apr 18 14:44:31 UTC 2023
    
      System load:  0.0               Processes:             89
      Usage of /:   7.3% of 19.20GB   Users logged in:       0
      Memory usage: 5%                IPv4 address for ens3: 192.168.10.147
      Swap usage:   0%
    
    
    0 updates can be applied immediately.
    
    
    The list of available updates is more than a week old.
    To check for new updates run: sudo apt update
    
    Last login: Tue Apr 18 14:22:40 2023 from 68.133.101.31
    To run a command as administrator (user "root"), use "sudo <command>".
    See "man sudo_root" for details.

    ubuntu@test-vm-1:~$ ping -c 3 192.168.10.136
    PING 192.168.10.136 (192.168.10.136) 56(84) bytes of data.
    64 bytes from 192.168.10.136: icmp_seq=1 ttl=64 time=0.332 ms
    64 bytes from 192.168.10.136: icmp_seq=2 ttl=64 time=0.234 ms
    64 bytes from 192.168.10.136: icmp_seq=3 ttl=64 time=0.336 ms
    
    --- 192.168.10.136 ping statistics ---
    3 packets transmitted, 3 received, 0% packet loss, time 2054ms
    rtt min/avg/max/mdev = 0.234/0.300/0.336/0.047 ms
    ubuntu@test-vm-1:~$ 
```
