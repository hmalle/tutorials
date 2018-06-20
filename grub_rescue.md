
# How to install grub2 using chroom on an lvm encrypted partition

#### Get the drive structure ,here Im assuming the boot partition is on /dev/sda1 and the LUKS/LVM encrypted partition is on /dev/sda5
```
fdisk -l /dev/sda/
  /dev/sda1 *boot 
  /dev/sda2/
  /dev/sda5/   (dmcrypt container)
```

#### Open the encrypted container with cryptsetup
```
  cryptsetup luksOpen /dev/sda5 chicken
```

#### Mount the encrypted container and the dev/sda1 
```
  mount /dev/mapper/chicken /mnt
  mount /dev/sda1 /mnt/boot
```

#### Now get the support folders from your base linux folder
```
  mount --bind /dev/ /mnt/dev/
  mount --bind /proc/ /mnt/proc/
  mount --bind /sys/ /mnt/sys/
```

#### Copy the network resolv.conf to the /mnt in order to be online when using chroot 
```
  cp /etc/resolv.conf /mnt/etc/resolv.conf
```

### Change root to /mnt
```
  chroot /mnt/
```

#### Purge grub2 and reinstall it again.
```
  apt-get purge grub*
  apt-get install grub2
  grub-install /dev/sda/
  update-grub2
```

#### If all goes well, you should see operating systems detected with the operating systems present
#### Exit out of chroot
```
  exit
```

#### Then its time to umount things
```
  umount /dev/sda1 /mnt/dev/ /mnt/proc/ /mnt/sys/
  umount /dev/mapper/chicken
  cryptsetup luksClose chicken
```

#### You can now restart the computer
```
  telinit 6
```

