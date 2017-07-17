# Student, Create Project

The create part of the project is to have the student put together a series of pictures with audio.
The audio can be a selected piece of music on the web or a recorded narration on their subject.
This collection is the content that will be transferred to the Raspberry Pi and associated with a RFID tag.

* Audio
  * This file is an MP3 file. The audio will be played when the series of pictures is displayed.
The audio will stop when the last picture display time ends.
* Pictures
  * This file is an JPG file.
The display time is configured by the student.
The sum of the display time should be less than the length of the audio.
* RFID Tag
  * An RFID Tag is Radio Frequency Identification tag. 
It is similar to a barcode where data is stored in th tag. 
Each tag has a unique identification number.
To obtain the number, the RFID tag needs to be swiped across a RFID reader.

When the RFID tag is swiped across the RFID reader, the associated audio will play along with associated picture(s).
Each picture is displayed for a specified duration (in seconds).
When the last picture is displayed at its duration, the audio will be stopped.
The monitor will display a default image with default music.

## RFID Tag Association

Each student is given a RFID tag.
The RFID tag needs to be swiped against the reader to obtain the RFID number.
The content will then be transfered to the Raspberry Pi.

### Create Content in Windows

* One MP3 file (other format types are not yet supported) is required.
* One or more JPG file (other format types are not yet supported) is required.
  * This image shall be 640x480 in widthXheight size (for Adafruit Monitor).
  * There is [software on the Raspberry Pi](sw-img-magick-tools.md) that can scale down the image.
This can also be done on the PC when the image is created.
* A USB stick is required to import the images into the Raspberry Pi.
This USB stick is assumed to be [setup to automount](hw-mount-usb.md) when inserted into the Raspberry Pi.
* Put files in a directory structure shown below on the USB stick.
It is suggested not to use uppercases.
The Raspberry Pi is case sensitive, therefore, using one case (lowercase) helps with debugging.
```
  import -+--- default
          |
          +--- sally
          |
          +--- joe
```
* Create a text file called hList.txt.
* The text file will list one MP3 file and N JPG file(s).
```
  Format:
  <Audio>,<Min>:<Sec>  <Picture>,<Sec>   <Picture>,<Sec> ... <EOL>
```
  * Audio filenames shall end with a ".mp3". It is always the first in the list.
  * Picture filenames shall end with a ".jpg"
  * The sum of the picture seconds shall be equal to or less than the audio (in seconds).
  * In the case below, the audio file is 2 minutes and 30 seconds.
    The file has three pictures.
    The first picture will play for 5 seconds, the second 4 seconds and the third 3 seconds.
```
pi> cat hList.txt
hFile1.mp3,2:30 hFile1.jpg,5 hFile2.jpg,4 hFile3.jpg,3
```
  * The text file, audio file and image file(s) shall exists in the same directory as the media files.

### Transfer content via a USB stick

The best way to transfer files into the Raspberry Pi is files on a USB stick.

* Login into the raspberry pi
* Insert the USB stick (the specific usb port does not matter).
* Verify that the USB stick is present.
In this case the USB stick is /media/mnt.
```
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
* Run a special script that reads from the USB stick.
Do not be concerned if a runtime error occurs about the MFRC522 library.
  * A list of directories in the 'Src Root' will be displayed.
  * The user will be prompted to select a directory to import. This is directories on the USB stick.
  * The user will be prompted to scan their RFID tag.
At this time, place the RFID tag againest the RFID reader.
```
pi> cd $HOME
pi> ./readUsb.py

-----
Dst Root         : /home/pi/data
Src Root         : /media/mnt/import
--
Src Default      : default
Dst Default      : ffffffffff
--
Rfid Default List: hList.txt
-----

Welcome to the Rfid directory setup

Select directory to import
1 . default
2 . Joe
3 . Sally
Option: 2
/home/pi/src/MFRC522-python/MFRC522.py:113: RuntimeWarning: This channel is already in use, continuing anyway.  Use GPIO.setwarnings(False) to disable warnings.
  GPIO.setup(22, GPIO.OUT)

Ready for RFID scan
Press Ctrl-C to stop.
-----
RFID-Status: Detected
RFID-Uid: 0xe196718b8d
Size: 8
Sector 8 [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
RFID-Auth: MI_OK

User Name: Joe
aRootDir : /media/mnt/import
aSubDir  : Joe
aTextFile: hList.txt
Line     = four-winds-web.mp3,2:10 01-images.jpg,5 02-LctVT.jpg,5 03-raspberry-pi-2-pinout.jpg,5 04-Fig-12-Raspberry-Pi-Components-Explanation.jpg,5 05-images.jpg,5
Elements = 6
four-winds-web.mp3,2:10
/media/mnt/import/Joe/four-winds-web.mp3
01-images.jpg,5
/media/mnt/import/Joe/01-images.jpg
02-LctVT.jpg,5
/media/mnt/import/Joe/02-LctVT.jpg
03-raspberry-pi-2-pinout.jpg,5
/media/mnt/import/Joe/03-raspberry-pi-2-pinout.jpg
04-Fig-12-Raspberry-Pi-Components-Explanation.jpg,5
/media/mnt/import/Joe/04-Fig-12-Raspberry-Pi-Components-Explanation.jpg
05-images.jpg,5
/media/mnt/import/Joe/05-images.jpg
Validated source file(s)

Rfid Tag : e196718b8d
aRootDir : /home/pi/data
aSubDir  : e196718b8d
aTextFile: hList.txt
Warning, file path ( /home/pi/data/e196718b8d ) does not exists.
Validated destination. Destination does not exists.

Copy over selected data? y
/media/mnt/import/Joe:/home/pi/data/e196718b8d/
cp -r /media/mnt/import/Joe /home/pi/data/e196718b8d/
Done
```
  * The source data will be validated. This is data on the USB stick.
  * The destination will be validated not to exist.
  * The user will be prompted to copy files over.

Run the command again for the next users.

If the RFID tag needs to be removed, the validation of the destination will fail.
The user will be asked if this directory should be removed, answer "yes".
When asked to copy over files, answer "no".
This should remove the tag from the system.

The "default" users is the default music/picture. This should only be done by the instructor.

### Transfer content using FTP

Transfering content via FTP requires a network connection.
This will be described later.