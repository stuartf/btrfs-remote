btrfs-remote
============

This is a not very user friendly script to do regular incrimental backups with `btrfs send` it's meant to work along side https://github.com/jf647/btrfs-snap

To use it you need to have a user on the remote machine that has sudo access to the btrfs command with no password. Then do a full `btrfs send` of your first snapshot. Then you can have a cron.daily script that does something like:

    !/bin/sh

    /opt/btrfs-snap/btrfs-snap -r /home 1d 7
    /opt/btrfs-remote/btrfs-remote /home ' \.snapshot/1d' backup@192.168.1.99 /var/backup/srcmachine 7

The arguments are `src` `prefix` `ssh destination` `destination subvolume` and `number of snapshots to keep`. This might change in the future to be more friendly as `prefix` is actually a combination of the source directory and prefix from `btrfs-snap`.

Note that because of a bug in `btrfs send` this currently only works with the btrfs root mounted somewhere and a clearly marked `HACK` in the script. I intend to fix this when btrfs-tools is fixed.
