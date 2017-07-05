# Software, Multiple Sessions with Screen

[Hardware, Installation](hw-project.md)

## Links

Using Screen with Pi, http://raspi.tv/2012/using-screen-with-raspberry-pi-to-avoid-leaving-ssh-sessions-open

## Installation

```
pi> sudo apt-get install screen
```

## Creating another session

When initially logged in, create a session. Execute a command that will run continuously.
```
pi> screen bash
pi> ./readAudio.py
```

Detach from the session by releasing (no carriage return). This command produces no output.
```
CTRL-A
```

Then detach by entering a letter (no carriage return). The initial shell will come up.
```
d
[detached from 815.tty1.raspberrypi]
pi>
```
At this point, you can get various information about the session.

## Session List

It is possible to have multiple screen sessions. Screen gives a option to list them.
```
pi> screen -list
There is a screen on:
 815.tty1.raspberrypi (05/25/2017 08:45:46 AM) (Attached)
1 Socket in /var/run/screen/S-pi.
```

## Return to session

If only one session is available, it is possible to return without knowing the session id.
```
pi> screen -r
```

Terminate a session
```
pi> screen -list
```

Terminate the  running script (no carriage return).
```
CTRL-C
```

Terminate the session (no carriage return). The initial shell will appear.
```
CTRL-D
[screen is terminating]
pi>
```
blah