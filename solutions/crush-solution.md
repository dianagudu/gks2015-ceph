
Solution for CRUSH exercise
============================

Create the hierarchy below:

                  default
                     |
                   room1
            _________|_________
           |                   |
         rack1               rack2
       _____|_____        _____|_____ 
      |           |      |           |
    ceph-1     ceph-2  ceph-3     ceph-4
      |           |      |           |
     osd0       osd1    osd2        osd3

First, create new buckets for room and racks:

    ceph osd crush add-bucket room1 room
    ceph osd crush add-bucket rack1 rack
    ceph osd crush add-bucket rack2 rack

Then, move each host bucket to its parent rack:

    ceph osd crush move ceph-1 rack=rack1
    ceph osd crush move ceph-2 rack=rack1
    ceph osd crush move ceph-3 rack=rack2
    ceph osd crush move ceph-4 rack=rack2

Move the racks to the room1 bucket, and then the room bucket to the default
bucket:

    ceph osd crush move rack1 room=room1
    ceph osd crush move rack2 room=room1
    ceph osd crush move room1 root=default

Finally, create a new ruleset:

    ceph osd crush rule create-simple racky default rack

And change the settings of the pools to use the newly created ruleset:

    ceph osd pool set data crush_ruleset 1
    ceph osd pool set rbd  crush_ruleset 1
