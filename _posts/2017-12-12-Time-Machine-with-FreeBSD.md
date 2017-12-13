---
title: How to Create a Time Machine Server with FreeBSD
layout: post
author: Eric Miller
category: Tutorial
tags: FreeBSD
---

Running a time machine server has historically been a pain. Which sucks, because it's actually a
pretty good backup system. For the uninitiated, Time Machine is the built-in backup system on macOS.
It keeps incremental backups, which means you can restore your machine to an hour ago, a week ago,
a month ago, a year ago, and various increments in between. However, running one tends to suck,
because there have historically been two options for doing it. Either sinking $300 on an Apple
router (they're nice enough routers, but not something I want personally) that's capable of it, or
buying macOS server and getting a spare mac to just be a server for backups. This is silly, because
macOS doesn't make for a good server. Luckily, with the new macOS, they made the time machine server
functionality part of the OS, rather than part of their server app.

Somehow, it's taken me embarassingly long to finally figure out how to set up a Time Machine server
on my FreeBSD machine. Though details proved hard to find, I eventually dug up some guides on how
to do it on Linux, and adapted it for my setup. This guide will walk you through how to do it on
FreeBSD, and if you're on Linux, you can probably figure it out between this and finding other
guides.

### 0. Notes

You don't want to run this over an insecure network. This is designed for running inside of home
or business networks, not being open on the internet or available to anyone on a guest network.

### 1. Netatalk

First, we need to install `netatalk3`. `Netatalk` is an open-source server for running AFP (Apple
Filing Protocol) file shares over your network. AFP is generally considered an inferior protocol,
but it's the only thing Time Machine supports, so we're stuck with it (unless you want this to get
complicated and unreliable). Do this with `pkg install netatalk3`.

### 2. Prepping your File System

This is basically an optional step. I wanted to limit the total size of all my backups to 1TB, and
have a partition on my file system specifically for Time Machine. I'm using ZFS for my data share,
so the command I ran was `zfs create -o quota=1T storage/timemachine`. You'll also need to set up
ZFS to auto-mount this new partition.

You can do this (or not do this) however you want, but you'll need to have a location ready to
hold Time Machine's files. Mine is `/storage/timemachine`. You'll also want to make sure that
the user accounts (on the machine) can access the underlying filesystem. Use `chown`, `chgrp`, and
`chmod` as appropriate.

### 3. Netatalk Settings

Next, you'll need to edit netatalk's settings, which are found on FreeBSD in 
`/usr/local/etc/afp.conf`. You'll want at least two sections - a "Global" section, and a "Time
Machine" section. Here's a quick look at mine, before I go through it piece by piece. A full
reference document can be found
[here](http://netatalk.sourceforge.net/3.0/htmldocs/afp.conf.5.html).

```
[Global]
; Global server settings
hostname = myserver
hosts allow = 192.168.1.0/24
afp listen = 192.168.1.111
zeroconf = yes

[Time Machine]
path = /storage/timemachine
time machine = yes
valid users = ericmiller
```

[Global] defines the settings that apply to **all** your following shares. If you ever choose to
set up another AFP share, it'll be useful to have these as a shorthand.

-   Hostname defines what hostname you advertise on your local network. You'll want this to reflect
    a real domain or IP address that can be used to connect to your server.
-   Hosts allow says what hosts are allowed to connect to your server. This is a basic security
    measure that limits what IP addresses can connect to your share. The range I have here
    (`192.168.1.0/24`) is standard CIDR notation saying that all IP addresses from `192.168.1.0` to
    `192.168.1.255` are allowed to connect. `192.168.1.0/24` is the typical subnet for consumer 
    routers. `192.168.0.0/24` is also common (ish).
-   AFP listen tells it which network interfaces (and port) to listen on and advertise. I only have
    one outward-facing network interface, which is the IP address of my server. Running 
    `ifconfig | grep inet` should give you a short list of options.
-   Zeroconf tells the server to advertise on the local network that it is an AFP server. You'll
    want to enable this to get time machine to work properly. If you're using avahi, you may not
    need this as long as you configure an avahi service for `_afpovertcp._tcp`.
-   [Time Machine] tells netatalk that the following settings are specific to just the share we're
    using for Time Machine. In the brackets, put whatever you want the display name of your Time
    Machine share to be.
-   path is the path to the place on the file system you want to use for time machine.
-   time machine tells the server that this share _is_ for time machine, and enables support for it.
-   valid users tells it what users (as defined through PAM) are allowed to access/modify the share.
-   This isn't in my config, but you may consider another line like `vol size limit = 1000000`,
    where the value given is in Megabytes. I don't need this because I have my own area carved out
    on the file system level, but it is generally recommended for Time Machine backups.
-   Look at the [reference document](http://netatalk.sourceforge.net/3.0/htmldocs/afp.conf.5.html).
    There may be other options you want (and more details) there.

### 4. Service

Next, you'll want to enable the service by adding the line `netatalk_enable="YES"` to
`/etc/rc.conf`. Then, just run `service netatalk start` to get it running.

### 5. Start Using It

On your mac, open System Preferences and go to the Time Machine pane. Click "Select Backup Disk".
The share you just created should pop up as an option. Select it. I also recommend selecting the
"Encrypt backups" checkbox, especially if the underlying file system is not encrypted (maybe even
if it is, just to be safe). Click "Use Disk". It will prompt you for a login - use the login for
your server that you should have in "valid users". Normally, this is the same as your general login
for the server. Make sure to set up any files or directories you want to exclude. Large binary
files (like virtual machines) and temporary files (like ~/Downloads) are great candidates here.
