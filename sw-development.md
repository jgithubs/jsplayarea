# Development, Scripts to intergrate Pictures/Audio/RFID

* [Hardware Project](hw-project.md)

## Development

## Backup

```
tar -cf x.tar readme1.txt
tar -tf x.tar

tar -rf x.tar readme2.txt
tar -tf x.tar
```

## Transfer of files

## Repackage tar file

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