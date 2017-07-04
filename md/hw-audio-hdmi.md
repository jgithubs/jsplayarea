# Hardware, Audio thru HDMI device

[Hardware, Installation](md/hw-project.md)

## Links

* Adafruit Product, 10.1" 136x768 Display, https://www.adafruit.com/product/2261
* Pi Audio Configuration, https://www.raspberrypi.org/documentation/configuration/audio-config.md
* HDMI Modes, http://forum.photonic3d.com/t/raspberry-pi-cea-and-dmt-modes/49
* RPiConfig, http://elinux.org/RPiconfig

## Device Information

```
pi> tvservice -n
VGA to HDMI, device_name=DEL-DELL_1704FPT
Auto HDMI,   device_name=RTK-LT-32X575
```


## Video Information

```
pi> tvservice -s
VGA to HDMI, state 0x120006 [DVI DMT (35) RGB full 5:4],   1280x1024 @ 60.00Hz, progressive
Auto HDMI,   state 0x12000a [HDMI CEA (5) RGB lim 16:9],   1920x1080 @ 60.00Hz, interlaced
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

## TTY Information

```
pi> stty size
VGA to HDMI, 64 160
Auto HDMI,   61 228, (24 80, SSH)
Adafruit,    48 170
SSH,         24  80
VGA-to-HDMI, 32 80, VGA to HDMI
```

Audio Information

Display all the controls
```
pi> amixer controls
 numid=3,iface=MIXER,name='PCM Playback Route'
 numid=2,iface=MIXER,name='PCM Playback Switch'
 numid=1,iface=MIXER,name='PCM Playback Volume'
 numid=5,iface=PCM,name='IEC958 Playback Con Mask'
 numid=4,iface=PCM,name='IEC958 Playback Default'
The order is 3,2,1,5. The IEC958 is SPDIF (Surround Sound) output.
```
Display all the contents
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
Blah