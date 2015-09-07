Solution for erasure coding exercise
===============================

Experiment with fault tolerance by comparing what happens when one vs two OSDs
break:

* get the list of OSDs where object *ecfile* is placed

        ceph osd map ecpool ecfile

* stop the first OSD

        on osd.2: service ceph stop osd

* try to dowload the object from the Ceph cluster using *rados get*

        rados -p ecpool get ecfile obj-fail1
        diff ecfile obj-fail1

* stop the second OSD

        on osd.3: service ceph stop osd
    
* try to download the object again

        rados -p ecpool get ecfile obj-fail2

What do you observe?

    Downloading the file worked when 1 OSD broke down, but was hanging when the second OSD failed.

Can you explain why this happens?

    Due to our chosen ec profile (m=1), only one failure is tolerated.
    Increasing m would improve reliability.

