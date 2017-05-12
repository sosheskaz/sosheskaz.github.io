---
layout: post
title: Linux and BSD - A Tale of Two Operating Systems
author: Eric Miller
category: Technology
tags: 
---

I've been using FreeBSD a lot recently. FreeBSD is similar to Linux operating systems in many ways,
and at least initially, it will feel like home to Linux users. But along the way, there are lots of
pitfalls stemming from the historical philosophical differences in the BSD and Linux communities. In this article,
I'm going to talk about my adventures in BSDand Linux, coming from mainly a MacOS background with some 
experience in Linux operating systems and a soft spot for FreeBSD.

# A History Lesson
This goes into the history of computing a bit. I find it interesting, but if you don't, there's a TL;DR
at the bottom.

In the days of early mainstream commercial computing (i.e. the 1960s and early 1970s), computers each
came bundled with their own operating system, designed specifically for that computer. Many companies 
reused components from their other systems (IBM's System/360 especially), or tried to integrate support
and similarities to other popularly used operating systems (many smaller companies needed their systems
to work well with larger companies' computers), but operating systems were not as modular as those of
today. The operating system you used was the one that came with the machine, because it was the only one
that was designed to work with that particular machine.

By the 1970s, computers were becoming cheaper, and minicomputers (as opposed to mainframes or
supercomputers) were becoming popular, with one example being Digital Equipment Corporation's (DEC) 
PDP-7. The PDP-7 was a very economical choice at the time, with very good performance for the price. DEC
was also a fairly major player at the time, having made some revolutionary changes to the industry over
the course of its existence (though by no means a major competitor to IBM - but that's another story).
Some researchers at AT&T's Bell Labs got their hands on one, and started work on an operating system 
called Unix. The right to this eventually wound up with a consortium called The Open Group, which led to
the creation of the Single UNIX specification, which became the name for the family of operating systems
which operated in a similar manner to the original Unix operating system. The idea was that understanding
of one operating system which matches the UNIX standard would give good understanding of others which 
also met the standard.

While relatively few operating systems are actually registered as meeting this standard, many other
operating systems follow this standard spiritually, including most Linux distributions, and can be 
considered UNIX-like. The abbreviation for UNIX-like operating systems is "*NIX", which refers to the
family of not just UNIX systems, but Linux, BSD, and other operating systems.

From UNIX, two main open-source operating system paradigms emerged, the Berkeley Software Distribution
(BSD) and GNU/Linux. GNU stands for "GNU's Not Unix" (programmers are silly people) and Linux is named
after its creator, Linus Torvalds. These were born from two very different paradigms, from economic,
practical, and academic perspectives.

### A Simplified Version of the *NIX Family Tree

![A simple version of the *NIX family tree.](/files/images/posts/2017-05-12/unix-family-history.svg)

Of note is MacOS, which itself was born from BSD. BSD was a great match, philosophically speaking, for 
Apple. Initially, they developed the Darwin kernel, which is based on BSD, and built what is now MacOS
on top of that. This means that MacOS can be considered part of the BSD family, although their
respective philosophies do diverge significantly. Other forms of BSD were also created, namely FreeBSD,
NetBSD, and OpenBSD, which are all open and free.

Also worth noting is that there were many, many descendants of Linux, called distributions or distros.
Then, of course, those distros had their own children. Notable distros include Debian, Fedora, and Arch
Linux, as well as the Android and ChromeOS operating systems.

As an Aside, DOS/Windows just kind of did its own thing and is not related at all to *NIX systems, 
and was separated from the academics of the time. This
led to some serious problems for Windows, but also some benefits (which in my opinion were outweighed by
the problems). In recent years, Windows has bridged many of these gaps.

TL;DR: Unix was created by Bell labs. This established a common thought pattern for operating systems,
and the main child operating systems BSD and Linux were created. After that, many offshoots of these
systems were created, including operating systems like MacOS, FreeBSD, Ubuntu, and Android.

# Philosophy
Linux users will often chide users of other operating systems, saying that their operating system of
choice is better because it gives them more control. To some extent, this is true - Windows and MacOS are
much more difficult to customize, especially at a low level, then Linux. The counterargument to this is
that an easier interface, even if it's more limited in absolute control, is easier to use for most users,
and thus will be most effective. I tend to agree more with the latter, which is one of the reasons I
prefer MacOS for my day-to-day work.

That said, BSD operating systems tend to have even more direct control than the Linux operating system
does. Linux is actually designed to be an easier to work with operating system than BSD is - the idea
is that it should be easy to get your system up and running in an easy, modular way. BSD, on the other
hand, will tend to do what you tell it to - and nothing more. This is because the BSD ecosystem exists
in two main components: The operating system, to which there are periodic and independent standalone
updates, while in the Linux system, everything, even the kernel, is considered a software package to
be updated whenever.

Take, for example, installing a simple *NGINX* webserver. On Linux this is quite easy - you simply type
`apt-get install nginx` into your terminal, and you're done. It's running with a default configuration,
and you have a webserver up right away. With FreeBSD, the package manager was almost an afterthought.
Initially, it just used something called the ports tree, which allowed building open-source packages
from scratch. So you have two choices - install a pre-built one with `pkg install nginx`, or build it
from scratch with `cd /usr/ports/www/nginx && make build install`. Then, if you want it to run 
automatically, you'll have to update your /etc/rc.conf file to and add `nginx_enable="YES"` to 
tell it that it's okay. As you can see,
FreeBSD is much more confusing, but it also allows the user to be more careful and specific, if they have
the knowledge to do so.

BSD becomes, in my opinion, the OS of academics, while Linux becomes the OS of the people.

# Licenses
This is also
reflected in the [BSD licenses](https://en.wikipedia.org/wiki/BSD_licenses), which BSD and the BSD 
utilities are licensed under, and the 
[GNU General Public License](https://en.wikipedia.org/wiki/GNU_General_Public_License), 
authored by Richard Stallman, which many utilities used commonly with Linux-based operating systems use.
Both licenses are used for open-source software, but they have important indications of the underlying
philosophies of the two communities. 

That important distinction is both an economic one and one based on the idea of "Free Software". Free
software, in this context, means free as in "Free Speech", not free as in "Free Pizza". The underlying
idea of free software is that the societal benefit of the creation of a piece of software is maximized
when it's released giving users freedom - the freedom to view, modify, and utilize the software however
they wish. 

The GNU license adheres strongly to this philosophy - meaning that any derivative work of 
a GNU program must be released as GNU itself. This means, if you develop a program based on GNU code,
perhaps with some modifications or improvements, then if you release it, it must be released under the
GNU license. That said, the tools themselves are free to be *used* for any purpose, whether for-profit or
not. For this reason, the GNU community is often considered to be philosophically aligned with communism,
as it is based on the belief that collaborative work, the fruit of which is usable by all, maximizes
that work's benefit to society. The GNU license is historically important, as it gave developers an assurance that 
whatever code they wrote would be free to any to use, and could never be charged for - that is, its full
value would be applied to society. This license is one of the major causes of the popularity and success
oof Linux-based operating systems.

The BSD license, on the other hand, believes that the restriction placed on derivative works actually
reduces its total benefit to society. The rationale is that if a for-profit entity can produce
derivative software that poses enough value to make its way in the free market, then that is 
intrinsically valuable to society as well (though not as valuable as if it were free).
However, it still allows altruistic developers to create their own free derivative works, much like GNU
does.

This is why BSD was such a good fit for Apple - it allowed them to repackage the BSD utilities, along
with their own work, and sell it for a profit. Were it not for the BSD license, Apple would not be as
successful as it is, if it would have been able to create an operating system at all. 
Of course, it is worth noting that the core of MacOS, Darwin, is available as open-source. 

# The Practical

Let's look at some of the most common distributions of each - FreeBSD for BSD, and
Ubuntu for Linux. We'll compare the minimum specs to run it, what comes installed, and how complicated
setup is.

### FreeBSD
* One thing to install. No options installed out-of-the box.
* Requires 96MB of RAM, and 1.5GB of disk space. Runs okay with most any CPU.
* Requires 2-4GB of RAM for a general-purpose desktop.
* Comes with just the basics installed - not even a desktop environment or common utilities are 
installed by default.

### Ubuntu
* Multiple choices for installers and base operating systems.
* For server install, requires 256MB of RAM, 1.5GB of disk space, 300MHz CPU.
* For desktop, requires 512MB of RAM, 5GB of disk space, and a 700MHz CPU.
* Comes with many utilities and services installable from the start.

As you can see, FreeBSD takes much more work to get up and running. The benefit of this, however,
is that the system winds up being much leaner. This means it uses less processing power, less memory,
and less disk space. It also means it can be easier to secure, as there are no attack vectors introduced
without the maintainer knowing about it. Another benefit is that, with less moving parts, FreeBSD is more
stable than its Linux counterparts, at least in my experience.

# A Learning Experience

But, interestingly enough, the most meaningful part of my experience with FreeBSD is how much I learned.
Ironically, learning BSD drove my understanding of all *NIX operating systems, because it requires
you to truly understand what you're doing every step of the way. It prepares you for different
utilities, and adapting to new situations where your existing knowledge base may no longer be accurate.
It teaches you to think in new ways, and to truly understand what's going on behind the scenes when you
start your computer, install a package, or disable a service.

And perhaps, most of all, it makes you appreciate easy-to-use operating systems like never before.
