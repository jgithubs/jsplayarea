# Hardware, Audio thru HDMI device

[Hardware, Installation](hw-project.md)

## Links

* Adafruit Product, 10.1" 136x768 Display, https://www.adafruit.com/product/2261
* Pi Audio Configuration, https://www.raspberrypi.org/documentation/configuration/audio-config.md
* HDMI Modes, http://forum.photonic3d.com/t/raspberry-pi-cea-and-dmt-modes/49
* RPiConfig, http://elinux.org/RPiconfig

## HDMI Connection

The Raspberry Pi has a HDMI connection to connect to a monitor. 
In this case using a HDMI monitor with speaker requires no hookup of physical speakers.
The audio and video is transmitted in the single HDMI cable.

## Adafruit Monitor

The project monitor is using a [10.1" Monitor from Adafruit](https://www.adafruit.com/product/2261).
When the Raspberry Pi is connected to the monitor, the text is too small to read.
Other HDMI monitor that are larger in size did not exhibit this problem.

To fix the Adafruit Monitor text size issue, edit the /boot/config.txt with the sudo command.
```
sudo vi /boot/config.txt
```
Add the 6 lines to the end of the file.
One line is a comment and 5 lines are the actual settings.
```
# Support for the Adafrit monitor
hdmi_force_hotplug=1
hdmi_drive=2
hdmi_group=2
hdmi_mode=81
config_hdmi_boost=4
```
For the changes to take effect, reboot the Raspberry Pi as an administrator.
```
sudo reboot
```

## HDMI Information

### Device Information

The following will provide the device name.
The last two are two HDMI sources.
```
pi\>  tvservice -n
VGA to HDMI,  device_name=DEL-DELL_1704FPT
Auto HDMI,    device_name=RTK-LT-32X575
HDMI to HDMI, device_name=ACI-ASUS-VH238
```


### Video Information

```
pi>  xtvservice -s
VGA to HDMI, state 0x120006 [DVI DMT (35) RGB full 5:4],   1280x1024 @ 60.00Hz, progressive
Auto HDMI,   state 0x12000a [HDMI CEA (5) RGB lim 16:9],   1920x1080 @ 60.00Hz, interlaced
HDMI to HDMI,state 0x12000a [HDMI CEA (16) RGB lim 16:9],  1920x1080 @ 60.00Hz, progressive
Adafruit,    state 0x12000a [HDMI DMT (81) RGB full 16:9], 1366x768  @ 60.00Hz, progressive
CEA (Entertainment devices, used by VGA),
```
```
HMDI_GROUP=1
RGB black level of 16 (in a 0-65535 range)

DMT (Standards for montors)

HDMI_GROUP=2
CEA modes have an RGB black level of 16 (in a 0-65535 range), whereas DMT modes have an RGB black level of 0.
This is for backwards compatibility with some ancient NTSC settings, where black level 0 is used to indicate a vertical blanking frame and can cause NTSC processing of interlaced images to go haywire if some parts of the image also have black level 0.
pi> tvservice -m DMT
Group DMT has 9 modes:
mode 4: 640x480 @ 60Hz 4:3, clock:25MHz progressive
mode 6: 640x480 @ 75Hz 4:3, clock:31MHz progressive
mode 9: 800x600 @ 60Hz 4:3, clock:40MHz progressive
mode 11: 800x600 @ 75Hz 4:3, clock:49MHz progressive
mode 16: 1024x768 @ 60Hz 4:3, clock:65MHz progressive
mode 18: 1024x768 @ 75Hz 4:3, clock:78MHz progressive
mode 21: 1152x864 @ 75Hz 4:3, clock:108MHz progressive
(prefer) mode 35: 1280x1024 @ 60Hz 5:4, clock:108MHz progressive
mode 36: 1280x1024 @ 75Hz 5:4, clock:135MHz progressive

pi> tvservice -m CEA
Group CEA has 0 modes:
```

### TTY Information

The [TTY](http://www.linusakesson.net/programming/tty/index.php) setting is the number of characters with and height wise in a linux shell.
There are times where not enough characters are display and excessive wrapping occurs.
```
pi> stty size
VGA to HDMI, 64 160
Auto HDMI,   61 228, (24 80, SSH)
Adafruit,    48 170
SSH,         24  80
VGA-to-HDMI, 32 80, VGA to HDMI
```

### Audio Information

Display all the controls.
```
pi> amixer controls
 numid=3,iface=MIXER,name='PCM Playback Route'
 numid=2,iface=MIXER,name='PCM Playback Switch'
 numid=1,iface=MIXER,name='PCM Playback Volume'
 numid=5,iface=PCM,name='IEC958 Playback Con Mask'
 numid=4,iface=PCM,name='IEC958 Playback Default'
The order is 3,2,1,5. The IEC958 is SPDIF (Surround Sound) output.
```

Display all the content.
```
pi> amixer contents
numid=3,iface=MIXER,name='PCM Playback Route'
 ; type=INTEGER,access=rw------,values=1,min=0,max=2,step=0
 : values=0
numid=2,iface=MIXER,name='PCM Playback Switch'
 ; type=BOOLEAN,access=rw------,values=1
 : values=on
numid=1,iface=MIXER,name='PCM Playback Volume'
 ; type=INTEGER,access=rw---R--,values=1,min=-10239,max=400,step=0
 : values=-1725
 | dBscale-min=-102.39dB,step=0.01dB,mute=1
numid=5,iface=PCM,name='IEC958 Playback Con Mask'
 ; type=IEC958,access=r-------,values=1
 : values=[AES0=0x02 AES1=0x00 AES2=0x00 AES3=0x00]
numid=4,iface=PCM,name='IEC958 Playback Default'
 ; type=IEC958,access=rw------,values=1
 : values=[AES0=0x00 AES1=0x00 AES2=0x00 AES3=0x00]
```