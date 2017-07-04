# Software, Audio with Alsa Mixer

[Hardware, Installation](md/hw-project.md)

## Links

Sound configuration with Pi and ALSA drivers, http://blog.scphillips.com/posts/2013/01/sound-configuration-on-raspberry-pi-with-alsa/

Command Line Audio, http://www.raspberrypi-spy.co.uk/2013/06/raspberry-pi-command-line-audio/

## Alsa Information

Setting the volume is best done using 'alsamixer'. A mini-GUI comes up and the volume can be changed by using the up and down arrows. The default setting is '44'.
```
pi> alsamixer
 Card: bcm2835 ALSA
 Chip: Broadcom Mixer
 View: F3[Playback] F4:Capture F5:All
 Item: PCM [dB gain: -17.25]
```
```
F2 System information
/proc/asound/cards
0 [ALSA]: bcm2835 - bcm2835 ALSA
                    bcm2835 ALSA
```

## Get current information using 'amixer'

```
pi> amixer scontrols
Simple mixer control 'PCM',0
pi> amixer scontents
Simple mixer control 'PCM',0
 Capabilities: pvolume pvolume-joined pswitch pswitch-joined
 Playback channels: Mono
 Limits: Playback -10239 - 400
 Mono: Playback -1726 [80%] [-17.26dB] [on]
```
## Audio control using 'amixer'

The audio levels can be controlled by setting the percentage.

Get the current levels:
```
pi> amixer
 Simple mixer control 'PCM',0
 Capabilities: pvolume pvolume-joined pswitch pswitch-joined
 Playback channels: Mono
 Limits: Playback -10239 - 400
 Mono: Playback -1725 [80%] [-17.25dB] [on]
```
Set the new level and check the results:
```
pi> amixer sset PCM,0 90

pi> amixer
 Simple mixer control 'PCM',0
 Capabilities: pvolume pvolume-joined pswitch pswitch-joined
 Playback channels: Mono
 Limits: Playback -10239 - 400
 Mono: Playback 90 [97%] [0.90dB] [on]
```

## Reset the audio to default levels

If settings were entirely messed up, reset back to the default values:
```
pi> sudo /etc/init.d/alsa-utils reset
[ok] Resetting ALSA....done.

pi> amixer
Simple mixer control 'PCM',0
 Capabilities: pvolume pvolume-joined pswitch pswitch-joined
 Playback channels: Mono
 Limits: Playback -10239 - 400
 Mono: Playback -1726 [80%] [-17.26dB] [on]
```
