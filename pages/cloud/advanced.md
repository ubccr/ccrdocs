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



