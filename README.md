GridKa School 2015 - Ceph tutorial
==================================

### Description

Ceph is an open-source, software-defined distributed storage system that
strives to achieve scalability and reliability through an innovative
decentralised design.
Distributed file systems nowadays face multiple challenges: scaling to
peta-byte capacity and providing high performance, while protecting against
failures. Moreover, file systems should be able to adapt to dynamic distributed
workloads to provide the best performance. Ceph tries to tackle these
challenges with a completely decentralised architecture that has no single
point of failure. Reliability is achieved through distributed data placement
and replication. Ceph's dynamic metadata partitioning feature helps deal with
dynamic workloads.

This session is an introduction to Ceph and it will cover theoretical
background on Ceph's architecture, as well as hands-on exercises, such as
installation and configuration of a Ceph cluster, simple usage and monitoring.
After completing this session, you should be able to understand and discuss
Ceph concepts, and deploy and manage a Ceph Storage Cluster.

### Required skills

Basic knowledge of Linux and storage concepts is required.

### Technical requirements for the course

For installing and running Ceph we will use virtual machines provided by the GridKA School.

On your personal laptop, you will only need:

* an ssh client to connect to the VMs - if you're using
Linux or Mac, this is already installed; on Windows, I would recommend
[PuTTY](http://www.putty.org/).
* a web browser to access the course material on
  [github](https://github.com/dianagudu/gks2015-ceph).
* **optionally**: a git client, if you wish to clone the course material and
  view it locally.

### Table of contents

* Introduction to Ceph ([pdf slides](presentation/presentation.pdf?raw=true))
* [Tutorial overview](tutorial/overview.md)
* [Preparing the nodes](tutorial/preflight.md)
* [Deploying a Ceph storage cluster](tutorial/deploy.md)
* [Basic usage of the Ceph cluster](tutorial/operate.md)
* [CRUSH](tutorial/crush.md)
* [CephFS](tutorial/cephfs.md)
* [RBD](tutorial/rbd.md)
* [Erasure coding](tutorial/erasure.md)
* [Troubleshooting](tutorial/troubleshooting.md)

