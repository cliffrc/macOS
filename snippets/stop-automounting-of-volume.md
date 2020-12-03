
# MacOS: Prevent auto-mounting of volume

- MacOS Version: 10.15.7 
- _Problem_: I wanted a thumb-drive re-formatted. After USB insertion the drive
  was auto-mounted (as per usual). When attempting to format via the `Disk
  Utility` (and `diskutil formatVolume ...`) neither were able to unmount the
  volume. `Force unmount` did not resolve.
- _Solution_: Prevent initial auto-mounting.

Attach the drive, which will trigger an auto-mount.

Then in `Terminal`:

```shell
# Copy the value of the long UUID_STRING (cmd-V) ...
$ diskutil info /Volumes/<VOLUME_NAME> | egrep "Volume (UUID|Name):"
   Volume Name:               <VOLUME_NAME>
   Volume UUID:               <UUID_STRING>
# Place the UUID_STRING value into /etc/fstab using ...
$ sudo vifs
# Place the UUID_STRING value here
UUID=<UUID_STRING> none msdos rw,noauto

```

Force-eject the mounted drive and reinsert. You will now be able to use `Disk
Utility` or `diskutil` to complete the formatting task.

