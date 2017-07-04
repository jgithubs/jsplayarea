# Hardware, Ethernet Connection

[Hardware, Installation](md/hw-project.md)

[Software, Headless](md/sw-headless.md)

## Connection

Connect a Ethernet cable to the Raspberry Pi.
The cable will be detected and the router will assign an IP address.
With the command below, get the assigned IP address that is associated with 'eth0'.
```
pi> ifconfig
eth0      Link encap:Ethernet  HWaddr b8:27:eb:b7:c3:e6
          inet addr:192.168.0.76  Bcast:192.168.0.255  Mask:255.255.255.0
          inet6 addr: fe80::ffa9:dc28:1b31:4936/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:144 errors:0 dropped:0 overruns:0 frame:0
          TX packets:135 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:11837 (11.5 KiB)  TX bytes:15066 (14.7 KiB)

lo        Link encap:Local Loopback
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:520 errors:0 dropped:0 overruns:0 frame:0
          TX packets:520 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1
          RX bytes:42576 (41.5 KiB)  TX bytes:42576 (41.5 KiB)
```

## Connection Verfication

Use the 'ping' command to verify that you can communicate with Pi through your PC. 

```
pi> ping 192.168.0.76

Pinging 192.168.0.76 with 32 bytes of data:
Reply from 192.168.0.76: bytes=32 time=4ms TTL=64
Reply from 192.168.0.76: bytes=32 time=3ms TTL=64
Reply from 192.168.0.76: bytes=32 time=3ms TTL=64

Ping statistics for 192.168.0.76:
    Packets: Sent = 3, Received = 3, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 3ms, Maximum = 4ms, Average = 3ms
Control-C
```

## Logging in thru Ethernet

A communication program can be used to login through ethernet.
Before this can be done, the [SSH Server](md/sw-ssh-server.md) needs to be activated.



