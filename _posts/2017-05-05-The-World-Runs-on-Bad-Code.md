---
layout: post
title: The World Runs on Bad Code
author: Eric Miller
category: Technology
tags: 
---

Code quality, the savior of, and the bane of, programmers.

Writing code is easy. I really do believe that with effort and willingness to learn, just about anybody
can write a simple program. The challenge, however, is writing good code.

In the paraphrased words of Peter Welch (a lot of this post is inspired by his essay, 
[Programming Sucks](https://www.stilldrinking.org/programming-sucks), and its counterpart by a different
author, 
[What Programming is Like](http://blog.samstokes.co.uk/blog/2014/05/01/what-programming-is-like/)), 
good code reads like poetry 
written by someone over thirty.
Expounding on this idea, it's quite accurate. Good code is descriptive without being obnoxious, neither 
too concise nor too verbose, carefully thought out, well organized, and has a nice rhythm. 

And it's really difficult.

# Okay, but Why is it that Difficult?
We all wrote those papers in high school. Perfectly prescribed formatting, with one introduction paragraph,
three middle paragraphs, and a conclusion. We're taught that because it's an easy writing style to make
coherent for a brief essay, but it's really not much good beyond that. It lacks sophisticated flow, is 
unsuited for expressing complex ideas, and of course, doesn't work very well if you're doing something
substantially longer. It's something teachers use to introduce you to the basic idea of how to structure
your thoughts for something legible and meaningful. Computer science is similar: you're taught basic
structures and patterns that are more legible, coherent, and effective than pure stream-of-consciousness.
But since each project takes maybe a few weeks, you don't really do anything sophisticated - you're writing
those 5-paragraph essays, when your job will be to crank out encyclopedias.

But it's not just like written language - it's much, much worse. Imagine, if you will, a world where not
only is it your job to crank out book after book, but that the history of written language is completely
different. In this scenario, written language is only 60 years old. Not only that, but every few years
a new revision of the language is put out, and whatever you wrote before is no longer compliant. Languages
don't translate easily, so you need to choose the right language to reach your entire desired audience.
Some languages are better suited toward certain ideas, and almost everyone specializes in 1-3 languages.
It's a haphazard imbroglio of rushing to find the best way to structure your words, what only works in
certain languages, and trying to keep up with the newest changes. 

Now, on top of all of that, you're writing it with a team of other people, all with their own linguistic
voice, different specialties, and ideas. You try to divide it up - agree on conventions, design the layout
of the book beforehand, divide up chapters - but as they say, no battle plan survives contact with the 
enemy.

# But it's your Job. You Should be Able to Do it.
There's truth to this, but computer science is an immense field. There are countless sub-areas, many of
which are probably too broad in and of themselves for any individual to have a thorough understanding. 
There's the mathematics, the philosophy, the design, data engineering, security, tech support, the
internet, robotics, and so much more. Code quality could probably nestle itself within the philosophy
of computer science, and it's still something that's hard to pin down. There are guidelines, things that
we all agree are good, but to a large extent judging code quality is a case of "I know it when I see it."

That said, there are gray areas. Sometimes something becomes completely illegible due to a programmer
using some "black magic" to get the job done, and do it efficiently. My favorite example is the 
[Fast Inverse Square Root Approximation](https://en.wikipedia.org/wiki/Fast_inverse_square_root), 
a bit of code used to power graphics in a lot of old games.
To be honest, I don't understand the mathematics behind it, but the code speaks for itself.

    float Q_rsqrt( float number )
    {
        long i;
        float x2, y;
        const float threehalfs = 1.5F;
        
        x2 = number * 0.5F;
        y  = number;
        i  = * ( long * ) &y;                       // evil floating point bit level hacking
        i  = 0x5f3759df - ( i >> 1 );               // what the fuck? 
        y  = * ( float * ) &i;
        y  = y * ( threehalfs - ( x2 * y * y ) );   // 1st iteration
    //	y  = y * ( threehalfs - ( x2 * y * y ) );   // 2nd iteration, this can be removed
        
        return y;
    }

This violates a **LOT** of the principles of clean code (swearing in comments is also always a bad sign). 
And yet, the author managed to abstract it away
deep enough that no one who uses the function will really need to know how it works (this is an important
principle of clean code), and it does its job more quickly and effectively than other algorithms of its
time. It's ugly, and it's beautiful. It's awful code, and it's great code. 

Most programmers have decent code quality. They have to. If you don't have a basic level of quality in
your code, you hit a point where you can't expand on it anymore because you don't know what it does. But
most programmers also drop their quality here and there, because management says *we need three weeks of
code done in three days and I don't care how*, or sometimes simply because it doesn't make sense to invest
that much effort in designing a basic piece of code.

# So What Does any of This Have to Do With Your Title?
Writing good code is an art. And like many arts, there are journeymen, experts, and masters. The
journeymen are common enough, but the experts and masters are rarities. People who write clean code as easily
as they think it, whose skills have progressed so far they've forgotten how to write bad code, whose
work toils unseen under the systems we experience every day and holds everything together.

It really is too bad that they are so rare.

Any shmuck with a computer and some determination can write some code and put it up online somewhere. And
there's a lot of shmucks with determination. 

Since it's such a difficult art, there are many people writing code that just isn't up to par. It's what
powers the internet, what powers our computers, and what drives our entire experience. And perhaps the
scariest part, we wouldn't be where we are without them. Behind every major website or application is at
least some bad code, and if there weren't people to write that code, nothing would work in the first
place.

# Where Do We Go From Here?
If the arts reached their greatest era in the renaissance, we're still doing cave paintings. Doing
guesswork and experimentation, finding the berries that make the best pigments, and theorizing what will
work based on a small sample size. The greatest masters of the art of clean code, most likely, have not
written their first program yet. One day, when languages have evolved, truths have been discovered,
and the likes of Donald Knuth, Linus Torvalds, and Jon Skeet are considered archaic example of what was
considered good code before we knew what we were doing, the premise of this post will no longer be true.

&nbsp;

----

*"When you do things right, people won't be sure that you have done anything at all."*
