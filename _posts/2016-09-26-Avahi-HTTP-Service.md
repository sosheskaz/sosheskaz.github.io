---
layout: post
title: How to use Avahi to advertise an HTTP service
author: Eric Miller
topic: Programming
---

This is a simple guide to how to set up avahi to advertise an HTTP service that a web browser (in this case, Safari's Bonjour) can detect and hook into.

Background: This is running on a server running FreeBSD 10.3.0. Avahi was installed using pkg and set up with the default configuration.
It is used largely as a sandbox for experimenting, as well as being a media/file server and a light webserver.
Its capacity as a media server is fulfilled using [Plex](https://www.plex.tv), so I want to advertise the existence of the Plex server for easy use.

First, install avahi with the package manager of your choice. In the case of FreeBSD and pkg, `pkg install avahi -y`.
If using FreeBSD, you'll need to enable the service by adding `avahi_daemon_enable="YES"` to `/etc/rc.conf`.
In GNU/Linux distros, this is typically not required.
The avahi service can now be started/stopped/restarted with `sudo service avahi-daemon <start/stop/restart>`.

Next, find the avahi services directory. With my installation, it is located in `/usr/local/etc/avahi/services`.
On other GNU/Linux distros, it may also be found in `/etc/avahi/services`.
In the services directory, you will likely see some default services aleady set up.
For example, I already had `sftp-ssh.service` amd `ssh.service` in mine.

Create a new file called `<your-service>.service`. In my case, this is `plex.service`.
Within that file, add the following (which I shamelessly stole most of from [here](http://holyarmy.org/2008/01/advertising-linux-services-via-avahibonjour/)):

```
<?xml version="1.0" standalone='no'?><!--*-nxml-*-->
<!DOCTYPE service-group SYSTEM "avahi-service.dtd">
<service-group>
<name replace-wildcards="yes">%h <YOUR_HTTP_SERVICE></name>
<service>
<type>_http._tcp</type>
<port><YOUR_PORT></port>
</service>
</service-group>
```

Now, restart avahi with the command `sudo service avahi-daemon restart`.
The new service will now be viewable via bonjour clients, such as Safari and dns-sd (see below).

![Avahi-Safari](/{{site.post_images_path}}/2016-09-26-avahi-in-safari.png)
![Avahi-dns-sd](/{{site.post_images_path}}/2016-09-26-avahi-in-terminal.png)
