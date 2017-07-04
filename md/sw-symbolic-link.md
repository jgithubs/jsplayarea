# Software, Symbolic links

[Hardware, Installation](md/hw-project.md)

## Overview

The use of symbolic links is handle through the development scripts.
Symbolic links is used to make the scripting easier because the filenames are always the same.

## Using Symbolic links with FBI

Setting the symbolic link
```
pi> cp file.jpg hardlink.jpg
pi> ln -s hardlink.jpg softlink.jpg
pi> ls -la
pi> fbi softlink.jpg
pi> rm hardlink.jpg
pi> fbi softlink.jpg
No file exists
```

Setting the symbolic link
```
pi> cp file.jpg hardlink.jpg
pi> ln -s hardlink.jpg softlink.jpg
pi> ls -la
pi> fbi softlink.jpg
pi> rm hardlink.jpg
pi> fbi softlink.jpg
No file exists



```