# raspbian-ua-netinst-ro
An installation of debian that creates a read only system

Intended to be used with [raspbian-ua-netinst](https://github.com/debian-pi/raspbian-ua-netinst)

Basically, what happens is that ```/var``` gets moved to ```/var_orig```, ```/var_rw``` is created and mounted as a tmpfs. After this a unionfs is created, so reads from ```/var``` really are "served" from ```/var_orig```, and writes go to ```/var_rw```. In case anything is written to a location, it's read from the ```*_rw``` location.

Possible improvements:

 * Disable journal
 * create writable partitions, so state is preserved, add a boot time check to recreate the filesystem if a problem is found with the writable partitions
 * ```mount_unionfs``` could be made in a more robust fashion
 * ```/var_orig``` should be cleaned out as much as possible
 * write scripts to remount the system read-write and back to read-only
 * Documentation
 * ...

Contributions are welcome, of course :wink: 

## Temporarily enable write:
One can issue the following command (same thing for /boot) to gain temporary write access to the filesystem (note that /var will still be mounted in a tmpfs, so changes there will be lost!):

`(sudo) mount -o remount,rw /`

when done writing changes, remount it ro again:

`(sudo) mount -o remount,ro /`
