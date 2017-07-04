# Hardware Project

This page describes how to build all of the software componets to work with the selected hardware. It also contains some areas of research to get the software to work together.

## RASPBERRY PI (PI) Setup

* [Raspberry Pi 3](md/hw-pi3.md)
* [Raspberry Pi 2](md/hw-pi2.md)
* Version of the operating system.
  * Raspbian-Lite image with Jessie, http://downloads.raspberrypi.org/raspbian_lite/images/
    * January 2017, YES
    * April 2017, NO. Configuration do not work even after updates
  * 8GB card seems most reliable
  ```
pi> cat /etc/os-release
PRETTY_NAME="Raspbian GNU/Linux 8 (jessie)"
NAME="Raspbian GNU/Linux"
VERSION_ID="8"
VERSION="8 (jessie)"
ID=raspbian
ID_LIKE=debian
HOME_URL="http://www.raspbian.org/"
SUPPORT_URL="http://www.raspbian.org/RaspbianForums"
BUG_REPORT_URL="http://www.raspbian.org/RaspbianBugs"
  ```
* Determine how to install the Operating System image on the Raspberry Pi.
  * [Headless example](md/sw-headless.md) (No Gui). Small in size.
  * Front-end example (XWindow). Large in size
  * Create [Serial connection](md/hw-serial-connect.md) for serial login
  * Create [SSH server](md/sw-ssh-server.md) for remote login
  * Create [FTP server](md/sw-ftp-server.md) to transfer files
  * Determine the voltage of the input/output pins (based on the model). This needs to be known so that the correct breakout board and LCD display is selected.
* Determine how to get a RFID working
  * The RFID install numerous development tools, it is advised to get this functional first.
  * Get the [RFID RC522 breakout](md/hw-rfid-rc522.md) board working.
  * Insure that the board can read and write RFDI/NFC tags.
  * NFC is the latest technology. It can hold large amounts of data.
  * Need a physical button to put the breakout board in "write" mode?
    * Insert a usb stick
* Determine how to play audio without a GUI
  * Audio playback with [Music On Console](md/sw-audio-moc.md) (MOC)
  * Audio output [thru HDMI](md/hw-audio-hdmi.md)
  * Audio control is is handle by the [ALSA mixer](md/sw-audio-alsa.md)
  * Audio output control is handled by XXX
* Determine how to display pictures with a duration of time without GUI
  * Display pictures with [Frame Buffer ImageViewer](md/sw-frame-buf-img-viewer.md) (FBI)
  * Converting images to specific size to avoid load time and scaling time. Use [Imagemagick](md/sw-img-magick-tools.md) Tools
  * Use [symbolic links](md/sw-symbolic-link.md) to change pictures with the same filename.
* Determine how to run multiple sessions. Audio will play in the background and the picture in the front.
  * Multiple sessions with [screen tool](md/sw-session-screen.md).
    * One session is to run the FBI viewer
    * The other session is to run a script for the RFID reader and MOCP
  * Use 'top' to see cpu usage information.
* Determine how to transfer [developed software](md/sw-development.md).
  * Create [FTP server](md/sw-ftp-server.md) to transfer files
* Determine how to [mount a USB stick](md/hw-mount-usb.md).
  * This shall be auto mounted at boot up
  * This shall be automatically detected when inserted.
* Determine how to power-off with a button
  * TBD
* Determine how to image an entire boot SD
  * This is for backup purposes

## Other Research

This is research done early in the project. The feasibility did not workout mainly because a GUIless method was choosen.

* Determine how to [create a web server/site](md/sw-web-server.md) on the Pi.
  * The site will be local on the Pi access via local host.
  * The site is view-able from the LCD Screen (only with XWindows).
  * The site is view-able from another computer.
    * Use this as a front-end to download pictures?
  * The data downloaded on the site when the RFDI/NFC tag is triggered.
* Determine how to create playback functionality
  * Audio and Video capability? We need more like Audio with Pictures.
    * Pi Game example, https://learn.adafruit.com/raspberry-pi-pygame-ui-basics/overview
    * Pi Game install example, https://www.raspberrypi.org/forums/viewtopic.php?f=32&t=33157&p=332140&hilit=croston%2bpygame#p284266
    * JPEG source stream example, https://blog.miguelgrinberg.com/post/stream-video-from-the-raspberry-pi-camera-to-web-browsers-even-on-ios-and-android
  * Find and OS or source that supports playback.
  * Do we need to connect an external speaker?
* Audio playback from the webserver on the Pi
  * Using PHP
  * Using other
  * Using mpg123, https://learn.adafruit.com/playing-sounds-and-using-buttons-with-raspberry-pi/install-audio
  * Using omxplayer, http://www.raspberrypi-spy.co.uk/2013/06/raspberry-pi-command-line-audio/
* How to [run scratch on the Pi](md/sw-scratch.md)
  * Need to run headless, however, it seems that this may be an issue
  * Start a scratch program from command line.
* Determine how to enable the LCD display on the Pi.
  * 10.1" HDMI Display, ($189.00), https://www.adafruit.com/product/2261
* Find an OS
  * Supports the [tft lcd screen](md/hw-tft-lcd.md)
  * Supports [wifi connection](md/hw-wifi-connect.md)
  * Supports the Playback
    * Need Open codecs, http://www.cnx-software.com/2013/01/26/raspberry-pi-now-has-experimental-support-for-vp6-vp8-mjpeg-and-ogg-theora-video-codecs/
    * X, https://www.tmplab.org/wiki/index.php/Streaming_Video_With_RaspberryPi
    * X, https://www.oblivion-software.de/index.php?id=56&type=98

## RFDI/NFC

* Insure that the board is compatible to the voltage level of the PI.
  * Voltage converters can be used, however, it adds complexity
* Products
  * RFID/NFC, https://www.adafruit.com/products/36
  * http://www.allaboutcircuits.com/projects/read-and-write-on-nfc-tags-with-an-arduino/
  * https://learn.adafruit.com/adafruit-nfc-rfid-on-raspberry-pi
  * https://learn.adafruit.com/raspberry-pi-nfc-minecraft-blocks
  * https://www.raspberrypi.org/downloads/raspbian/
  * RFID, https://www.fasttech.com/products/0/10002711/1201004-jt500sak-serial-port-nxp-mifare-tag-rfid-rfic
    * PC Based
      * SDKs and sample codes available in Visual C, Visual Basic, and Delphi

## RFDI/NFC Tags

* The tags needs to be small enough to fit under the 3D part.
  * Dimension?
* The tags needs to support the proper frequency of the selected RFDI reader/writer.
* Prefer re-writable tag
* Low cost tags that work at a maximum of 3 inches (76.2mm). The minimum depends on the layout of the board (still to be determined).
* Products
  * RFID, https://www.sparkfun.com/products/9417
    * Highlights
      * Small
      * 125kHz
      * Max 32mm read distance
<img src=https://swittersb.files.wordpress.com/2009/12/sizing-mm-to-inch.jpg width=480>
https://swittersb.files.wordpress.com/2009/12/sizing-mm-to-inch.jpg
    * Lowlights
      * Not reprogrammable
      * Pricy (3.95 each)

  * NFC, https://www.alibaba.com/product-detail/ISO14443A-Programmable-NFC-Tag-Waterproof-Smart_60165209646.html
  * NFC, https://www.fasttech.com/products/0/10002690/1385005-rewritable-programmable-ntag203-nfc-tag-button
  * NFC, https://www.fasttech.com/products/0/10002690/1272200-ntag203-rewritable-programmable-nxp-mifare-nfc-sti
  * RFID, https://www.seeedstudio.com/13.56MHz-RFID-book-tag-p-1067.html
  * RFID, https://www.amazon.com/YARONGTECH-50pcs-MIFARE-Classic-adhesive-Sticker/dp/B01LZYOR7P/ref=sr_1_21?ie=UTF8&qid=1485206504&sr=8-21&keywords=rfid+tags

## Import Software

* Write a program/script to pull in the students data into PI
  * Create a top level web page
  * Create a preformatted web page from the student's data
    * Whole page as a single image?
    * Add music or dings/dongs?
  * Copy the files to the PI or read from a USB stick
    * Assign an associated RFDI tag ID
  * Allow the tag to be rewritten
  * Suggested Methods
    * https://dave.cheney.net/2015/09/04/building-go-1-5-on-the-raspberry-pi
    * https://dave.cheney.net/2012/09/25/installing-go-on-the-raspberry-pi

## Student Creation Software

* Expect the software to already exists
* Determine the files/formats of the files
  * Pictures
  * Audio
  * Should we create the web page here?

