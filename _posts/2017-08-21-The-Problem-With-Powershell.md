---
layout: post
title: The Problem with PowerShell
author: Eric Miller
category: Technology
tags:
---

In my past life as a Windows/.NET developer, I spent a lot of time working with various parts of the
.NET world, including PowerShell.

For those uninitiated, the .NET framework is the framework Microsoft has been increasingly
pushing for development for their operating systems. Multiple programming languages in the MS world
use this same framework - it's made to work well across different programming languages. The most
popular languages for the framework are C# (one of my favorite programming languages, right next
to Swift), Visual C++, Visual Basic, F#, and PowerShell. It's a powerful and, in my opinion, very
good framework.

So then what is PowerShell? PowerShell is a very novel and inspired idea. The idea behind it is that
you have an interpreted shell (like bash), but it has the full power of a proper programming
language behind it, making it much more flexible. This is an intriguing idea, but it hasn't been
tested enough to comment on how effective it is.

Now, it's worth noting that PowerShell is not the first language that brought the power of a full
programming language to the shell. Interpreted languages like python and ruby have interactive
shells as well. However, using them in that way comes with a lot of overhead and problems. They
don't have the same kind of support for things like customization, syntax highlighting, and
auto-completion that "true" shells, like bash and zsh, have. This makes the shell sometimes nice
for some quick testing, but utterly lacking for full-time interactive use.

PowerShell tries to remedy this problem by focusing more aggressively on being useful as a shell
while still retaining that complete .NET programming language support. To an extent, it succeeds -
it allows access to all of the executables on the `PATH` (a list of locations on the disk where
programs are stored, allowing them to be started by name rather than specifying their exact
location on the disk every time), it has syntax highlighting and autocompletion, and it has all of
the other features that you'd expect from a standard shell.

But a problem arises. On \*NIX systems, the shells are built on a few ideas. Require as few
keystrokes as possible to invoke a command. Many smaller utilities that perform very specific
functions, and perform them well. This ecosystem has had decades of developers working to create
useful tools for the system, and building on each others' work. Windows doesn't have the same kind
of history, and PowerShell attempts to cover for that by making the full features of the .NET
framework available. Considering MicroSoft's position, I don't think this is a bad idea.

This could've been executed really well. It could've even been a game-changer, making the \*NIX
shells look like trash and leaving them in the dust. 10 years later, MicroSoft has admitted this
has not happened, even going so far as to release the abomination so sillily called "Bash on
Ubuntu on Windows"

And they screwed that up too.

# The Autopsy

So why did PowerShell fail to live up to its potential? Let's pick it apart.

## 1. Cmdlets

You know, this could've worked. They needed to address the lack of CLI utilities on Windows for this
language, and so the natural response is to make some of them yourselves. They largely succeeded,
but this failed on two important fronts. First, the way they take arguments and return values is
too verbose and complicated. Because it has the full power of a programming language, the developers
of the language got greedy, and made all the interaction use _objects_. Look at bash. Does it have
objects? No. Not that you're exposed to, anyway. Why is that? Because when typing commands into a
terminal, your keyboard doesn't write _objects_. It writes _text_. This means that if you want to
invoke a cmdlet, which should be a simple one-liner, you have to consider how you're going to build
the objects to give it as input, and figure out how to store the output. That's adding a lot of
complexity and throwing it on the user's plate, which for an interactive app (which a shell _is_),
goes against User Experience 101.

The second problem that cmdlets run into is their names and their wordiness. Let's look at the
command to download the google.com webpage on Windows, and on \*NIX.

```PowerShell
Invoke-WebRequest -Uri https://google.com -OutFile google.txt
62 characters
```

```bash
wget -O google.txt https://google.com
38 characters
```

That's 63% more typing to accomplish the exact same thing. Another thing to note is that PowerShell
likes to throw hyphenated names everywhere, while bash keeps it simple and lowercase. PowerShell
also considers it "bad form" (though legal) to not capitalize words. This adds more typing time and
keystrokes.

So overall, the cmdlets are more complicated and take longer to type, which, while it sounds benign,
is critical for something intended to be used interactively.

## 2. Flags and Options

My last point reminded me of this. _NIX has developed an extremely efficient way to process command
line arguments. When writing my own apps (I usually use python), I usually try to find a tool that
will let me follow this format as closely as possible. It goes like this: Single-letter arguments,
called flags, don't require space after them. This means that, if you're setting a few modes at once
(for example, `tar -xvzf`) you don't need to put spaces between them. If one of these requires an
argument, you don't need it either - so if you needed to run a hypothetical program in 'quiet' mode,
you could add on `-mquiet`. This shorthand lets you write things a lot faster and more compactly,
and yet somehow, is actually easier to read (to me, anyway) than the verbose PowerShell style of
writing out _everything_. If you need a longer, more specific parameter, you just put two dashes
(`--`) instead of one, and write it out. Overall, this is cleaner and easier to read.

## 3. Remoting

*NIX systems have had SSH (Secure SHell) for ages. It's a foundational and ubiquitous way of doing
things that is secure and easy to use. It all works the same way, and it does all of the negotiation
between client and server behind the scenes. You can even use FTP over SSH to transfer files
securely between host and destination. It's been around since 1995. PowerShell remoting, on the
other hand, was released in 2009, runs over HTTPS, and isn't nearly as well-integrated as the SSH.

Let's say I want to SSH to a machine with my username and password. Here's roughly how it goes:
```bash
ssh ericmiller@mycomputer.net
Enter Password:
```

Pretty easy. Let's see the same with PowerShell:
```PowerShell
New-PSSession -ComputerName mycomputer.net -Credential ericmiller -UseSSL
Enter Password:
```

Again, look at that character count. 147% more characters to do the same thing, plus there's more
work to look up flags, as opposed to the *NIX-standardized user@machine nomenclature. If you're
using LDAP you have to specify the domain too - whereas \*NIX/SSH will automatically figure it out.

As a side note, SSL isn't enabled by default. That's a stupid default. I don't know what they were
thinking, especially considering that SSH had it figured out **14 years** prior. Dissapointing 😔.

# Why Did MicroSoft Fail at This?

This is pretty subjective, and the best we can do is guess. But my opinion is that they were too
closed-minded when it came to building PowerShell. On *NIX systems, these programs were built and
refined over time by multiple people all arguing about what would be a better way to do things. My
guess is that, while developing, they had a bunch of Windows people who didn't have the \*NIX
background to understand what had made \*NIX shells successful, or who maybe even didn't bother to
understand what users wanted. Or maybe they didn't understand, and brushed it off saying that the
users didn't know what they liked. I really can't say. What I can say is that it wasn't built with
due consideration of UX or of its predecessors, and for that reason, it fell flat.

# Cause of Death

Developers didn't give due consideration to their users' needs.

# Shell on Windows

Don't bother with PowerShell. If you want a usable shell on Windows, use
[CygWin](https://www.cygwin.com) and either [Cmder](https://github.com/cmderdev/cmder) or
[ConEmu](https://conemu.github.io). It leaves a lot to be desired, but it gets the job done and is
the best thing I've found. Between the *NIX utilities that Cygwin gives you, and the nicer UI of
Cmder/ConEmu, you get something usable.
