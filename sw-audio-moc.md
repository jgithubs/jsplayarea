# Software, Music on Console (MOC)

[Hardware, Installation](hw-project.md)

[Alsa Audio](sw-audio-alsa.md)

## Links

https://www.raspberrypi.org/forums/viewtopic.php?t=43108

http://superdecade.blogspot.co.uk/2016/01/music-on-console-for-raspberry-pi.html

Free Sound Effects, SoundBible, http://soundbible.com/free-sound-effects-1.html

3MU Examples, Wikipedia, https://en.wikipedia.org/wiki/M3U

Documentation, http://moc.daper.net/documentation

Ubuntu mocp manual, http://manpages.ubuntu.com/manpages/xenial/man1/mocp.1.html

RavanSpi, http://dalliard.net/files/ravenispi.php

Autums Child, Mark Holland, http://autumnschild.com/index.html

## Audio Files

Download example files by typing the commands below or using a [SSH connection](sw-ssh-server.md).
Simple copying of the links below into the SSH connection.

```
cd $HOME
mkdir data
cd data

wget http://www.freespecialeffects.co.uk/soundfx/household/bubbling_water_1.mp3

wget http://www.freespecialeffects.co.uk/soundfx/sirens/police_s.wav

wget http://www.freespecialeffects.co.uk/soundfx/computers/bleep_01.wav
```

## Install package(s)

```
sudo apt-get install moc
```

## Status Commands

```
pi> mocp --info
FATAL_ERROR: The server is not running!

pi> mocp --info
State: STOP

pi> mocp --info
State: PLAY
File: /home/pi/Music/Animals/FrogsInTheForest-SoundBible.mp3
Title:
Artist: SoundBible.com
SongTitle:
Album:
TotalTime: 00:06
TimeLeft: 00:04
TotalSec: 6
CurrentTime: 00:02
CurrentSec: 2
Bitrate: 112kbps
AvgBitrate: 148kbps
Rate: 44kHz
```

## Server Commands

```
pi> mocp --server
Running the server...
Trying JACK...
Trying ALSA...
pi> mocp --server
FATAL_ERROR: Server is already running!

pi> mocp --exit
FATAL_ERROR: The server is not running!
pi> mocp --exit
Play/Stop Commands

pi> mocp --stop
FATAL_ERROR: The server is not running!
pi> mocp --stop
```

## Playback - Single file

```
pi> mocp -c -a -p /home/pi/Music/Animals/cow2.wav

pi> mocp --clear --append --info --play /home/pi/Music/Animals/cow2.wav
State: PLAY
File:
Title:
Artist:
SongTitle:
Album:
TotalTime:
TimeLeft:
TotalSec:
CurrentTime:
CurrentSec:
Bitrate:
AvgBitrate:
Rate:
```

## Playback - From playlist

There is a bug with the playlist will sort the list in alphabetical order, then play, therefore, name files alphabetically to get desired order.
```
pi> cat seta.m3u
 /home/pi/Music/Animals/cow2.wav
 /home/pi/Music/Animals/ZoodpeckerCall-SoundBible.mp3
 /home/pi/Music/Animals/FrogsInTheForest-SoundBible.mp3
 /home/pi/Music/Animals/BlackbirdBirdCall-SoundBible.mp3
```
Play the playlist
```
pi> mocp --clear --append seta.m3u --play
Playback - From directory

pi> cat seta.m3u
/home/pi/Music/Animals/cow2.wav
/home/pi/Music/Animals/ZoodpeckerCall-SoundBible.mp3
/home/pi/Music/Animals/FrogsInTheForest-SoundBible.mp3
/home/pi/Music/Animals/BlackbirdBirdCall-SoundBible.mp3

pi> mocp --clear --append seta.m3u --play
```

## Adjusting Audio Levels

MOCP does not seem to adjust levels as described.
Another method is to use ALSA commands directly.

## Convert Audio

```
sudo apt-get install mpg123
```

```
mpg123 -w dst.wav src.mp3
```

### Convert MP3 to WAV



### Convert WAV to MP3