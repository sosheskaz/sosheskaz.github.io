---
title: Handy Apps and Programs
author: Eric Miller
layout: page
permalink: /software/
---

This is a list of apps and CLI programs I consider "essentials" (in that I use them constantly).
It's divided up into two sections – one for apps (for most people) and one for command line tools.
This is basically just a curated list of software that I personally attest to. It's going to be
focused on mac apps, but many of them are cross-platform and will be available on Windows or Linux.

## Apps

### Cross-Platform

* [LastPass](https://www.lastpass.com). Free. Can't recommend this one enough. It stores your passwords (securely) and syncs them
across devices. The most common response I get is "but isn't that putting all your eggs in one
basket? What if LastPass' servers get hacked? The answer is that they don't actually *know* your
passwords – at no point are their computers ever able to read them. I've personally read their
whitepaper, and their use of technology is sound in terms of security of your passwords. I like
them because they are cross-platform and cheap, but 1Password, Keeper, and for command line users,
`pass`, are all good alternatives.
* [Authy](https://www.authy.com). Free. Authy is a tool for 2-factor authentication, a great way to add a lot of extra security to
LastPass, banks, Amazon.com, and lots of other places that support it. It has desktop, Chrome, and mobile apps.

### macOS

* [The Unarchiver](https://theunarchiver.com). Free. Think 7-Zip for mac. Can open pretty much any
kind of compression file. Install with homebrew-cask or with the installer, not with the mac app
store for best user experience.
* [QuickLook Plugins](https://github.com/sindresorhus/quick-look-plugins). There's a lot of them,
but each one expands what QuickLook can do. A lot of these are developer-focused, but there's a lot
of more friendly ones too.
* [BetterTouchTool](http://bettertouchtool.net). $6.50. Adds optional window snapping to macOS,
along with letting you customize trackpad, mouse, keyboard, and touchbar shortcuts on a global or
per-application basis.
* [Amphetamine](https://itunes.apple.com/us/app/amphetamine/id937984704?mt=12). Free. Temporarily
turn off sleep functionality.
* [NoSleep](https://integralpro.github.io/nosleep/). Free. Don't sleep when closing the
lid. Most people don't need this, but if you do, boy does it come in handy.

### iOS

* [Carrot Weather](http://www.meetcarrot.com/weather/). A heavily featured iOS weather app, costing
$5 on the app store. Lots of features, lots of accuracy, lots of snark.
* [Scanner Pro](https://itunes.apple.com/us/app/scanner-pro/id333710667?mt=8). $4. Takes relatively
high-quality document scans using your phone's camera, using perspective to shape it into a
normally-shaped PDF document and syncing to iCloud. Also supports OCR text recognition. Was great
for digitizing records when I was a college student.
* [MeasureKit](https://itunes.apple.com/app/id1258270451). Free with an in-app purchase for more
features. An augmented-reality-based app that you can use to visualize size and take approximate
measurements of length, angle, levelness, and now magnetic fields for some reason. Occasionally
useful, and novel if nothing else.

## CLI Tools

### Cross-Platform

* [OpenResty](https://openresty.org/en/) or [NGINX](https://www.nginx.com). Great load balancer,
basic web server, or reverse proxy. Simple, lightweight configuration, and doesn't share Apache's
flawed (in my opinion) scale-unfriendly architecture.
* [rbenv](https://github.com/rbenv/rbenv). Stamp out pesky ruby version conflicts.
* [Aria2](https://aria2.github.io). Multi-threaded downloader. Can download the same file from
multiple sources simultaneously via multiple threads or multiple connections (ex. HTTP, FTP, and
bittorrent simultaneously). Great for downloading operating system images fast!
* [Duplicity](https://launchpad.net/duplicity). Simple and adaptable incremental backup tool. Works
really well with AWS S3!

### macOS/Linux/BSD

* [homebrew](https://brew.sh) for mac. Mac's missing package manager.
* [docker](https://www.docker.com). Easy, fast virtualization and containerization of services.
* [tldr](https://github.com/tldr-pages/tldr). Do you love documentation but hate reading? Me too!
* [htop](https://hisham.hm/htop/). A customizable, colorful, and interactive process viewer.
* [suricata](https://suricata-ids.org). Free intrusion detection system.

### Windows

* [Cygwin](https://www.cygwin.com). Free. GNU utilities for Windows, to make it a bit easier to use for
command line folks. If you're a CLI user, this is essential for Windows in my opinion.
* [Chocolatey](https://chocolatey.org). Free. The Windows package manager. Caveat: sometimes the
maintainers for individual packages don't keep their checksums up-to-date.
