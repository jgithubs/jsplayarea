# Development, Scripts to intergrate Pictures/Audio/RFID

* [Hardware Project](hw-project.md)

## Development

The development portion of the project is the writing of a series of python and bash scripts.
A [series of software](hw-project.md) was install that reads the RFID tag, plays pictures, plays audio, etc.
The script binds all the software together to associate RFID tags with pictures and music.

There exists two sets of hardware.
One hardware is simply to test the installation and write the scripts.
The second set of hardware is for the Maker Camp for the students.
What needs to happen is to bring down the scripts into the Raspberry Pi.

A series of developed files are packaged into tar files (similar to zip files).
These files are transfer to the second set of hardware and unpackaged.
The transfer of the file can be done by copying it to the USB stick, transfer it over using FTP, or downloading it into the Raspberry Pi through GitHub.
These sections describe how to package and unpackage the python and bash scripts.

## Backup using tar files

Tar files are frequently used in linux like systems.
Raspberry Pi is linux like.
The 'tar' software is 

Create a tar file with a single file. Display the content of the tar file.
```
pi> echo "hello" > readme1.txt
pi> tar -cf x.tar readme1.txt
pi> tar -tf x.tar
readme1.txt
```

Append a new file to the same tar file.
```
pi> echo "hi" > readme2.txt
pi> tar -rf x.tar readme2.txt
pi> tar -tf x.tar
readme1.txt
readme2.txt
```

## Package Creation

A script was written to package all development scripts and rfid data.
The results are two files.
This script uses wildcards and references subdirectories.
```
pi>./pkg.sh

pi> ls *.tar
dat.tar  pkg.tar
```

Here are the content of the packaged files.
This will vary as development progresses.
Three key scripts are described in the documentation (readAudio.py, run-loop.sh, and readUsb.py).
Other scripts are script that are called by the three key scripts.

It would of been great to create just python scripts, however, ran into an issue.
There was a need to run commands (from installed software) and get the printed results back.
This worked in a limited capacity. 
The problem was that all of the passed arguments was not passed on to the command.

To work around this issue was to use bash scripts.
The argument was passed in one long string (from python).
The bash script then parsed the argument and called the command.
The printout from the command did come into python.
Due to time contraints, a proper resolution to this will be investigated in the future.
If you have any solutions, feel free to submit an example.

The rfid data will vary based on the Maker site.
```
pi> tar -tf pkg.tar
jpg-h.sh
jpg-w.sh
pkg.sh
run-loop.sh
readAudio.py
readUsb.py
signalUp.py
./src/run-cp.sh
./src/run-kill.sh
./src/run-link.sh
./src/run-mocp.sh
./src/run-rm.sh
./src/runIntf.py
./src/cleanup

pi> tar -tf dat.tar
./data/ffffffffff/
./data/ffffffffff/01-NM-History-Museum.jpg
./data/ffffffffff/Drone_MP3-1.mp3
./data/ffffffffff/hList.txt
./data/ffffffffff/02-NM-History-Museum.jpg
./data/251c718bc3/
./data/251c718bc3/hFile2.jpg
./data/251c718bc3/hFile3.jpg
./data/251c718bc3/hList.txt
./data/251c718bc3/hFile4.jpg
./data/251c718bc3/hFile1.mp3
./data/e63a177cc/
./data/e63a177cc/hFile2.jpg
./data/e63a177cc/hFile1.jpg
./data/e63a177cc/hList.txt
./data/e63a177cc/hFile1.mp3
./data/e196718b8d/
./data/e196718b8d/02-LctVT.jpg
./data/e196718b8d/05-images.jpg
./data/e196718b8d/04-Fig-12-Raspberry-Pi-Components-Explanation.jpg
./data/e196718b8d/01-images.jpg
./data/e196718b8d/03-raspberry-pi-2-pinout.jpg
./data/e196718b8d/hList.txt
./data/e196718b8d/four-winds-web.mp3
./data/set3.m3u
./data/set4.m3u
./data/seta.m3u
./data/setb.m3u
```

## Packages

The package is intented to be uploaded to the git-hub where it can be downloaded.
Other options is to transfer using FTP, writing the file to the USB stick, etc.

```
pi> cd $HOME
pi> tar -xf pkg.tar
pi> tar -xf dat.tar
```

## Outdated information

The following is an old method. Please ignore.
```
cd ftp
cd files
tar -xf pkg.tar

cd src
rm -rf SPI-py
rm -rf MFRC522-python

tar -cf mov.tar *
cp mov.tar $HOME/.

tar -xf mov.tar

```