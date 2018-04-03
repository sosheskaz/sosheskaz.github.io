---
layout: post
title: General Purpose Computing – Then and Now
author: Eric Miller
category: Technology
tags: technology apple general purpose computing history
---

The term "general purpose computing" is kind of a strange term. Until I was introduced to it within
the context of computer science history, it didn't make much sense. I want to talk about the future
and some interesting developments happening within the computer industry, but that's really
impossible without looking at how computers came to work like they do now.

## Before General Purpose Computing

In the 1940s, computers were machines of war. They were for calculating the trajectories of
explosives, making aeronautical calculations, and so on. As former government employees who built
computers moved into the private sector, the technology started to come to market. Computers were
then used largely for high-level number crunching, in particular payroll. However, because of their
extremely high price, they were really only used by the largest customers who had a massive amount
of information to process.

There was a push to specialize the machines, which was somewhat natural at the time. The idea was
basically that one computer would only do one thing – for example, if a computer was only ever
going to be used for payroll, why bother making it versatile enough to be used for anything else?
Lots of companies decided to capitalize on that idea, and move in on that opportunity. They went
out of business.

## General Purpose Computing Wins Out

In the 50s and 60s, the computer science industry was growing very, very fast. Computers jumped from being
super-exclusive artifacts saved for the military to doing hardcore processing in large business and
science. Hobbyists were getting into it, in the same way that people are interested in HAM radio. 
It went from a hyper-inclusive field to something that affected all sorts of people, even if they
weren't interacting with computers directly.

----

In the first half of the 20th century, a manufacturing methodology called "Lean" started catching
on. It made huge improvements in efficiency, and made the manufacturing that fuels our lives today
possible. It maximized the speed, efficiency, and scale of manufacturing, and made it possible to
build things better and cheaper.

----

Between the lean methodology, the rapid growth in the industry, and how wide it spread, a perfect
environment for general purpose computing was formed. It shaped the way we think about computers,
to the point where what were radical ideas now seem like the intuitive way to do it. For example,
it was a radical idea to store the data a computer processes, and the program it uses to process
it, on the same device. Now days, we don't even think about doing it any other way. After all, to
the hard drive, the programs and the data they run are both just chunks of binary.

Ideas like that one took off across the entire architecture of the computer. Instead of hard-coding
a processor to work with one kind of data, they'd make one that could do everything reasonably well
and specialize it in software. This allowed the people building computers to sell their products to
a much larger audience. Since they could sell to a larger audience, they could benefit from
[economies of scale](https://en.wikipedia.org/wiki/Economies_of_scale), allowing them to make
components cheaper and cheaper to manufacture, and spend more and more money on research and
development. This essentially meant non-stop breakthrough developments and upsets for people in
general purpose computing, while specific purpose computing would flounder because they couldn't
compete with the huge markets and low prices of their general purpose counterparts. And of course,
general purpose processors could be swapped out as rapid advancements were made, making using them
a lot cheaper over time.

----

## Rethinking General Purpose

General purpose computing dominated the industry for the last half of the 20th century. However, in
the 21st century, we've been seeing particular industries creating markets for much more specialized
components. In the 19th century, general purpose computing could keep pace just because of how
incredibly rapidly the power of computers was growing. These days, however, we're running into more
and more problems. With 21st century manufacturing technology, we can only make transistors so small,
can only cram so many billion transistors onto a piece of silicon, and can only run processors so
fast before they start combusting. The laws of thermodynamics have not been very kind to our desires
for faster and smaller processing chips.

These days, specific purpose computing is growing more and more. The market is more inundated with
general purpose computing power than ever before, thanks to cloud providers like Google and Amazon,
where if you have a big enough credit card, you can rent a fleet of virtual computers with thousands
of processors between them by the hour.

And yet, with this incredible amount of computing power at our fingertips, new inventions in
high-performance hardware continue. On the most basic level, we can look at graphics processors
and solid state drives as great examples. It's become very common for computers, especially gaming
or animation computers, to have multiple of the same kind of component so that they can be
specialized. Many computers have a graphics processor in addition to a central processor, just to
speed up certain kinds of operations. Many people use a solid state drive to store their programs
to load as fast as possible, and a slower disk drive to store large amounts of data. Going back to
how storing programs and data on the same device was the way of the future, we're now moving away
from it.

Even the kinds of processors we use has been branching out. In processors, there are two popular
architectures: x86 and ARM. x86 is fast but inefficient, while ARM is slower but much more
efficient. The result is that, when manufacturers are building a device, they now have choices to
make about which specialized processor is better for what they need to do.

## The Economics of the Resurgence of Special Purpose

What makes this possible? Well, the same economies of scale that made general purpose computing
take off are now working against it, and the rapid year-over-year advances in computing power
are... no longer quite so rapid.

Economies of scale. The more you produce, the less it costs you to make an individual unit. This is
the market force that drives why buying wholesale is cheaper than buying small-scale, and why
short-run manufacturing is so expensive. However, there's a limit to that effect; the bigger you
get, the lesser the effect gets. There are only so many places where you can reduce cost on a
per-unit basis thanks to up-scaling your operation.

The computer industry is utterly huge. If you're making a specialized component that caters to one
group of peple, that group of people is realistically big enough that you can get most of the
effect of an economy of scale just by specializing. That levels the playing field between general
purpose and new-generation specialized purpose computing. And because the devices you're selling
are specialized, they can run circles around their general purpose counterparts in their chosen
activity. And general purpose computing can't keep up, because there's only so much you can do
with electronics before the laws of thermodynamics start to blow things up.

## Apple & Special Purpose in Embedded Electronics

Because this blog is what it is, and many roads lead back to Apple, I want to bring up some things
that they're doing that are interesting considering these trends.

If you keep up with the iPhone and iOS changes, you probably know that Apple is *cramming* as many
"coprocessors" as they can into their electronics. There are coprocessors for motion tracking,
image processing, and sound processing. New MacBook Pros ship with a coprocessor just to run the
touch bar. iPhones use specialized processors with different levels of processor cores that switch
out depending on whether they need maximum power or should run more power-efficiently. And because
they're a company with such a huge market share, they're uniquely well-suited to capitalize on the
economies of scale that specialized computing can take advantage of these days.

----

## What Happens Next?

When I learned about general purpose computing, and its history, I was surprised that Apple was
trying so hard to specialize their coprocessors. After all, it was historically shown that
general purpose computing just wasn't profitable. With how sophisticated their main competitor,
Google is, I thought that it might be a misguided attempt at claiming relevance that would
ultimately lead to making their products fail to keep up even more.

But looking at it deeper, I think that we're at the beginning of the rebirth of specialized
processing, in a new form. General purpose has been pushed far, and it's not going anywhere, but
it's just not a complete solution anymore when it can't keep up with general purpose computing
that's integrated with other special purpose components.

Ultimately, I wouldn't be surprised if we look back on the techniques being used to create
coprocessors today as the pioneering efforts that ultimately make incredible things possible in the
next few years (and decades?). I think that this is going to ultimately prove to be a very big
deal, starting in consumer electronics and working their way up as the techniques involved in these
kinds of coprocessors.
