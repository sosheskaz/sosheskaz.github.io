---
layout: post
title: The Case of the Circular Dependency
author: Eric Miller
category: Server
tags:
---

As some know, I keep a personal server. I've developed tales of my (mis)adventures and the things
I've learned from them. I found this one humorous. Why? The root cause.

My hard drive is *too fast*.

----

I'll start at the beginning. If you're not into computers, I'll explain things in a way that
hopefully anyone can understand, but to be honest I'm not sure if you'll get a lot out of it. In
either case, I hope you'll enjoy it.

## The Background

So, background on my server setup. The operating system is installed on a medium-quality solid
state drive (SSD). The main appeal of solid state drives is that they're really fast, at the cost of
size. My server is used for a multitude of things – including backups and file, which take up
hundreds of GigaBytes of data. I want it to boot fast, but I also want lots of storage space. The
result is that the operating system is installed on the SSD while large files are stored on an
external USB 3.0 drive. The USB 3.0 drive is fast enough that, for what I use it for, it never
causes substantial slowdowns. The upside of using USB 3.0 is that external drives can get pretty
much as big as you want, but the downside is that USB 3.0 isn't as fast or reliable as a built-in
drive.

The server runs FreeBSD as its operating system, which works pretty well. Since I wanted to learn
more about using it, I did some experimentation with the file system. FreeBSD supports two file
systems – UFS and ZFS. UFS is old and simple, but rock-solid and fast. ZFS has tons of features,
but is very very slightly slower and is considered to be less reliable just because it's younger.
UFS is installed on the SSD for maximum reliability and simplicity, while ZFS is installed on the
USB 3.0 drive for its self-recovery and other features.

I later found out that this setup is kind of stupid, and I should be using ZFS across the board.
But it's more work than I'm interested in to reimage my whole machine and fix it, so I'm just
going to have to live with its quirks for now.

## The Problem

The problem was simple enough, albeit a bit enigmatic. From time to time, the external drive will
freeze up. The processes that need to access the data on it will try, and get stuck. No data is
retrieved, and no error is triggered. Nothing goes wrong directly until one of my monitors starts
triggering because it can't retrieve test data.

This is strange. FreeBSD still thinks the drive is there. The drive shows as being mounted. But when
I look at the drive's status, it says `UNAVAILABLE` and shows an unhelpful error message about
something going wrong.

## My First Attempts

The first thing I did was try to list the files in the external drive. It hung forever and never
showed me any of my files or folders. Vexing.

I could identify the process that was tied up trying to access the drive by seeing which one my
monitors showed was down. My first attempt was pretty simple, restart the service that ran the
process.

```
# service restart myservice
```

I waited. And waited. I figured it was trying to figure out what was going on with the drive in
order to clean itself up. But after a while, it was apparent that it was totally stuck with no way
out. So then I tried something a bit nastier. I got the process ID and tried to kill it myself.

```
# kill 9876
```

I waited. And waited. And nothing happened. What that command basically does is tell the process
in question "You need to stop. Right now please. Seriously." It almost always works. Sometimes it
doesn't. When it doesn't, there's a fallback that always works.

```
# kill -9 9876
```

Unlike normal `kill`, this doesn't ask the process to stop. It tells the operating system to
terminate the process immediately. No being nice, no letting it clean up resources. Just drop
everything it's doing. That's why it can't fail – you're telling the part of the computer that
allows processes to run **at all** to not let that process run anymore.

I waited, and the process didn't stop. That shouldn't happen.

This xkcd comic seemed apt at the time.

![Source: xkcd.com](/files/images/posts/2018-02-20/inexplicable_2x.png)

Well, nothing's working. Time to pull out the big guns.

```
# reboot
```

Here's a note to the Linux/BSD fans out there. If the operating system isn't able to force kill
a process, it can't reboot. The reboot hung my server in a state of purgatory, unable to die
but far from alive.

Ultimately, my solution was to force a restart. You know, when you hold down the power button
until everything stops. This is potentially really bad for your computer, especially if it's in the
middle of writing to the disk, which is what it looks at this point like mine was doing. At this
point, I'm prepared for it to be broken when I come back.

I log back in, the drive mounts, and everything is fine. Huh? I list the errors the drive is having.
With ZFS, this is pretty easy, because it actively tracks the problems with it. It's showing two
issues with metadata. I run `zfs scrub`, which auto-fixes anything wrong. This fixes the issues and
I move on, figuring it was a one-off glitch.

## The Second Time

Then it happened again. I remembered the headaches of the time before, and just hard rebooted it
again, feeling bad about doing it, but not wanting to deal with the headache. At some point, I make
a mental note that I should actually figure out how to fix it. That day comes, and the problems
manifest again in the same way they always do. I get googling (and reading the manual) and
eventually try a command I found on the internet: `zpool clear`. It works again!

`zpool clear` basically just says "ignore any issues you've found, just keep working". It seems odd
to me that the default behavior is to fail as enigmatically as possible, but I'm also not willing to
dive deep enough to the C++ source code to try and make a fix, so I left it as-is.

I go to bed, happy that I have a better (if not ideal) solution.

## The Third Time

Why, oh why, didn't I write down what I did. Stupid, stupid, stupid Eric. Hard reboot again.

## The Fourth Time

This time, I'm going to find the right way to solve it. And then I'm going to make a script to do
it for me, called something like `fix_zfs`. Then I won't miss it again. I rediscover `zfs clear`,
much more quickly this time, and start working on a script that detects if it's down and clears it
if it is, then runs an auto-repair. I finally have a self-fixing system.

At this point, I've got a few hints, and can deduce my best guess on what happened that caused this
enigmatic behavior. It looks like the ZFS drive is in a zombie-like state – it's not mounted,
because the file system is inaccessible, but something is in the middle of some sort of operation
with it. The process can't stop because it's in the middle of an I/O (input/output) operation and
stopping would be dangerous (in terms of data corruption. The drive can't be fully unmounted because
a process is in the middle of accessing it, and stopping would be dangerous. Luckily, because of how
ZFS works, it can auto-repair those errors.

And so we have our result – a circular dependency. Everything is in gridlock, unable to move because
it would might break things. And nothing can stop it because nothing can move. It's bizarre, and
it's a little bit cool. But the inquisitive mind will ask: *why?*

## The Autopsy

So, I have something that will detect and fix my problem within 4 minutes of it happening, but why
did it go wrong in the first place? If you guessed that it was because I did something stupid, you
win the prize. At this point, I described my predicament to a friend, and they sent me back (once
again) an apt xkcd comic.

![Source: xkcd.com](/files/images/posts/2018-02-20/tv_problems_2x.png)

So what was I doing that was so stupid? Here's a look at my crontab:

```
* * * * * zfs mount storage
```

What that's doing is, every minute, it tries to mount my ZFS drive. One of the fun side effects of
this is that if the drive is already mounted, it throws off an error. And when a `cron` job throws
an error, it sends a local email to the root account. I had over 170,000 emails from that job in
my root account, and they took up about a GigaByte of space. That's not directly related to the
issue, but it is pretty hilariously inept on my part.

What was happening, as best I can tell, is that eventually the `zfs mount` process interfered in
*just* the wrong way with the other processes trying to access that drive, and things went wrong.
This is an insane problem caused by an insane solution and all ultimately my fault.

----

Then the solution is obvious, right? Just remove that `cron` job. Well, there's a problem with that.
Without the `cron` job, the drive isn't mounted on boot. And if it's not done on boot, then I have
to log in and do it manually, which is *such a hassle*. Thing is, it **is** supposed to be mounted
on boot. I've jumped through all the hoops and made 100% sure – it's definitely running the code to
mount all of my ZFS drives on boot. So why aren't they there when I log in?

So I took to IRC, started diving through the boot logs, and going through built-in operating system
files to try to hack something to work. And there it is, buried deep in the time stamps. The
auto-mount is running a few seconds before the USB ports are fully on. That's it – my SSD is booting
up **too fast** for it to work correctly.

Taking to IRC, someone gives me a helpful line to add to `/boot/loader.conf` (the settings for
booting up).

```
kern.cam.boot_delay=10000
```

That's delaying 10 seconds (10,000 milliseconds) before starting the bootup processes.

And when I say computers are the work of the Devil, that's what I mean.
