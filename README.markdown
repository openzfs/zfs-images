This repository contains a collection of ZFS pools which are intended
to be used as reference images.  The goal is to ensure that there are
representative samples from all the major ZFS implementations.  It is
also desirable that these images encompase the myriad of optional states
in which a pool can exist.

Each of the images described below is maintained as a compressed tarball
which includes the vdevs needed to describe a pool.  When contributing a
new image care should be taken to minimize its size.  Effective techniques
for minimizing the image include sparse files for vdevs, writing highly
compressible data patterns, and using the 'tar --sparse' and  'bzip2 --best'
options.  Finally, each new image must be briefly described in this file.


Name                  | Version | Description
-------------         | ------- | ------------------------------------------------
zol-0.6.1             | v5000   | Created with ZoL v0.6.1
                      |         | 
                      |         | The pool was created with all default settings and
                      |         | populated with a few hundred files and directories.
                      |         | It includes a snapshot and clone of the filesystem
                      |         | which has been modified from the original.  The pool
                      |         | has been scrubbed once and was cleanly exported.
                      |         |
zol-0.6.2             | v5000   | Created with ZoL v0.6.2
                      |         | 
                      |         | This pool was created in same way as the zol-0.6.1
                      |         | pool described above.
                      |         |
zol-0.6.2-173         | v5000   | Created with ZoL zfs-0.6.2-173-g881f45c
                      |         |
                      |         | Pools which have been imported with this version of
                      |         | ZoL and scrubbed or resilvered cannot be imported by
                      |         | older versions of ZFS.  This was accidentally caused
                      |         | by https://github.com/zfsonlinux/zfs/issues/2094 and
                      |         | this pool was created for future reference.  New ZoL
                      |         | versions must be able to import the pool and fix it.
                      |         | It was created the same was as the zol-0.6.1 pool.
                      |         |
zevo-1.1.1            | v28     | Created with ZEVO v1.1.1
                      |         |
                      |         | This pool was created to illustrate differences in
                      |         | the on disk format of a ZEVO pool.  In particular,
                      |         | https://github.com/zfsonlinux/zfs/issues/1911
                      |         | describes how neither an "external ACL" (ZNODE_ACL)
                      |         | nor a new-style DACL_ACES SA are created.  One of
                      |         | these is required by all other ZFS implementations.
                      |         |
bptree_obj-zol-0.6.2  | v5000   | Created with ZoL v0.6.2
                      |         |
                      |         | This pool was created to illustrate one of the many
                      |         | states in which a valid exported pool may exist.
                      |         | It contains the optional "bptree_obj" entry in the
                      |         | MOS object directory which points to an object of
                      |         | type DMU_OTN_UINT64_METADATA containing a pair of
                      |         | bptree_entry_phys_t entries; one for each of a
                      |         | pair of filesystems for which a deferred destroy is
                      |         | pending.  Although ZoL 0.6.2 was used to create this
                      |         | pool, it was custom-modified to not process the
                      |         | deferred destroy list in order to create this pool
                      |         | cleanly.  The pool's name is "tank" and it contained
                      |         | a pair of filesystemes, "tank/fs1" and "tank/fs2",
                      |         | each of which contained a single small file.  The
                      |         | deferred destroy object and its object's data were
                      |         | created by destroying both of these filesystems.
