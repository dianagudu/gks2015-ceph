Deploying a Ceph cluster
========================

Now let's start deploying a Ceph cluster, using the set-up description in the
slides:

* ceph-1: mon, osd
* ceph-2: mon, osd
* ceph-3: mon, osd
* ceph-4: mds, osd
* ceph-5: admin

First, create a directory on the admin node for maintaining all the
configuration files and keys that ceph-deploy generates during the
installation process:

    mkdir my-cluster
    cd my-cluster

Next, create the cluster by specifying the initial monitor nodes:

    ceph-deploy new ceph-1 ceph-2 ceph-3

Note the files created by ceph-deploy in the current directory. You can modify
the settings in ceph.conf, for example by setting the public network (in our case, private)
and the default number of replicas in Ceph to 2 instead of 3:

    public network = <private network of VMs>
    osd pool default size = 2

Now install ceph on all nodes:

    ceph-deploy install ceph-1 ceph-2 ceph-3 ceph-4 ceph-5

This will take some time...

After the installation is finished, add the initial monitors and gather the
keys:

    ceph-deploy mon create-initial

Once you complete the process, you should have the following keyrings in your
current directory:

    ceph.client.admin.keyring
    ceph.bootstrap-osd.keyring
    ceph.bootstrap-mds.keyring
    ceph.bootstrap-rgw.keyring

The *ceph.client.admin.keyring* allows you to operate the cluster as admin user
if passed to the *ceph* command with *-k*. To copy the admin key to a node so
that you don't need to use the *-k* argument, execute the command:

    ceph-deploy admin ceph-5
    chmod +r /etc/ceph/ceph.client.admin.keyring

Check the status of the monitors with:

    ceph mon stat

Next, we will deploy the 4 OSDs. We will use an entire disk (/dev/vdb), that
will be partitioned by ceph-deploy into 2 partitions: journal and data.

    ceph-deploy osd prepare ceph-1:/dev/vdb ceph-2:/dev/vdb ceph-3:/dev/vdb ceph-4:/dev/vdb

However, Ceph supports any location in the filesystem as location for journal
and data.

To activate the OSDs, execute:

    ceph-deploy osd activate ceph-1:/dev/vdb ceph-2:/dev/vdb ceph-3:/dev/vdb ceph-4:/dev/vdb

Check the status of the Ceph cluster with:

    ceph -s

Check the hierarchy of OSDs and their status (up/down/in/out) with:

    ceph osd tree

Next, we will deploy the MDS which will be used for CephFS:

    ceph-deploy mds create ceph-4

We now have a fully functioning Ceph cluster.

[Next: Operating a Ceph cluster >>](operate.md)
