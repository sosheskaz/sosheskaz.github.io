---
layout: post
title: The Intel Disaster
author: Eric Miller
category: Technology
tags:
---

It's a bit of a hot topic right now, still in the early stages: one of the biggest security bugs
ever.

Intel is a company that makes various components, but is most widely known for their processors for
desktop and laptop computers. They are by far the largest processor manufacturer, with up to 70%
market share, depending on your source. Processors power everything your computer does – in
computer science 101, they're called the main "brain" of the computer, which is fairly apt.
Everything your computer does touches the processor at some point.

Intel is the "quality" brand, the brand known for the best performance and the highest quality.

Which is why this is so embarassing.

Based on what we know now (this may change later), there's a major security bug in their hardware
going back to the Pentium Pro, released in 1995. That's over 22 years of processors.

# Wait a Minute, 22 Years? My Computer is From that Timeframe!

Yeah. Statistically, you're probably affected. All of my computers are affected. But just to be
safe, I'm going to lay out how to tell you how to find out if you are.

**NOTE**: If I don't explicitly say you're affected, it's uncertain whether you are or are not
affected. Only a select few people have the privileged detailed information on this design flaw,
and I am not that important.

## Macs

1. If your Mac is model year late 2006 or later, you're affected.
2. Go to  in your menu bar, then to "About this Mac". Look at the part that says "Processor". If
   "Intel" is in there, you're affected.

## Windows

1. If your computer has an intel processor. It probably shipped with an "Intel Inside" sticker or
   something. If your computer has such a sticker, you're affected.
2. Open "Control Panel". Click "System and Security", and then "System". There will be a field on
   that page that tells you your processor type and speed. If "Intel" is in there, you're affected.
   If it says "AMD", you're safe. If it's something else, we're not sure yet.

## Linux/BSD

This is left as an exercise for the reader. You set up your system, you figure it out.

# Okay, so I'm Affected. Now What?

## Macs

Apple has [already patched](https://www.macrumors.com/2018/01/03/intel-design-flaw-fixed-macos-10-13-2/)
the issue. Just make sure to update, this one's pretty serious.

## Windows

Microsoft has already dropped a patch as well – make sure you get the latest updates right now,
this isn't one to skip.

## Linux

The folks in charge of the Linux kernel are working on it. They should drop a patch soon.

## FreeBSD

Because I play favorites with FreeBSD, I'm including it here. I'd imagine that they're racing for
a patch (**if** they're vulnerable), but they don't have the resources that the Linux folks do. At
this point, I haven't found any reliable sources. However, based on *unreliable* sources, it looks
like FreeBSD may not be vulnerable.

# Wait, so if it's Already Patched, Why is it so Bad?

This is bad. Very bad. Like I said, one of the worst vulnerabilities ever, and certainly the worst
in the time I've been paying attention to the industry.

## The Reach

This affects a ***LOT*** of computers. As you could see earlier, it's extremely widespread. It's
also a very big flaw – according to sources, even Javascript in web browsers may be able to exploit
it. That means, in a worst-case scenario, your machine could be attacked by some stupid ad on some
stupid website.

## The Severity

This flaw isn't the *worst* possible thing that could happen to your computer, but it allows the
attacker to see some information that they *really* shouldn't be able to see. What kind of information?
Well it's complicated, and we're not really sure yet (again, very select few people know). I will
go into some more detail (it's more technical than how I usually write, but there's just no way
around that here).

## The Solution

The benchmarks aren't in yet, but it's estimated that the "fix" will slow down computers by 5%-30%.
Based on what I've seen, I'd guess it's about 15%. But trust me, this is a really, **REALLY** bad
security flaw, and you want the patch.

Yeah. That's how bad it is. We're nerfing our computers by potentially 30%, and it's **still**
better than the alternative.

# What is Intel Doing About This?

Not much. They released a processor with a feature that was broken, and now that operating systems
have taken advantage of that feature, there's not really anything they can do. They can't just
patch it, the problem is with the physical hardware.

The CEO of Intel sold off $24 million worth of stock when they became aware of the issue. Intel
stock dropped 3.39% today. I'd expect it to drop quite a bit more once the fixes get rolled out
and people learn why their computers are so much slower.

# Why Do We Know So Little?

Responsible disclosure. Responsible disclosure is the generally-agreed-upon process for turning
over knowledge of a security flaw to the appropriate people. Basically, it works like this:

1. You find a security flaw.
2. You notify the people who need to fix it. You tell them that you will release full, detailed 
   information to the public and the press in a fixed amount of time (usually 30 days).
3. The company makes and pushes out a patch within the time period given.
4. After the 30 days pass, you release everything you know to the public.

This process isn't perfect. At the end of it, the information is released, meaning that any bad
actors who want it can learn to exploit it on anyone who didn't update. However, it also means that
consumers and consumer
advocates (there are lots of them in the tech world, though they don't usually call themselves
such) can make informed decisions. It also *forces* the person who can fix it to release a solution
in a timely fashion.

Right now, we're in the early stages of this process. This flaw is big enough that basic
information has been released to the public one way or another, but all of the details are in the
hands of the people responsible for fixing it.

# So What Is the Bug, Actually?

That is a difficult question. Partially because, frankly, I'm not qualified to answer it. Partially
because details are still hidden from the general public. Partially because it's a "low-level"
problem, and "low-level" is computer-science-speak for "Here There Be Math Dragons". But I'll do my
best.

I can't describe this without using technical words and descriptions. You have been warned.

In operating systems, there are lots of spaces. What we're concerned about here are "userspace" and
"kernelspace". "Userspace" is the part of the computer that lets the user do things, and that is
concerned about what the user of the computer wants to do. So if you're running an app, that app
exists in userspace. Kernelspace is the part of the computer that handles the bookkeeping and
administrative tasks. It decides what processes can run when. It controls access to shared system
resources, like RAM and the hard drive. When a userspace process needs to do something particular,
like save a file to disk, it needs to send the file through the kernel, and through kernelspace.

Think of it like going on a vacation with a travel agent, where you're the user and the travel
agent is the kernel. You need a plane ticket? You tell the kernel that you need it, they figure out
the details, and give you back the plane ticket. You need a hotel? Same thing. What you do on the
plane, and what you do in the hotel, are things only you need to deal with, but the kernel gets a
lot of information about what you're doing and where you are just because they're going through
them. You just expect the kernel to keep your information private, because that's part of your
agreement.

Now is where I lose my ability to metaphor. Also, the following information is largely speculative,
but it comes from decent sources. It's also based on my understanding, which comes up a bit short
in this particular area.

Basically, some processors (including Intel's) use some technology that allows the kernelspace and
the userspace to share some of the same "pages" in memory. The processor (supposedly) keeps them
separate, no matter what, as long as it's set up properly in the operating system. Because the
kernel often needs information from userspace, this can speed things up a lot.

The problem is, since the kernel handles information from every process, it *has* information on
every process, that's supposed to be secret. The exploit somehow allows userspace to access the
kernelspace on the same "pages" as their own data. Since kernelspace can contain data from any
process, this could include anything. It could include all your passwords, it could be mostly
empty, it could contain those pictures of cats you saved. But, even though I'm putting it in (relatively) simple
terms, it's important to remember that **everything** in kernelspace is supposed to be
confidential, and that there are lots of things computers do behind the scenes that could do a lot
of damage to you personally if they fell into the wrong hands.

Modern operating systems have been designed around the idea of this working, and working
*correctly*, for at least a decade. And now we find out it's all garbage. And it's not just a
problem in code that can be patched up and pushed out, it's a physical flaw in a physical device
that's the root cause. So the "fix" is to simply turn it off – one of the oldest and most tested
ways of speeding up computers. That's why the fix is such a big slowdown.

Hope you didn't buy too much stock in Intel.
