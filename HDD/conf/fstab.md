```
# /etc/fstab: static file system information.
#
# Use 'blkid' to print the universally unique identifier for a
# device; this may be used with UUID= as a more robust way to name devices
# that works even if disks are added and removed. See fstab(5).
#
# <file system> <mount point>   <type>  <options>       <dump>  <pass>
# / was on /dev/sda2 during installation
UUID=f778e737-e06c-4e6f-a3e9-ae70e9116684	/			ext4	errors=remount-ro 0       1
# /boot was on /dev/sda3 during installation
UUID=5424d353-e27e-4f82-a23a-0ce928241f41	/boot 		ext4	defaults	0		2
# /home was on /dev/sda7 during installation
UUID=a432ba96-eb78-4b20-b65d-1f03d3be61ef	/home		ext4	defaults	0		2
# /tmp was on /dev/sda5 during installation
UUID=5e7bb7f0-0700-43e3-b14c-3096f53ed85b	/tmp		ext4	defaults	0		2
# /var was on /dev/sda6 during installation
UUID=c4b25dd8-4e05-4afc-bfa8-4cb0b244768d	/var		ext4	defaults	0		2
# swap was on /dev/sda1 during installation
UUID=c9e4dd97-a0ef-45ad-b41d-b2e01e3aeb59 	none		swap	sw			0		0
LABEL=NAS /mnt/NAS auto nosuid,nodev,nofail,x-gvfs-show 0 0
```
