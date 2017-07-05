# Software, SSH Server Setup

[Hardware, Installation](hw-project.md)

[Software, Headless](sw-headless.md)

## Notables

Insure that the image has been update. SSH is know not to start automatically if this is not done.
```
sudo apt-get update
```

## SSH Server Enable

Enabling SSH is done using the configuration tool. Check the status of the service after turning on and after the reboot.

```
pi> sudo raspi-config
Advanced Option->SSH, enable

pi> sudo service ssh status
pi@raspberrypi:~ $ sudo service ssh status
ssh.service - OpenBSD Secure Shell server
   Loaded: loaded (/lib/systemd/system/ssh.service; enabled)
   Active: active (running) since Thu 2017-06-22 05:08:35 UTC; 1min 22s ago

pi> sudo reboot
```

## SSH commands

There are multiple commands to fiddle with the ssh service.

```
pi> sudo service ssh status
pi> sudo /etc/init.d/ssh status
pi> sudo /etc/init.d/ssh start
pi> sudo /etc/init.d/ssh stop
pi> sudo update-rc2.d ssh defaults
pi> sudo update-rc2.d ssh enable
```

## Login using SSH

The communication tool requires the IP address of the Raspberry Pi.
The port is most always Port 22.
Insure that your ethernet cable is attached.
Use ipconfig to obtain the address.
See [Ethernet instructions](hw-ethernet-connect.md) instructions for more information.

![](img/PuttySsh.jpg)

Once the connection is made, a login screen should appear.

![](img/PuttyScreen.jpg)