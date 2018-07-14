---
title: Project Awful
author: Eric Miller
layout: page
permalink: /project-awful/
---

I'm a big fan of software that provides dubious or negative value. This page is in honor of that
idea. I'll link to anything I've made that's Awful, and anything I've found from other people that
I find particularly uninspiring. If you have software you'd like to see here, let me know and I'll
see if I think it belongs here.

Honorary mention: [The Stupid Shit No One Needs and Terrible Ideas Hackathon](http://www.stupidhackathon.com)

----

## Criteria

Code doesn't have to meet all of these criteria. In fact, meeting just one substantially well and
Awfully is sufficient to put it here. So what are these criteria?

* Value to society. Is the program pointless? If so, it's a good candidate.
* Accomplishes its goal. Anyone can write a program that doesn't work. For software to be Awful, it
has to at least basically work sometimes.
* Uses pointer hacking or does other, similarly stupid things.
* Steamrolls errors or rewrites its own code. The
[Wheeler Jump](https://www.youtube.com/watch?v=zR8V0lq029c) is a good example of what I'm getting
at here.
* Shows code to the user, fails to work under random conditions, has Awful error messages, or
otherwise shows sloppy implementation details to the user.
* Code Golf. The less characters it took to write, the ~better~Awfuller, generally speaking. A bigger
codebase is more prone to bugs, true, but it's also likely to have better error handling. And error
handling is not Awful.
* Code Quality. The less readable the code is, the better. For example, a crappy program may be
bad, but a crappy program written in [Ook](https://esolangs.org/wiki/Ook!) is really awful.
* Malicious Compliance. Technically complying with best practices in order to make itself less
readable or functional is an Awful thing.
* "You're holding it wrong". Changes whether it works well or poorly based on seemingly random
differences in how it's used.

## What ISN'T Awful?

I haven't found any software that isn't at least a little bad. But to be Awful requires something
more. So I'm going to make a list of things that aren't awful.

* Stupid or generally ugly UI.
* Generally unhelpful error messages.
* Random crashes (unless comedically timed or caused)
* Generally crappy code.

## Project Awful!

### fuckit.py

[fuckit.py](https://github.com/ajalt/fuckitpy). The Python Error Steamroller. Anything I write
won't do it justice, so just go check it out.

| Criteria                | Status                                                                   |
| ----------------------- | ------------------------------------------------------------------------ |
| Value to society        | Actively makes code worse.                                               |
| Accomplishes its Goal   | It steamrolls errors all right.                                          |
| Stupid Things           | Live edits the call stack and rewrites the syntax tree.                  |
| Steamrolling            | Literally called "the Python error steamroller".                         |
| Detail Exposure         | Screws up stack traces sometimes, nothing too Awful though.              |
| Code Golf               | 183 significant lines at time of writing. Not bad. Pretty Awful, really. |
| Code Quality            | Pylint rates it at a 6.7/10. Readable. Uses too many best practices IMO. |
| Malicious Compliance    | None really.                                                             |
| You're holding it wrong | The author actively fixes problems when people report them.              |

&nbsp;

### NoColon

[nocolon](https://github.com/paradoxxxzero/nocolon). Removes the need to use colons in Python,
because colons are *unpythonic*.

| Criteria                | Status                                                                        |
| ----------------------- | ----------------------------------------------------------------------------- |
| Value to society        | Pointless.                                                                    |
| Accomplishes its Goal   | Does its job, but doesn't work in some specific conditions.                   |
| Stupid Things           | Live edits code as it's being imported.                                       |
| Steamrolling            | No steamrolling used.                                                         |
| Detail Exposure         | N/A                                                                           |
| Code Golf               | 52 significant lines at time of writing. Good job!                            |
| Code Quality            | Pylint rates it at a 4/10. Readable. No code comments.                        |
| Malicious Compliance    | Makes fun of the idea of being "pythonic" by doing stupid, unpythonic things. |
| You're holding it wrong | Just doesn't work in lots of edge cases.                                      |

&nbsp;

### SiriSings

It may be a bit of a faux pas to promote my own stuff here, but damn it I'm proud.
[SiriSings](https://github.com/sosheskaz/sirisings) is a command line app for mac that allows you
to put in words and have a siri-like voice sing a song found based on those words. You can install
it with `pip install https://sosheskaz.github.io/pypi/sirisings.zip`

| Criteria                | Status                                                                         |
| ----------------------- | ------------------------------------------------------------------------------ |
| Value to society        | Creates unpleasant sounds.                                                     |
| Accomplishes its Goal   | Works pretty well, doesn't work right sometimes.                               |
| Stupid Things           | Disables warnings using the shebang.                                           |
| Steamrolling            | Performs no checking of whether or not the song it found is actually singable. |
| Detail Exposure         | Will sometimes "sing" HTML tags to the listener when it screws up.             |
| Code Golf               | 54 significant lines at time of writing. Good job!                             |
| Code Quality            | Pylint rates it at a 10/10. Readable. Intentionally bad whitespacing.          |
| Malicious Compliance    | Uses technical compliance with PEP-8 to make it less readable.                 |
| You're holding it wrong | Doesn't work for instrumentals or seemingly random, specific songs.            |
