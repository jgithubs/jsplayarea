# Software, Frame Buffer ImageViewer (FBI)

[Hardware, Installation](md/hw-project.md)

[Software, Headless](md/sw-headless.md)

## Links

Wall Display without XWindow, http://www.instructables.com/id/Raspberry-Pi-Wall-Display-Without-X-Windows/

Photo Frame, http://blog.jacobean.net/?p=941

Using symbolic link with viewer, https://raspberrypi.stackexchange.com/questions/24180/how-can-i-refresh-image-displayed-by-fbi-without-black-screen-transition

Execute in script with kill, https://unix.stackexchange.com/questions/138198/how-to-display-a-jpg-file-using-fbi-in-a-bash-script-for-set-amount-of-time-and

## Files

```
cd $HOME
cd data

wget http://adafruit-download.s3.amazonaws.com/adapiluv320x240.jpg
wget http://adafruit-download.s3.amazonaws.com/adapiluv480x320.png
wget http://art110.wikispaces.com/file/view/Mystery-100x100.jpg/30649064/Mystery-100x100.jpg
```

## Install Package(s)

```
sudo apt-get install fbi
```

## Execute

Running the viewer shall be executed on the primary screen, not through SSH or Serial connection.
This viewer requires access to the video hardware.

-a, Auto zoom

-t 5, display for 5 sec

-1, do not loop after each image is displayed

-noverbose, show no information when the image is displaying
```
fbi -a -noverbose image.jpg
fbi -a -noverbose -t 10 image1.jpg image2.jpg image3.jpg
fbi -a -noverbose -t 10 -1 image1.jpg image2.jpg image3.jpg

-d /dev/fb0
-T 1
sudo fbi -t 3 -1 -T 1 File.jpg
```

## Issues

There are issues where the display time is longer than the specified time.
One known issues is that the image is being resized. Large images can take up to 5 seconds.
It is suggested to resize the images using the [ImagemagicK tools](md/sw-img-magick-tools.md).

