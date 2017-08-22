# Hardware, Mount a USB stick

[Hardware, Installation](hw-project.md)

## Links

*Mount various usb sticks, https://raspberrypi.stackexchange.com/questions/41959/automount-various-usb-stick-file-systems-on-jessie-lite
*Auto mounting usb, http://posts.danharper.me/raspberry-pi-2-auto-mount-usb/

## Obtain USB device information

Before a USB stick can be mounted, the device name needs to be obtained.
* Insert USB stick into USB port
* The following statement will write out the last few lines in the log file.
Type CNTRL-C to break out of the statement.
The device is displayed as 'sda1'
```
pi> tail -f /var/log/messages
May 15 13:07:31 raspberrypi kernel: [ 3574.312148] usb 1-1.2: SerialNumber: 20042400530CBF40D94D
May 15 13:07:31 raspberrypi kernel: [ 3574.331486] usb-storage 1-1.2:1.0: USB Mass Storage device detected
May 15 13:07:31 raspberrypi kernel: [ 3574.332192] scsi host0: usb-storage 1-1.2:1.0
May 15 13:07:32 raspberrypi kernel: [ 3575.333048] scsi 0:0:0:0: Direct-Access SanDisk Cruzer Switch 1.26 PQ: 0 ANSI: 5
May 15 13:07:32 raspberrypi kernel: [ 3575.337412] sd 0:0:0:0: [sda] 15633408 512-byte logical blocks: (8.00 GB/7.45 GiB)
May 15 13:07:32 raspberrypi kernel: [ 3575.339263] sd 0:0:0:0: [sda] Write Protect is off
May 15 13:07:32 raspberrypi kernel: [ 3575.340225] sd 0:0:0:0: [sda] Write cache: disabled, read cache: enabled, doesn't support DPO or FUA
May 15 13:07:32 raspberrypi kernel: [ 3575.369501] sda: sda1
May 15 13:07:32 raspberrypi kernel: [ 3575.376712] sd 0:0:0:0: [sda] Attached SCSI removable disk
May 15 13:07:32 raspberrypi kernel: [ 3575.409148] sd 0:0:0:0: Attached scsi generic sg0 type 0
```
* Another method of identification is the following command.
The actual device is '/dev/sda1'.
The format type is 'vfat'
```
pi> sudo blkid
/dev/sda1: UUID="A843-0FD9" TYPE="vfat"
```
* The commands provide numerous information
```
Device: /dev/sda1
UUID  : A843-0FD9
Type  : vfat
```

## Another USB Stick

This usb stick has a number of partitions. The partition of interest is the /dev/sda1
```
pi> sudo blkid
/dev/mmcblk0p1: LABEL="boot" UUID="0F5F-3CD8" TYPE="vfat" PARTUUID="ec6ba75b-01"
/dev/mmcblk0p2: UUID="0aed834e-8c8f-412d-a276-a265dc676112" TYPE="ext4" PARTUUID="ec6ba75b-02"
/dev/sda1: UUID="E241-A542" TYPE="vfat" PARTUUID="30ed0dca-01"
/dev/mmcblk0: PTUUID="ec6ba75b" PTTYPE="dos"
```

* The commands provide numerous information
```
Device: /dev/sda1
UUID  : E241-A542
Type  : vfat
```

## Mount a USB device
Determine a directory name and create it with 'sudo'. 
In this case, the name is "mnt" that is typically created in the 'media' directory.
```
pi> sudo mkdir /media/mnt
```

Key attributes was obtained when the device was queried.
* Mount the drive passing the type, group, device name and the mount directory name.
Verify the mounting with the 'df' command.
```
pi> sudo mount -t vfat -o uid=pi,gid=pi /dev/sda1 /media/mnt

pi> df
Filesystem     1K-blocks    Used Available Use% Mounted on
/dev/root       30583756 1313548  27997888   5% /
devtmpfs          218256       0    218256   0% /dev
tmpfs             222540       0    222540   0% /dev/shm
tmpfs             222540    4524    218016   3% /run
tmpfs               5120       4      5116   1% /run/lock
tmpfs             222540       0    222540   0% /sys/fs/cgroup
/dev/mmcblk0p1     63503   20604     42899  33% /boot
/dev/sda1        7812864 5704800   2108064  74% /media/mnt
```
* Test the read and write ability
```
pi> cd /media/mnt
pi> echo "boo" > hi.txt
pi> cat hi.txt
boo
pi> rm hi.txt
```

## UnMount a USB stick
To release the mount, use 'sudo' with the 'unmount' command.
```
pi> cd $HOME

pi> sudo umount /media/mnt

pi> df
Filesystem     1K-blocks    Used Available Use% Mounted on
/dev/root       30583756 1313548  27997888   5% /
devtmpfs          218256       0    218256   0% /dev
tmpfs             222540       0    222540   0% /dev/shm
tmpfs             222540    4524    218016   3% /run
tmpfs               5120       4      5116   1% /run/lock
tmpfs             222540       0    222540   0% /sys/fs/cgroup
/dev/mmcblk0p1     63503   20604     42899  33% /boot
```

## Automounting a USB stick
Define the auto mount by entering the device information in a booting up file.

* There is one line to add and the usb stick should be in the Raspberry Pi usb port.
Editing this file requires 'sudo' privilages.
```
pi> sudo vi /etc/fstab
UUID=A843-0FD9 /media/mnt vfat auto,users,rw,uid=1000,gid=100,umask=0002 0 0 
```
* Test the entry by calling the auto mount command manually.
Prove that the USB stick was mounted by displaying the filesystems.
```
pi> sudo mount -a

pi> df
Filesystem     1K-blocks    Used Available Use% Mounted on
/dev/root       30583756 1313548  27997888   5% /
devtmpfs          218256       0    218256   0% /dev
tmpfs             222540       0    222540   0% /dev/shm
tmpfs             222540    4524    218016   3% /run
tmpfs               5120       4      5116   1% /run/lock
tmpfs             222540       0    222540   0% /sys/fs/cgroup
/dev/mmcblk0p1     63503   20604     42899  33% /boot
/dev/sda1        7812864 5704800   2108064  74% /media/mnt
```
* Unmount the drive then pull out the USB stick.
* Put the USB stick back in and verify that it is mounting automatically.
* This procedure is for one specific USB stick.
Automounting any USB stick will be studied later.

NOTE: There is an issue that will cause the OS image not to boot.
If the OS is shutdown with the USB stick, the boot up process remembers this.
The OS boot up will fail and state that the root account is locked.
The solution is to put the USB stick back into the port and reboot.
If you want the OS to reboot without the USB stick, then unmount the stick manually.
Then shutdown the Raspberry Pi.