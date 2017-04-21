---
layout: post
title: Why Package Managers are Great - With a Focus on Homebrew
author: Eric Miller
category: Technology
tags:
---

I really like package managers. Often, I'll even get a bit preachy about them.
So guess what I'm going to do!

Package managers are a lovely piece of technology. Linux users will be very
familiar with the terminology, but the fact is most of us interact with them
regularly without even realizing it.

From [Wikipedia](https://en.wikipedia.org/wiki/Package_manager): *A package
manager or package management system is a collection of software tools that
automates the process of installing, upgrading, configuring, and removing
computer programs for a computer's operating system in a consistent manner.*

Sound familiar? That's what the iOS and Android app stores do. That's even what
the Windows and Mac app stores do. And that's really all this is: instead of
downloading an app off the internet, running it, and then having to dig around
for an uninstaller to remove it. Package managers take care of this for you.
Of course, a package manager also has even more upsides:

* If the software has any dependencies, the package manager will install those
automatically.
* You can easily update all of your software at once, or even automate it to
happen regularly.
* Most package managers are curated, so when you install something, you can be
confident that it came from a legitimate source.
* There is a unified interface for everything - there are no special steps to
install or remove software.
* Things install consistently - you don't need to choose an install directory,
or show the installer where the dependencies are - it takes care of everything.
* It uses sane installation options. You know how sometimes you'll open an
installer and it'll "generously" offer to change your search engine to Yahoo,
install 14 toolbars, and other goofy things? Package managers will disable those
by default (typically).
* It adds command line tools to your PATH automatically, so you don't have to
think.
* It verifies that your download hasn't been corrupted.
* It makes migrating to a new computer a breeze.

----

Traditional package managers operate using the
[command line](https://en.wikipedia.org/wiki/Command-line_interface). If you're
not computer savvy, this is probably intimidating. But I'll provide some options
regardless. For Windows users, [Chocolatey](https://chocolatey.org/) exists.
In my opinion, it's a bit incomplete, and somewhat poorly maintained, but to me
a mediocre package manager is better than none. For Mac, there are two good
options, [Homebrew](https://brew.sh/) and [MacPorts](https://www.macports.org/).
I recommend Homebrew, as it's simpler in my opinion, but MacPorts has its own
advantages. I won't wax philosophical about it here.

Package managers are particularly useful to people in software development or
IT, as they handle many of the intricacies that are easy to mess up. If you're
in those fields, and are not familiar with package managers, I highly recommend
taking the time to learn your way around them.

# So How do You Use One?

In this example, I'm using Homebrew, because it's native to my OS and I'm most
familiar with it. To install software, for example ruby, simply type `brew
install ruby`. To remove it, `brew remove ruby`. Easy. But what about installing
something bigger, like Java? Homebrew has a built-in extension for some packages
that were outside the philosophical scope of the original homebrew, called
Homebrew-Cask. To install Java, just run `brew cask install java`, and to remove
just `brew cask remove Java`. Again, easy.

Now you want to update your apps. For homebrew, just run `brew update && brew
upgrade -y`. The `-y` lets it know that you're sure you want to upgrade them, so
it doesn't ask you if you're sure. But wait! You don't want to upgrade something
because you need a specific version! `brew` has you covered. Just run `brew pin
something` and it'll stay at the version it's at.

Unfortunately, Homebrew (and Cask) is an incomplete package manager at this
point in time. This is one of the reasons MacPorts can be better. Homebrew-Cask
doesn't actually have an updater built-in, but you can install one with
[this](https://github.com/buo/homebrew-cask-upgrade). TL;DR: Run this:
`brew tap buo/cask-upgrade` to install, and `brew cu` to update your apps.
Unfortunately, it doesn't support pinning, so beware. Otherwise, you can update
manually with `brew cask remove something && brew cask install something`.

Finally, package managers can make migrating to a new computer a breeze. I don't
necessarily trust most migration software, so I tend to want to do it myself. I
also like to do clean installs, so any "gunk" my old computer accumulated
doesn't pass on to my new one. To do this, there are three easy steps:

1. `brew list > brew.txt && brew cask list > brewcask.txt && brew tap --list > btlist.txt`
2. Copy `brew.txt` and `brewcask.txt` to your new computer.
3. `cat btlist.txt | xargs brew tap && cat brew.txt | xargs brew install && cat brewcask.txt | xargs brew cask install`

Now all your software is on the new machine, in three steps and about two
minutes worth of work.

# Closing Up

Package managers have a bit of a learning curve at first, being command line,
but in the end they simplify things a lot. The funny thing is, I actually don't
know how to install most of the software I use, because I never have to choose
the installation directory, the options, or set up dependencies. I just type a
few words.

Think about how much the app store has simplified things. How instead of having
to hunt down a website and a tutorial and check whether the developer is legit
and forget to uncheck the box so now Yahoo is your search engine. There's one,
simplified way to do everything, that's safe and easy. That's what package
managers do.

And it's beautiful. 🍺
