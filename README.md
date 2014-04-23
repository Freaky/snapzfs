snapzfs
=======

Yet another ZFS auto-snapshot script. You probably don't want to be using it yet.
Unfinished, untested, untidied.


Features
--------

 * Driven almost entirely by ZFS user attributes.
 * One cronjob.
 * All snapshot types share a namespace.  Just @auto.yyyy-mm-ddThh:mm:ssZ
 * UTC or death.
 * Destroys unnecessary empty snapshots.
 * Kicks puppies.
 * Self-contained script. No gems, just stock Ruby 2.0+ and its standard library.
 * Probably won't cause data loss.  Probably.


Usage
-----

    snapzfs policy "4 * 15 minutes; 24 hourly; 7 daily; 4 weekly" tank
    snapzfs disable tank/junk
    snapzfs enable tank/junk/important
    snapzfs policy "7 daily" tank/media
    echo "*/15 * * * * root /path/to/snapzfs auto" >>/etc/crontab

Keeps four snapshots at 15 minute intervals, 24 at hourly intervals, 7 at daily
intervals, and 4 at weekly intervals.  `snapzfs list` to view them. `snapzfs nuke`
to get rid of them all.

Use "zfs hold" for any snapshots you want to keep.


ZFS Properties
--------------

    st.hur:snapshot.
                    policy      String    The snapshot policy.
                    auto        Bool      Whether this dataset is snapshotted.
                                  Note expirations happen regardless.
                    policies    String    The policies applied to this snapshot.
                    created_at  Integer   Unixtime this snapshot was made.
                    expires_at  Integer   Unixtime this snapshot expires.
                                  Not currently used.


TODO
----

 * Named snapshots with expiry dates.
 * Time/date based snapshots.  e.g. "7 midnight" for seven at or near 00:00.
 * Localtime.  '+' is an invalid snapshot name, which torpedoed my desire for
   ISO 8601 dates.
 * Test suite.
 * Refactor.  One monolithic file seemed like a good idea at the start.
   (And it probably still is for deployment).
 * Actually use OptionParser.
 * Documentation, license, etc.

