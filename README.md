# raspbian-ua-netinst-ro
An installation of debian that creates a read only system

Intended to be used with [raspbian-ua-netinst](https://github.com/debian-pi/raspbian-ua-netinst)

Basically, what happens is that ```/etc``` and ```/var``` get moved (with ```/etc``` links are created, otherwise the first boot after install will fail) to ```/etc_orig``` and ```/var_orig```, ```/etc_rw``` and ```/var_rw``` are created and mounted as a tmpfs. After this a unionfs is created, so reads to ```/etc``` (or ```/var```) come from ```/etc_orig``` (or ```/var_orig```), and writes go to ```/etc_rw``` (or ```/var_rw```). In case anything is written to a location, it's read from the ```*_rw``` location.

Possible improvements:

 * Disable journal
 * create writable partitions, so state is preserved, add a boot time check to erase if a problem is found with the writable partitions
 * ```mount_unionfs``` could be made way more robust
 * Documentation
 * ...

Contributions are welcome, of course :wink: 
