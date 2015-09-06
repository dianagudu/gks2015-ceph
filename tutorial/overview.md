Overview
=========

You will all receive access information to 5 virtual machines to be used for
this tutorial, named **ceph-${studentid}-[1-5]**. You have to use the
associated public IPs to connect to them, as the hostnames are not registered
with any DNS server.

Test that you can connect using the username *gks* and the password you
received:

    ssh gks@<IP>

We will use host *ceph-${studentid}-5* as admin node: this VM will not be part
of the cluster, but rather act as client connecting to the storage cluster or
administrator issuing commands to create and configure the Ceph cluster.

We will therefore have the following roles assigned for each machine:

* **ceph-${studentid}-5**: admin node, Ceph client
* **ceph-${studentid}-1**: Ceph monitor, Ceph OSD
* **ceph-${studentid}-2**: Ceph monitor, Ceph OSD
* **ceph-${studentid}-3**: Ceph monitor, Ceph OSD
* **ceph-${studentid}-4**: Ceph metadata server, Ceph OSD

**Note** that in production clusters, it is not recommended to run multiple
Ceph daemons on the same machine, to make it more resilient to failures.
Moreover, there are specific
[hardware](http://ceph.com/docs/master/start/hardware-recommendations/) and 
[OS](http://ceph.com/docs/master/start/os-recommendations/) 
requirements for each Ceph daemon, in order for the Ceph system to run smoothly.

We will start with [preparing the nodes](preflight.md) for deploying the Ceph cluster.
