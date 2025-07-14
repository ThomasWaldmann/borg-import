What is borg-import?
====================

borg-import converts backups made with other backup software into the format used by `BorgBackup <https://github.com/borgbackup/borg>`_.

See ``borg-import -h`` for more information.

Potential advantages over manually doing it
===========================================

Note: we have different importers and some importers may not support all the features.

- automation: less manual work, import lots of backups into a borg repo with one command
- automatically makes up borg archive name from what you give + discovered timestamp
- sets borg archive creation timestamp to the historically correct date/time
- temporarily moves the source directory so the borg files cache will speed up borg create

Currently supported import formats
==================================

`BorgBackup <https://github.com/borgbackup/borg>`_
--------------------------------------------------

Imports archives from an existing Borg repository into a new one.
This is useful when a Borg repository needs to be rebuilt (e.g. if
your borg key and passphrase was compromised).

Usage: ``borg-import borg SOURCE_REPOSITORY DESTINATION_REPOSITORY``

See ``borg-import borg -h`` for help.

`rsnapshot <https://github.com/rsnapshot/rsnapshot>`_
-----------------------------------------------------

Usage: ``borg-import rsnapshot SNAPSHOT_ROOT BORG_REPOSITORY``

See ``borg-import rsnapshot -h`` for help.

Simple rsync with hard links
----------------------------

Assumes one folder per archive, with changes being tracked based on last modification time (mtime).

Usage: ``borg-import rsynchl RSYNC_ROOT BORG_REPOSITORY``

See ``borg-import rsynchl -h`` for help.

`rsync-time-backup <https://github.com/laurent22/rsync-time-backup>`_
---------------------------------------------------------------------

Similar to `rsynchl`, except with timestamp extraction optimized for `rsync-time-backup` folder names.

Usage: ``borg-import rsync_tmbackup --prefix=foo- RSYNC_ROOT BORG_REPOSITORY``

See ``borg-import rsync_tmbackup -h`` for help.

Backup tools based on rsync with hard links
-------------------------------------------

borg-import should, in principle, be able to import backups from any backup tool that is
based on rsync with hard links. This requires that the tool matches the assumptions listed above for simple
rsync.

* `backintime <https://github.com/bit-team/backintime>`_

* others?
