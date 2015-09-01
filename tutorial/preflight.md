Preflight checklist
===================
We will use the ceph-deploy tool to install the necessary packages on each
node and deploy each Ceph daemon. First, we need to prepare the nodes for deploying the Ceph cluster.

Connect to ceph-5, the admin node:

    ssh gks@<public ip ceph-5>

Add the Ceph release key and repository:

    wget --no-check-certificate -q -O- 'https://ceph.com/git/?p=ceph.git;a=blob_plain;f=keys/release.asc' | sudo apt-key add -
    echo deb http://ceph.com/debian-firefly/ $(lsb_release -sc) main | sudo tee /etc/apt/sources.list.d/ceph.list

Update your repository and install ceph-deploy:

    sudo apt-get update && sudo apt-get install ceph-deploy

On all nodes, ntp and openssh-server must be installed.

Now we need to setup passwordless ssh between the admin node and all other nodes, because the ceph-deploy tool needs to install packages without prompting for passwords.

Because of the Openstack deployment with floating IPs, we will use the private
network between the VMs for our Ceph cluster. 

* first, get the private IP of each VM by connecting to the public IP and executing:

        ifconfig

* on ceph-5, add the hostnames in /etc/hosts corresponding to these IPs:

        <private ip ceph-1>    ceph-1
        <private ip ceph-2>    ceph-2
        <private ip ceph-3>    ceph-3
        <private ip ceph-4>    ceph-4
        <private ip ceph-5>    ceph-5

**Note: Throughout this tutorial, you should use the hostnames of YOUR virtual machines.**

We will use the gks user to deploy the Ceph cluster, which already has sudo privileges without password required (root is NOT recommended):

* generate ssh keys on admin node

        ssh-keygen

* from the admin node, copy the key to each ceph node; use the IPs and passwords you received:

        ssh-copy-id gks@ceph-1
        ssh-copy-id gks@ceph-2
        ssh-copy-id gks@ceph-3
        ssh-copy-id gks@ceph-4
        ssh-copy-id gks@ceph-5

* modify the ~/.ssh/config file on the admin node so that you can login to the ceph nodes without requiring the username:

        Host ceph-1
          User gks
        Host ceph-2
          User gks
        Host ceph-3
          User gks
        Host ceph-4
          User gks
        Host ceph-5
          User gks

* now check that you can connect to the nodes without requiring a password or username:

        ssh ceph-1

Next, we will learn how to deploy a Ceph cluster [>>>](deploy.md)
