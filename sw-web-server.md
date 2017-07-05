# Software, Setting up a Web Server

[Hardware, Installation](hw-project.md)

## Links

* Setting up Apache webserver, https://www.raspberrypi.org/documentation/remote-access/web-server/apache.md
* Use Pi as a WebServer, https://computers.tutsplus.com/tutorials/how-to-use-a-raspberry-pi-as-a-local-web-server--cms-19943

## Install the packages:

The core of the instructions comes from the main Raspbian site. The first step is to install the Apache Server.
```
sudo apt-get install apache2 -y
```

Once installed the web page can be access using the IP address of the Pi.  From a browser, type in the following command to verify that the website is seen.
```
http://192.168.1.2
```

The default page is complex. To prove to that is our site, we want to modify it with a simple 'Hello World' page. The web files are located in '/var/www/html'.  The owner of the files is 'root', therefore, 'sudo' has to be used when attempting to modify the 'index.html' file.
```
cd /var/www/html
ls -la
total 24
drwxr-xr-x 2 root root  4096 Jan 31 10:47 .
drwxr-xr-x 3 root root  4096 Jan 31 10:39 ..
-rw-r--r-- 1 root root    88 Jan 31 10:47 index.html
```

## Setting permissions to the website:

Change the permissions of the file (or directory?) such that it can be modified without 'sudo'. From the 'whoami' command, the user name is 'pi'. Change permissions with the 'chown' command.
```
sudo chown pi: index.html

ls -la
total 24
drwxr-xr-x 2 root root  4096 Jan 31 10:47 .
drwxr-xr-x 3 root root  4096 Jan 31 10:39 ..
-rw-r--r-- 1 pi   pi      96 Jan 31 10:50 index.html
```

## Modifying the website:

Modify the file with simple 'hello world' html example. Copy and paste the following in the file and save.
```
<html>
<header><title>This is title</title></header>
<body>
Hello world
</body>
</html>
```

Refresh or retype the page location from another PC. We now have a web server running our own web page.

