# Software, File Transfer Protocol (FTP) Server

[Hardware, Installation](hw-project.md)

## Links

* How to setup Pi Ftp, https://pimylifeup.com/raspberry-pi-ftp/

## Transfer of files

There is a need to transfer audio files to test. There is an option to transfer the files to a USB stick and then access it through the Pi, however, it is sometime convenient to transfer the files using FTP.

Install the package
```
sudo apt-get install vsftpd
```

Change the ftp configuration file.
```
cd /etc
sudo vi vsftpd.conf
```

From the default settings, found that two lines needed to be uncommented.
```
write_enable=YES
local_umask=022
```

Two lines needed to be added then saved.
```
user_sub_token=$USER
local_root=/home/$USER/ftp
```

A FTP directory needs to be created (in the user account) to enable the user to transfer files. The permissions to the first directory needs to be changed. When transferring files into Pi, it can only be transferred into the 'files' directory, not the 'ftp' directory.
```
cd $HOME
mkdir ftp
mkdir ftp/files
chmod a-w $HOME/ftp
```

Restart the ftp service.
```
sudo service vsftpd restart
```

From a PC, attempt to transfer a file into the Raspberry Pi.  When the login is successful, the current directory is 'ftp'. The user has to specifically move to the 'files' directory before transferring the file.
```
ftp <IP address>
ftp user> pi
ftp password> <password>
ftp> !dir
ftp> cd files
ftp> put filename.txt
ftp> ls
ftp> quit
```
Verify on the Pi side that the file was transferred.