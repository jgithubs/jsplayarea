# Hardware, Mount a USB stick

[Hardware, Installation](hw-project.md)

## Images

* wget http://adafruit-download.s3.amazonaws.com/adapiluv320x240.jpg
* wget http://adafruit-download.s3.amazonaws.com/adapiluv480x320.png

## Setup

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

pi> sudo blkid
/dev/sda1: UUID="A843-0FD9" TYPE="vfat"
```

Determine a directory name and create it with 'sudo' . In this case, the name is "mnt"
```
sudo mkdir /media/mnt
```

Mount the drive passing the device and the directory name.
```
sudo mount -t vfat -o uid=pi,gid=pi /dev/sda1 /media/mnt
```

Test the read and write ability
```
echo "boo" > hi.txt
cat hi.txt
```

To un-mount the stick
```
sudo umount /media/mnt
```

Mount automatically using the UUID. There is one line to add.
```
sudo vim /etc/fstab UUID=A843-0FD9 /media/mnt vfat auto,users,rw,uid=1000,gid=100,umask=0002 0 0 
```