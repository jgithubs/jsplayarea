# Software, Using Imagemagick tools

[Hardware, Installation](md/hw-project.md)

## Links

Converting images on Pi, http://garyhall.org.uk/converting-images-on-raspberry-pi.html

Overlaying text on image, http://raspi.tv/2014/overlaying-text-and-graphics-on-a-photo-and-tweeting-it-pt-5-twitter-app-series

Command line for imagemagick, https://www.imagemagick.org/script/command-line-tools.php

Basic Usage, https://www.imagemagick.org/Usage/basics/#cmdline

## Installation

```
pi> sudo apt-get install imagemagick
```

Installs additional software

* convert
* identify
* magick (is not present)

## Convert image size

Giving the exact width. The height is adjusted accordingly.
```
pi> convert cover.jpg -resize 680 new-cover.jpg
```
Giving the exact height. The width is adjusted accordingly.
```
pi> convert cover.jpg -resize x480 new-cover.jpg
```
Giving the exact width and height. Notice the '!' for the size. The image may appear stretched.
```
pi> convert cover.jpg -resize 680×480! new-cover.jpg
```
Test image in using [FBI](md/sw-frame-buf-img-viewer.md) to verify that no "resizing" is ocurring.

## Image information

Displaying information about the image.
```
pi> identify a.jpg
a.jpg JPEG 3912x2000 3912x2000+0+0 8-bit sRGB 1.549MB 0.060u 0:00.159
pi> identify a-1000x511.jpg
a-1000x511.jpg JPEG 1000x511 1000x511+0+0 8-bit sRGB 136KB 0.060u 0:00.150
```
This file was converted from (width x height), 3912x2000 to 1000x511 in size.