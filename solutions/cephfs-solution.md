CephFS Exercise
===============

Let's simulate storing a performance sensitive directory to a pool that is
stored on SSDs. We want to stripe files over 8MB RADOS objects and write 4 files 
of different sizes to this directory (8 MB, 20 MB, 24 MB, 36 MB). How many
objects are there in the new pool?

First, create new pool:

    ceph osd pool create cephfs_ssddata 64

Add it as a data pool for cephfs:

    ceph mds add_data_pool cephfs_ssddata
    ceph fs ls

Create new directory:

    sudo mkdir /mnt/cephfs/ssd

Change directory layout to be stored in new pool:

    sudo setfattr -n ceph.dir.layout.pool -v cephfs_ssddata /mnt/cephfs/ssd
    getfattr -n ceph.dir.layout /mnt/cephfs/ssd

Change striping settings:

    sudo setfattr -n ceph.dir.layout.object_size -v 8388608 /mnt/cephfs/ssd/
    getfattr -n ceph.dir.layout /mnt/cephfs/ssd

Write the 4 files:

    sudo dd if=/dev/urandom bs=8M  count=1 of=/mnt/cephfs/ssd/file1
    sudo dd if=/dev/urandom bs=20M count=1 of=/mnt/cephfs/ssd/file2
    sudo dd if=/dev/urandom bs=24M count=1 of=/mnt/cephfs/ssd/file3
    sudo dd if=/dev/urandom bs=36M count=1 of=/mnt/cephfs/ssd/file4

Check the objects stored in the pool:

    $ rados -p cephfs_ssddata ls | wc -l
    12

    $ rados -p cephfs_ssddata ls
    1000000000f.00000002
    1000000000e.00000002
    1000000000f.00000003
    1000000000d.00000002
    1000000000f.00000000
    1000000000e.00000001
    1000000000f.00000004
    1000000000d.00000000
    1000000000c.00000000
    1000000000f.00000001
    1000000000d.00000001
    1000000000e.00000000
