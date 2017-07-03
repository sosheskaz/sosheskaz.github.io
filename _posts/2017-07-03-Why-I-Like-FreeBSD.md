---
layout: post
title: Why I Like FreeBSD
author: Eric Miller
category: Technology
tags:
---

Those of you who know me may have noticed I've been talking about FreeBSD. When
I get into a technology, I like to research it. I like to understand the
philosophy behind it, and I like to learn how to use it to its full potential.
When I'm into a technology, I try to dig in and maximize my use of it. So since
I've been living with FreeBSD for quite a while, I'll explain why I like it so
much, and what it has to offer (in my opinion) over other alternatives, as well
as reasons why I, personally, like it.

# 1. Because I'm a Mac User

Using Linux came fairly naturally to me, because as a mac power user, I learned
the Terminal, and a lot of it carried over pretty well to Linux. But BSD
distributions take it a step further in making it feel like home. MacOS itself,
as well as iOS, are based on Darwin, which is Apple's version of BSD. Apple
chose to base its operating system on BSD for two big reasons. The first is that
it would have been illegal for them to charge for an operating system based on
Linux, due to the GNU General Public Licence (GPL). Second, because BSD has a
philosophy that will sound very familiar if you're a mac user. From
[Over-Yonder.net](https://www.over-yonder.net/~fullermd/rants/bsd4linux/08):
_BSD builds up a core system which is uniform, whereas Linux distributions takes
pre-existing pieces and pretty much puts them together helter-skelter.
Naturally, the BSD method is far more amenable to keeping things ordered, while
the Linux method practically necessitates utter chaos. That's not to say that
chaos is inherently bad, or order inherently good. They're just different
environments._
So BSD tries to keep things internally consistent, and tries to keep the core
functionality of the operating system working in a consistent way. A way where
everything, at the core level, is designed to work and play well together. This
reminds me of Apple's methodology of trying to make all of their core apps work
and play well together, as well as having very consistent methods of accessing
functionality between different apps.

Given to that similarity in philosophy, it's natural that I, as a mac user,
would prefer the nature of BSD-based operating systems in general - it simply
feels like home to me.

# 2. Because it's Stable!

FreeBSD, in my experience, has been an incredibly stable operating system. I've
never once had to reboot it to resolve an issue. When I used Linux distributions
like Ubuntu and Debian for my personal server, I would often encounter strange
issues and have to either reboot every few weeks, or have planned reboots. I'd
also encounter strange issues from time to time (as is the nature of linux IMO).
With FreeBSD, once the software is installed and configured, I trust it to work
correctly.

Some reasons for this go to the way in which FreeBSD versions are released. The
core BSD utilities are, unlike in Linux distributions, all updated at the same
time as part of an operating system upgrade, which happens on a fixed schedule.
This also means that each release is extensively tested and crafted to function
as a single, unified system. Linux distributions could be more accurately
described as a collection of software packages assembled around a Linux kernel,
as opposed to the unified, thorough nature of FreeBSD releases.

# 3. Because I'm a Control Freak

One of the common arguments in favor of using Linux distributions over Windows
or MacOS solutions is that it offers much greater control over how your computer
works. This is an accurate observation, but it comes at the cost of greater
difficulty and increased complexity when configuring and interacting with your
system. If we consider that an accurate relative description of Linux
distributions, then BSD is the Linux of Linux.

Linux users (generally speaking) don't have to worry about loading specific
kernel modules at boot time, explicitly enabling services after they're
installed, or installing packages by building their own. FreeBSD peels off
another layer of abstraction over the OS, allowing for a lot more control. This
helps it run really lean.

It also comes with _very_ few software packages pre-installed, minimizing the
bloat of the operating system as well as its footprint on the disk. There's also
not much installed on the computer that I didn't specifically need or ask for,
which is comforting to me.

# 4. Because it's Simple

FreeBSD is designed to be as simple as possible, at least internally. This is
a boon because, as any engineer knows, simplicity is almost always more stable
than complexity. While a simple solution can require a bit more footwork in some
cases than a more complicated system that does a lot for you, it's much more
predictable. When trying to do something with some new software package, it's
often more predictable what it will do, and what you'll need to do to get it
up and running.

Simple design is incredibly difficult to achieve. It always comes with
tradeoffs that are difficult to compensate for, and it's easy to brush off its
benefits when you're trying to get something up and running. Linux makes it
easy to get some new software working, but it also encourages developers to
take shortcuts to make that easier. Without those shortcuts, you get something
much less bleeding-edge, but also much easier to work with once you know it.

# 5. Because I Like Staying Up-to-Date

It's true, Linux distributions tend to update more often than BSD distributions
do, and have more bleeding-edge features. But that advantage comes with a pretty
big downside - there's not a lot of backwards compatibility, and any time you
upgrade software that's critical to the core operation of the operating system,
there's the chance that it breaks some things there. Sure, the components are
more hot-swappable, but it doesn't do much good if you're afraid it might
bring your system down. Even if it doesn't, it's not unlikely that some software
packages may not be compatible with the new operating system. I've been burned
by this pretty frequently on Linux.

With FreeBSD, every update has been 100% safe and 100%
backwards compatible. You can upgrade packages and distributions without fear
of it breaking your system, which means there's less downside to staying
up-to-date. This keeps your uptime as high as possible, while still not becoming
outdated (and potentially security-vulnerable) for fear of downtime.

# That's All Folks!

I love my FreeBSD box. It's been so incredibly stable, and once you learn it,
it's a breeze to work with. If you like servers, I definitely recommend looking
into it. It's a great operating system for servers, especially with regard to
sustainability and maintainability.
