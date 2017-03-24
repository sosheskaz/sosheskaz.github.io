---
layout: post
title: How to Secure Your Online Life
author: Eric Millerw
---

Have an online stalker who you're worried might hack your account? Have sensitive materials in your accounts or computer
that you don't want to be exposed to a threat? Just want to be safe in the modern day internet environment? Here you'll
find some simple guidelines to stay safe out there.

As time goes on, personal information security has gotten more and more important, and knowing what exactly to do and
how to do it is difficult. For that reason, I'm making a short post about how to lock down your online life.

# Important Terms
When talking about online security, there are some precise terms because of how new this field is. So I'll cover some of
these here.

* Encryption - Encryption is a process that scrambles data using a passcode. When data is properly encrypted with a secure password, it is unreadable by anyone.
* AES - The standard for "symmetric" encryption. This is what the NSA uses for top secret files, which should indicate its reliability.
* Multi-Factor Authentication - The process of using multiple ways to verify that someone is who they say they are. For example,  a password (something only you should know), and a code texted to your phone (something only you should have). By verifying someone's identity in multiple ways, you increase the barrier to entry of breaking into your phone.

# Step 1. Password Manager
![LastPass in action](/{{site.post_images_path}}/2017-01-17-LastPass.png)

Passwords in general have two main vulnerabilities:

1. They're usually made up of words, maybe with a number tacked on to the end. This becomes predictable, and makes easier to guess.
2. People often reuse the same password on multiple websites, so if an attacker gets one password, they get them all.

The best answer to these problems is a Password Manager. I recommend [LastPass](https://lastpass.com), because it's truly cross-platform and affordable. [1Password](https://1password.com) is also popular. iCloud Keychain is built in to macs, and has some nice features as well, but is **only** on MacOS and iOS. Here's what they do:

* Remember all of your passwords, securely encrypted in a "vault" with AES encryption.
* Lock that vault with one password - which means you only have to remember that one.
* Plug in to web browsers and other apps and fill in your passwords automatically or with a prompt.
* Generate new, secure passwords that have a mix of letters, numbers, and symbols, and can be relatively long. Here's an example: &B3BPBSNMKfus%9e*gy4. Good luck guessing that, hackers!

The result is that, as long as you guard your master password jealously, avoid reusing it where possible and use the generated passwords, your web life will be very secure.

However, password managers have one important downfall: if your master password gets out, you can lose everything. Which is why you may also want to use:

# Step 2. Two-Factor Authentication
<div class="col-md-12">
<img src="/{{site.post_images_path}}/2017-01-17-Authy.PNG" class="col-md-6">

2-factor authentication can send a unique code to a device you own, to prove that you are who you say you are, when you first log in to a service from a new device or haven't logged in for a long time.

Typically, this is a service you have to turn on in the web service you're looking at. Usually it works by sending you a text with a one-time code that you can use to log in, but there are other solutions.

I recommend <a href="https://www.authy.com">Authy</a> as your "one-stop-shop" for this, as it works with a lot of websites, won't fill up your text inbox, and works on iOS, Android, and Desktop. When setting up two-factor authentication on a website, look for "Google Authenticator". It'll give you a QR code - just scan it, and it's set up! Note that some sites only support text for authentication, and not Google Authenticator.

You can use this for LastPass, and now in order for someone to get into your account, it makes it *very* difficult to break into your account.

Note: Apple and Microsoft have their own ways for doing this for their accounts, that are in some ways more convenient and in some ways less so.
You should definitely use these, as these are likely some of your most important accounts.
</div>

# Step 3. Full Disk Encryption
<div class="col-md-12">
<img src="/{{site.post_images_path}}/2017-01-17-FileVault.png" class="col-md-8">

This is a rather drastic step, but it has been made feasible by advances in technology. This will slow down your computer, but if you have a Solid State Drive (SSD) it isn't particularly noticeable. The previous two steps can be considered sufficient for most people. This is turned on by default in Android and iOS.

The hard drive is where all your data is kept. Under normal circumstances, if someone steals this or your computer, they can read anything on it (that isn't encrypted). Hackers have a saying: "Physical access is total access". Of course, if there's nothing interesting/private on your computer (that's not encrypted already, like LastPass and Authy) this is a pointless exercise.

Windows does this with BitLocker, and MacOS does this with FileVault. Both are excellent solutions (although Apple has a better record of not programming "back doors" in their software - which has lost them fans among the NSA and FBI and gotten them praise from privacy advocates). If these aren't sufficient for you, you can do research and find your own solution.
</div>
# Conclusion
Congrats! With step 1 and 2, and proper diligence, your digital life is now locked down tight. If you followed step 3 as well, you're Fort Knox 🎉.