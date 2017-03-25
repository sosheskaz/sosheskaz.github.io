---
layout: post
title: 3 Things I Like About Swift
author: Eric Miller
topic: Programming
category: Apple
tags: swift programming
---


<div class="col-md-9">

Within the past several months, I've been working a lot in Swift 3 and XCode 8. The language was a brand
new experience for me, and there was quite a learning curve. I've never worked with a language like it and
while, as always, programming skills carry over, the syntax of Swift proved tricky. However, after this time,
I've either gained an appreciation for some of the more novel features in Swift, or else I've gained
stockholm syndrome. Determining which is left as an exercise to the reader.

</div>
<img src="https://developer.apple.com/swift/images/swift-og.png" class="img-rounded col-md-3" 
style="padding-bottom: 20px;" />

# 1. Nil! Nada! Nothing!
That's right, "nil". That's what null is called. Yes, it's weird that they've eschewed traditional
labeling in favor of this. The logic kind of makes sense, but I won't go into it - I'm not actually here
to talk about nil, but about *how it's handled* in Swift.

In C#, there's a concept called **Nullable.** This makes primatives, like floating-point numbers and 
integers, which one would not normally be able to assign a value of null, to be assigned null. 
This is often quite useful when you want primatives to behave like normal objects. Swift implements a
similar system, but instead it works for any object.

As an example, say you have a "Point" object, stored in the variable point.

    var point: Point = Point(1, 3)
    
The variable point can never be nil. If one tries the following code: `point = nil` it will raise a compiler
error. However, if you wanted it to be able to be nil, all you have to do is add a '?' to Point, so that
the type is now "nillable".

    var point: Point? = Point(1, 3)
    point = nil

This seems novel at first, but in conjunction with other features (one of which is coming up next) it really
simplifies programming. When writing a function, if one wants, they can mandate that no values passed in are
nil, which can simplify edge cases and testing. Now, onto "nillable's" best friend:

# 2. Guard Statements
Guard statements were, for me, covered briefly in a class, but beyond that, not talked about much. A guard
statement is a statement at the beginning of a function where it's decided whether the function can basically
work. They're often used to check for null or for error conditions. Swift, however, has its own dedicated
keyword for this, logically called `guard`. The keyword alone is useful for keeping code readable, because
one can see the keyword, realize it's just checking for error conditions, and skip over it when understanding
how some code works.

But other than that, what benefits are there? For one, they force good practice; the compiler won't allow
you to forget to `return`, `break`, or execute some other control flow. They allow one to create variables
for future use, allowing one to seamlessly unwrap a nillable. Here's that in practice:

    func doThing(thisReallyShouldNotBeNil: Int?, shouldBeTrue: Bool) {
        guard let notNil = thisReallyShouldNotBeNil else {
            print("you put in nil you dummy!")
            return
        }
        guard shouldBeTrue == true else {
            print("This should never happen :P")
            return
        }
        
        // notNil is an Int now, not an Int?.
        
        print(notNil != nil) // you will get a compiler warning because this will never be possible. 
    }

Obviously this is simplified, but it becomes very powerful in keeping things from getting out of hand as 
they get more complicated.

# 3. String Templating
Y'all, this is the best templating I've ever seen. Even better than Ruby or C#. It's simply beautiful. Say
one wants to print out a person's information:

    print("Name: \(person.name)    Height: \(person.height)    Profession: \(person.profession)")
    
It's the simplest thing. Backslash, parenthesis. Fits the context of the language, is perfectly clear,
and is one of the least verbose methods out there in any language. Simple beauty. It's the small things in
life.

# The Bad
Swift is an innovative, different, and unique language, and it has its share of bad. Most of it boils down to

## XCode
Swift is hard to build without XCode. Really hard. Even JetBrains' AppCode relies on opening XCode for 
certain operations. One of the main reasons for this boils down to the flat filemap. In most programming
languages, if you put something in a folder, that means it's in that folder in the operating system.
This makes traversing and interacting with your project from the command line natural. Instead, there's an
XML file that keeps track of the folder and subfolder in every file. If you want to look at the project as
intended, you need XCode. While this maps well to Apple's (and arguable BSD's) centralized philosophy, it's
an annoyance to developers.

XCode is buggy and crash-prone; lots of times features simply stop working and XCode needs to be restarted.
It reminds me of my early days with Eclipse over 5 years ago, and even then I believe Eclipse was more 
reliable.

Beyond that, it just has poor design in many ways. Keyboard shortcuts aren't shown in menus, the toolbar is
at times incomplete, and "generate" code functionality is painfully absent, to name a few.

# Closing
So yes, I like Swift quite a bit. It winds up being a different language, but some of the language features
have shown to not only be nice to use, but to be very forward-thinking in terms of keeping large codebases 
sustainable. It also keeps up with more modern functionality, syntax, and paradigms quite well, while also
putting its own spin on it.

Finally, it's important to consider that Swift is designed very specifically around building UI apps. In
this way it's often more specific, or at least has a different focus, than many other languages. When 
learning it, it's important to keep an open mind, and to give Swift's way of doing things a shot. I'm glad
I did.
