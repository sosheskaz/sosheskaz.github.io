---
layout: post
title: The Case for the Artificial Sciences
author: Eric Miller
category: Technology
tags: 
---

The two traditional branches of science are the natural sciences (such as physics, chemistry, and biology)
and the social sciences (such as sociology, psychology, and anthropology). Computer science falls into 
neither of these categories, as it is neither a study of the natural world nor a study of human society.
It's been argued that, because of this, the term "Computer Science" is a misnomer, instead relegating
Computer Science to the realm of mathematics. That said, I have some problems with this.

First, let's take a look at how sciences typically form, and how they are used in our society. Let's look
at physics as an example. It essentially has three layers of study that, when used together, cover its 
study as well as its application in society. The top, and purest layer is mathematics, in particular 
calculus. Second comes physics itself, which is the study and understanding of physical phenomena using
mathematics to quantify it. Third comes the various forms of engineering which use physics as a basis for
their application, such as mechanical, civil, and electrical engineering. Of course, these forms of
engineering often draw from other sciences as well, such as from Chemistry for material analysis.

Computer Science itself follows this pattern very closely, though due to the recent and rapid emergence,
all three layers I just described are called "Computer Science". At the top of the pyramid is mathematics,
in particular number theory. Second comes the use of these mathematics in practical terms, which is what
is largely considered "theoretical computer science". Finally come the concrete applications of these 
ideas, which manifest in software engineering and computer engineering. This means that if we look at the
central layer, theoretical computer science, it seems to be functionally very similar to more traditional
sciences. One of the peculiar and unique things about this field, however, is that engineering shapes
science. As new things are created, the field of science is broadened. This is due to its nature as what
I call an "artificial science" - it is shaped by human endeavors and advances. 

----

From this point on, I'm going to change my terminology somewhat to try to rectify the vernacular problem
I mentioned at the top of the previous paragraph. When I say "Computer Science", I'll be referring to the
second tier in the hierarchy I described above. When I say "Computer Engineering", I'll be referring to 
both software and computer engineering, unless otherwise specified. 

----

The main problem with calling computer science a science, in my opinion, is that there's a lot of blurring
of lines between these three tiers. Many academics see computer science not as a science, but as 
mathematics, because of the nature of computers themselves. Computers are, essentially, pure mathematics
projected onto a human-created device. Then, it makes sense that it would be wholly considered to be a
branch of mathematics.

But this is incorrect. The logic is sound, but it has an implicit premise that is incorrect, and thus
the conclusion itself must be reevaluated. That premise is that computers are pure applications of 
mathematics. The fact is, they're not; the nature of computers is *based* on mathematics, but is muddied
by practicality.

From a fairly low level, computers are fairly pure mathematics. It's often taught that binary was chosen
as the base numbering system for computers due to practical constraints, and while there is some truth
to this, it's not the whole story. Many of the circuits used in computers, especially the memory cell
circuit (how computers have short-term memory) depend on boolean algebra and mathematical logic. Adapting
these circuits to work with other number systems would be difficult and complicated, and any gains from
using a more efficient number system would likely be lost by the increased size and complexity of the 
new circuits required.

However, as we get more abstract, things get muddier, less pure, and more arbitrary.

# Programming Language Theory

Programming language theory is a subfield that was born over time through more and more developments in
programming languages and hardware improvements. At first, it was fairly simple. A computer would be 
hard-coded to do certain things when certain sequences were given to it as an instruction. For example,
`000000` could mean "Add". In the implementation I'm using, an additional `00000100000` is required at the
end. Then, more information is passed to tell it what to add and how. So we give it
the addresses of two "registers" where these numbers are stored, for example `01010` and `01011`. Finally,
we need to tell it where to put the result, which could be register `01001`. This gives us the full
instruction `00000001010010110100100000100000` that tells the computer exactly what I've just described.

The argument that this is pure mathematics with totally arbitrary choices on top of it is a fair one, so 
the corollary argument that this is still pure mathematics holds up.

The next stage was assembly language. It's basically just a shorthand that sits on top of this binary 
layer of instructions. So, for example, the same thing we just did could be described as 
`add t1 t2 t3`. Much easier, right? We're ADDing, putting the RESULT in register t1, and the INPUTS we're
using are the contents of registers t2 and t3. This decodes to the machine language instruction above.
Now we're getting closer, but this is still just an arbitrary layer on top of the previous. It's exactly
the same, just a bit easier to read for humans. We're still not doing anything too interesting.

But then things like COBOL and C started happening. Take a look at 
[this](http://www.csis.ul.ie/cobol/examples/Perform/MileageCount.htm). It's an example of a simple COBOL
program. It's a lot simpler and more intuitive than messing around with registers and carefully describing
every single minute operation. Over time, these abstractions got bigger and bigger, until we're no longer
looking at things that are even close. Let's look at a few examples that illustrate how much simpler
and more abstract programming has gotten, to the point where these instructions are no longer 
recognizable.

## 1. SQL
SQL stands for Standard Query Language. It's used in a lot of common and mature databases to read, 
modify, and create data. Here's an example line of SQL - you'll probably be able to tell what it's doing,
even if the terminology is a bit specific.

    SELECT first_name, last_name, phone_number FROM contact_list WHERE state='WI';
    
It looks in our "contact list" database table for people who live in Wisconsin, and grabs their first
name, last name, and phone number. Imagine turning that into assembly language. What's more, it's
incredibly fast. There's no real math here - it's based on efficient and easy writing.

## 2. Java
Java is probably the single most popular and in-demand programming language. Traditionally, the way 
programming languages work is this: Something called a "compiler" looks through the code, figures out
what it means, and translates it into assembly language or binary in as optimized a way as it can think
of. The result can then be fed into the processor, and it will run the program as desired.

Java works similarly, but with a very important distinction. Compiled Java programms *cannot* run on the
CPU naturally. Instead, you have a "virtual machine" that it's compiled to run on, and the virtual 
machine itself is the only thing compiled for the CPU. This isn't mathematical at all - it's a practical
method of writing programs that can run on almost any machine. It can't be described as mathematics - 
it's a phenomenon.

## 3. Python
Python is another popular programming language, especially for web applications and automation. Python
isn't compiled at all. Like Java, a compiled "runner" exists for whatever computer it's running on, but
it reads the code and interprets it in real time. Again, this goes beyond pure mathematical abstraction.

## So What?
This creates a problem in the viewpoint that computer science is pure mathematics, but saying it's a 
science is still a stretch. So, in order to justify my assertion that computer science *can indeed* be
considered a science, I'm going to show that programming language theory can be considered a science.
If one branch of computer science can be considered the science, then computer science itself can be
considered a branch of science if it's defined sufficiently clearly and precisely.

From [Wikipedia](https://en.wikipedia.org/wiki/Natural_science), *"Natural science is a branch of 
science concerned with the description, prediction, and understanding of natural phenomena, based on 
observational and empirical evidence."*

I'm going to create my own parallel definition of "Artificial Science" following this structure, and show
that programming language theory meets these criteria. My argument, then, is that if it functions just 
like natural science, but with respect to the artifical, it can reasonably be asserted that artifical 
science is a valid field. My definition follows:

*Artificial science is a branch of science concerned with the description, prediction, and understanding
of phenomena of human technology, based on observational and empirical evidence.*

Now, let's trim that to describe how programming language theory meets the criteria of a subscience.

*Programming language theory is a sub-branch of artificial science concerned with the description,
prediction, and understanding of programming language phenomena, based on observational and empirical
evidence.*

----

So, we now have a few things to prove. We need to prove that programming language describes, predicts,
and understands programming languages, as well as that this is based on observational and empirical
evidence.

----

## Some Background Information
I have some information here that I'm going to utilize for the discussion, so I want to make sure my 
readers and I are on the same page for a few things.

Within programming language theory, there is a discussion of two different kinds of programming, 
[imperative and declarative](https://tylermcginnis.com/imperative-vs-declarative-programming/). 
Essentially, the difference is that imperative tells the computer *what to do
and how to do it,* while declarative tels the computer *what to do, and leaves the how up to the
computer.* This description is pretty relative, but it becomes important. This definition is kind of 
hard to understand at first, so I recommend taking a look at that link, up until he goes into actual
programming examples.

In programming, there's something called code quality. Code can be awful, even if it works. Code can be
beautiful, even if it doesn't quite work right. In the words of Peter Welch, good code "reads like 
poetry written by someone over thirty." People have come up with various ways to quantitatively measure
some aspects of code quality, one of the most popular being 
[Cyclomatic Complexity](https://en.wikipedia.org/wiki/Cyclomatic_complexity). In general, a score of over
50 is considered "untestable" (this is a problem) and a score of over 100 is considered "unmaintainable"
(this is a **BIG** problem). Essentially, it looks at
your code and spits out a number, telling you how good it is and how maintainable it is. The lower the
number, the better it is. Interestingly, this measure has actually been used in court to show that a 
company (in this case, [Toyota]()). Their code scored a 146. 

## Onward to Proof!
Now that that's cleared up, let's get down to brass tacks.

Cyclomatic Complexity gives us empirical and observable evidence of code quality. Let's consider code
quality as our dependent axis, while we look at imperative vs. declarative as our independent axis.

Imperative is the more traditional of the two types, given that it's fundamentally simpler to create
and is still more common in computer science. However, declarative programming has been growing more
popular. Why? Because of our empirical evidence.

Because declarative programming leaves more minute details up to the computer, a few things happen.
First, it tends to be faster because the computer can perform more optimizations. Second, it winds up
being vastly simpler code. Simpler code means a lower cyclomatic complexity, which means the code is 
more testable, more maintainable, and more stable.

As a result, people have been predicting a greater shift to declarative languages and paradigms in 
programming, as well as development of new language features that follow declarative paradigms. We can 
also predict that lower-level languages, which are more imperative, will have higher cyclomatic 
complexities than their higher-level declarative counterparts, and thus will be less robust.

So there we go. Observable (in the actual success and failure of programs and languages) and empirical 
(in the form of things like cyclomatic complexity) evidence that are used to describe (such as 
describing the differences between imperative and declarative) predict (predicting changes to 
programming languages, as well as future successes and failures), and understand (using this information,
we can dig into *why* declarative winds up behaving better than declarative) the phenomenon of 
declarative and imperative language performance differences.

This means that, at the very least, programming language theory *behaves* like a science. Further, it
can't be described by mathematics; cyclomatic complexity can be, but these phenomena are studied and used
in engineering. It's also not the field of engineering itself, because it's not intrinsically creating
anything. It occupies a space analogous to physics in the mathematics-physics-engineering hierarchy.

Computer science is an incredibly vast field. Much like the other sciences, people often to specialize in
one, or a few specific areas. Basic programming language theory is something I'm familiar with, but there
are countless other examples. Security, user experience, file systems, computer vision, artificial
intelligence, and so much more are all fields that are as wide, or wider, than programming language
theory, and occupy the same spaces. If we decide that the amalgamation of these fields is "computer 
science", that the mathematics are "computer mathematics", and the implementation is "computer 
engineering", it begins to look and behave very much like any other science.

If it is functionally the same as other sciences, which I've argued that it is, then it makes sense to
include it under the umbrella of "the sciences". But it's also not broad enough to merit being its own
primary branch of the sciences, like natural or social. Therefore I propose that we consider a new 
primary branch of science, "artificial science", concerned with the study of complex systems created by
human beings, of which computer science will be the first member. As we advance further, there will no
doubt be more - and we'll have a way to describe and categorize them.
