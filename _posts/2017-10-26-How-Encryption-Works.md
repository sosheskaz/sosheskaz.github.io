---
layout: post
title: How Encryption Works
author: Eric Miller
category: Technology
tags:
---

These days, encryption is becoming more and more important to understand, politically and
personally. However, when it gets discussed in an open forum, it's usually discussed so abstractly
that the layperson doesn't really understand the specifics of what's going on. That's what I'm here
for. I'm going to talk about encryption in a way that anyone can understand, and explain how it
works and why.

# What is Encryption?

From [Wikipedia](https://en.wikipedia.org/wiki/Encryption): "_encryption is the process of
encoding a message or information in such a way that only authorized parties can access it_".
Essentially, this means we want our data to be a secret from anyone who tries to look at it. The
internet, and almost everything on it, _needs_ encryption to function. The process of turning
encrypted information back into useful information is called "decryption". Banks need to protect
information to protect identity theft. Companies need it to protect intellectual property. In fact,
_everything that has a login screen_ should have encryption (some sites haven't caught up yet) to
prevent bad actors from intercepting the message and stealing passwords.

As an example, one of the oldest, simplest, and least secure forms of encryption is the
[Caesar Cipher](https://en.wikipedia.org/wiki/Caesar_cipher). The idea is that you take a message
and shift all the letters. So for a Caesar Cipher of shift 1, A becomes B, B becomes C, Z becomes A,
and so on. The idea is that someone who sees the message can't read it without knowing the shift.

Important to understanding encryption is the idea of _keys_. A key is essentially a secret code that
tells you how the cipher works. In a Caesar Cipher, the _key_ is the shift. So if we have a shift
of 5, we know that to encrypt it we have to shift the letters forward 5, and to decrypt it we have
to shift them backward 5. A key can be used to lock or unlock your data as needed.

# Symmetric and Asymmetric

There are two kinds of encryption: symmetric and asymmetric. These words refer to how the keys work.
In symmetric encryption, you use the same key for encryption and decryption. It's the same on both
sides, so it's _symmetric_. This means that in asymmetric encryption, you need a different key for
encrypting and decrypting.

Both are important, for different reasons. The short of it is that symmetric keys are usually used
for storing data, while asymmetric keys are typically used for communication. To understand why, we
need to look a bit closer at how they actually work.

# Walkthrough

I'm going to be walking through an example using [OpenSSL](https://www.openssl.org), a widely-used,
free, and libre/open-source (meaning that the code behind it is in the public domain) encryption
tool. My examples will be designed to work in the macOS Terminal (/Applications/Utilities/Terminal),
the Linux terminal, and the Windows command prompt (cmd.exe).

If you're on a mac and want to follow along, you'll need to do two things. First, if you haven't
installed [homebrew](https://brew.sh), do so now. Next, run `brew install openssl`.

If you're on Windows, you'll need to download and install
[OpenSSL for Windows](https://slproweb.com/download/Win32OpenSSL-1_1_0f.exe). Then, press the
"Windows" key on your keyboard, type "cmd" and hit enter - it should open the command prompt.

## Terminal Crash Course

The terminal, or command prompt on Windows, is one of the oldest ways of using a computer
interactively. The idea is pretty simple - type a command, hit enter, and it executes a program and
writes the output on the screen below your command. Commands are generally made of two parts - the
command name and the arguments. The command name tells it what program to run like how when you open
an application, you need to tell it what application to run. Arguments give it information on _how_
it should run. For example, if you open Notepad, you might send it a file, and it will open that
file instead of making a new document.

Arguments on the command line are often more complex than that example though. Commands like these
are generally made to be able to run without human interaction, so arguments replace the user
interface. There are generally three types of arguments:

-   Flags: These are a simple way to toggle something on/off. for example, in Windows installers,
    running them with `/q` will run them in quiet mode, where they don't have any prompts. They
    usually start with `-` or `--` (or `/` on Windows).
-   Keyword Arguments: These are arguments whose significance is determined by a flag-like preceding
    command. The difference between a keyword argument and a flag can be hard to tell -
    syntactically they're very similar. It depends on how the developer implemented that argument -
    there is no standard differentiator.
-   Positional Arguments: These are arguments that aren't part of a keyword argument, and whose
    meaning is determined by their order. For example, in the UNIX copy command, the first argument
    is the file to copy, and the second is where to put it. For example, `cp myfile.txt ~/Documents`
    will copy the file "myfile.txt" to my Documents folder.

# Symmetric Encryption

Okay, we've got our terminal, we've got OpenSSL, let's make a secret file that we want to encrypt.
I'm putting it in `secret.txt`, and the secret text in the file is "the quick brown fox jumped over
the lazy dog".

Now, it's pretty easy to encrypt it. For our "key", all we need is a password. For my example, I'm
going to use `aovj[pr{14-0c9r/y423895]2.77u5rjf-sld`. This will be an example of how to encrypt a
file using symmetric encryption.

```sh
$ openssl enc -aes-256-cbc -k "aovj[pr{14-0c9r/y423895]2.77u5rjf-sld" -in secret.txt -out encrypted.txt
```

Whoa, that's a lot. Let's go step by step and break down exactly what happened, one command at a
time.

-   `enc` - this positional argument tells OpenSSL that we want to run in "encode/decode" mode.
-   `-aes-256-cbc` - this flag specifies the encryption algorithm we're going to use. AES-256 is an industry
    standard symmetric encryption method for sensitive documents. Even U.S. intelligence uses this
    algorithm to keep Top Secret documents safe.
-   `-k "aovj[pr{14-0c9r/y423895]2.77u5rjf-sld"` - this keyword argument tells OpenSSL the password to use as the key.
-   `-in secret.txt` - this keyword argument tells OpenSSL the file to create an encrypted version of.
-   `-out encrypted.txt` - this keyword argument tells OpenSSL where to save the encrypted file

Now let's look at what's in encrypted.txt.

```
    Salted__q°öµ`f!ÏÀQùW≤!	êƒÂ®[Vá K-|)&Ö⁄ ºíÌ^Õn6µá˚◊´0Î?z
```

Wow! That's certainly unreadable. You may note the word "Salted" in there. Salting is basically just
an additional low-level security measure - it doesn't matter to us right now. The word "Salted" is
in there so that, when we're decrypting, OpenSSL knows that salting is used.

Now, just for fun, let's try decrypting it with the wrong password.

```sh
$ openssl enc -aes-256-cbc -d -k "ThisIsNotThePassword" -in encrypted.txt -out decrypted.txt
bad decrypt
49993:error:06065064:digital envelope routines:EVP_DecryptFinal_ex:bad decrypt:/BuildRoot/Library/Caches/com.apple.xbs/Sources/OpenSSL098/OpenSSL098-64.50.6/src/crypto/evp/evp_enc.c:330:
```

As you can see, we don't know what's in the file. We are _completely
unable_ to figure out what's in the file without the password. In order to get in, we need to guess
the password, which could take trillions of trillions of trillions of attempts, if we're really
lucky. Breaking into AES, when it's protected with a good password, is conventionally thought of
as impossible because of the computing time it would take (on current machines, think hea).

Now, let's decrypt it.

```sh
$ openssl enc -aes-256-cbc -d -k "aovj[pr{14-0c9r/y423895]2.77u5rjf-sld" -in encrypted.txt -out decrypted.txt
```

This is mostly the same, except we're going the other way around. the `-d` flag in there tells OpenSSL
that we're using "decode" mode. Let's look at the contents of `decrypted.txt`.

```
    the quick brown fox jumped over the lazy dog
```

Exactly what we expected! So now you should have some understanding of how symmetric encryption
works, and why it's secure. On a side note, the exact algorithm and technology that AES uses is
publicly available in [RFC 3565](https://tools.ietf.org/html/rfc3565) (this has very advanced
computer engineering and mathematics - don't expect to understand it, just take away that the exact
implementation details are in the public domain).

## What it's Used For

-   Encrypting laptops and phones so if they get stolen or accessed by a bad actor, data can't
    be stolen.
-   WiFi passwords - used to encrypt the airwaves so any shmuck with an antenna can't skim data, and
    so to let someone join, you just give them the password.
-   Locking PDFs or other documents so they can only be accessed by people you give the password to.

## The Problems

-   If it's used for communication, everyone involved needs to share the secret password beforehand,
    if they want their communication to be secure.
-   Because in many cases, people are encouraged to share the password (like with WiFi), it's more
    likely for someone bad to get access.
-   Because the key can be shared around, you can't tell if someone you're communicating with is who
    they say they are.

# Asymmetric Encryption

Now we're on to asymmetric encryption, which is a bit more complicated. It's less efficient than
symmetric encryption in terms of CPU usage, but it has a few benefits. There are a few scenarios,
however, where symmetric encryption just doesn't cut it. Say you need encryption between two parties
(think you and your online bank) but we don't have a symmetric key agreed upon to encrypt our communications. We can't send it,
because then anyone snooping will have the key and be able to decrypt our data anyway. We need a way
to talk secretly without agreeing on anything beforehand.

Enter asymmetric encryption and RSA. RSA is just an implementation of asymmetric encryption, but
it's currently the best. It is to asymmetric encryption as AES is to symmetric encryption.

The first thing to note is that, unlike AES, our "key" isn't a password, it's actually a file. Or
rather, a pair of files. Asymmetric encryption has 2 "keys", a private, and a public. The private
key, unlike a symmetric encryption password, shouldn't be shared, and should be closely guarded.
The public key, on the other hand, can be given out freely to anyone. In fact, it should be.

The best way to understand how this works is to see it in action, so I'll show how to do it, and
comment as we go along.

```sh
$ openssl genrsa -out harry-private-key.pem 4096
Generating RSA private key, 4096 bit long modulus
...........+++
..............................................................................................................................................................+++
e is 65537 (0x10001)
```

-   `genrsa` - this tells OpenSSL that we want to create a new private RSA key.
-   `-out harry-private-key.pem` - this tells OpenSSL where to save the key.
-   `4096` - how many "bits" to use in the RSA key. More bits is more secure - 4096 is considered to
    be highly secure.

If we look at `harry-private-key.pem`, it looks like this:

```
-----BEGIN RSA PRIVATE KEY-----
MIIEowIBAAKCAQEAxoGOg5t2jyk8NapJlCSg0XBIudR32oMb2pGS5r74uLFDAdVA
ZLFuVPjY1Ba6ZlwMhakUxQb2obUqzGBJAgp5zfhxRU9bgv4w9RYdX5Cib2+0uaez
Myf16Gfb5oghvCNQC1laXWtDQe9TkUv+6a8/E47Gwbz1fVRFChnuJKN68ODhejdi
+I9rxqa8Za+BJhA6g82HTi/JrNIh8q1OlyD/mjrNYrztuH0RQNf52cm9HhhFFcqy
H5zys4glbLUDkzc8r50ElcABpnoG+T5vS2U54tta2F1Jbth6zlITrD8gEKbnGRQb
xxt/AdSaRvdfrWC5ARMzUKR14LTk8EjMNPJUZQIDAQABAoIBAQCBbPNop7JTgUU6
kD7NElywcY9ZakiC9jzw8z1eqWEtupW/2jTT8kPHr0BgeDksiBO6ChX6qKGhqaev
/Y9cf0wPmU7xK960t9tf0P1x07G1CpZA/jB+yC0zTJQ56MRmEHgeDjI2+rqtgMdx
0qTv5E0yCUNaCkPdZVZmUaXNybFc33yfu5v8wsRk2pqH1kZlx36DK5peICc8Cxil
obdBfWII5BzldCw/kB71+rZx6mlIVsvO3mjT7v4KiL/9z7FHbX04EXdYKYWMdfsf
WfXv5EtYi5dw1Ec8gJtkhBbZD+uZYAMc2tBQU/FVDno6Cxv6cnH+VYRTgnKA+SjL
XVUNvtPBAoGBAOvvDuI2KGuG5whdAojBz3UXHvDgUa9g9NJS0EmmAZAHjHKp1etz
XrdQIYd2kYKqnd2uRPyepZTlx6XOFCnOLC39nAWFBO6L/b6bhGIkVy8hF54qaWK5
zrBVnrUaz/bFr6xfEDsKOc0WP6L2z3Uq4QsaULmoEn/fqAm6SS1EPuspAoGBANdj
l2+cUX96eswXbtRAwBeqngr+Z+n7nhzZ+ZRfrcmR2nljKcmbkWnT/kcUgNt5vo7Q
3l4B8aOaWwGKF7tN4B8Krh5v4FdOa1GAJSomgJWmUdiel92MT8eWyoXZ038T5dcd
ACsaxdB+LGbN8v2Qa2cbFsQiPrJLzBsVwO1q0wLdAoGACM8pQBsDkVg9IhvO72pF
I7sURawqgKDfI0dCTa2sG0Oc498hhKQPIksUpWkw768NK+zI2KHXzuJxfOhf6luv
XJw+iho4X+vMMqS94ag3tSPILPiqbKxBYmYgAeUZZL5m28nE4l90Xwr4n04V2usZ
8f8uinATGMEyFgLlnpIQw1kCgYBPg6KqP2kOyKaApb3yeZzwn7oMkPLHvG4YdJfg
oJnFqiSfX25T0SyThwF+OCGB5KXmj1EoH0uXfCpQnSw5p3wvuX+iGOcXFAomYkpW
DzS1Clt4vsONtHjXU+GcHFgpt6zIBxrCzvVsDMhTg4BK/3/G5oc3DPVcWQMWlKdO
fns7uQKBgGpjJzK23Nak70HjJz/xtdCYqnglRChoJ+/KGl6CHxi8M4k7l5JxjUIn
MuLFSf/dnV6AI8ELYLaMaD14fCPkt3EzIW9cIFmVlhYaDJrCYNgebzdPqjrN7KAu
pmYplN3YpsM34VLMv1e0ZkldqwQMbsNiiL7ah+PTYCpmYQXdMvHP
-----END RSA PRIVATE KEY-----
```

Now we'll create the public key that goes with the private key we just made. **NOTE:** the public
key can be created from the private key, but the private key cannot be reproduced from the public
key. This is critical.

```sh
$ openssl rsa -in harry-private-key.pem -outform PEM -pubout -out harry-public-key.pem
writing RSA key
```

-   `rsa` - tells OpenSSL we're doing something with RSA.
-   `-in harry-private-key.pem` - we're using the private key we just made as the base.
-   `-outform PEM` - there are a few formats that public keys can take, pem is just a way the key
is formatted.
-   `-pubout` - tells OpenSSL we want to create a public key.
-   `-out harry-public-key.pem` - tells OpenSSL where to save the public key.

`harry-public-key.pem` will look something like this:

```
-----BEGIN PUBLIC KEY-----
MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAxoGOg5t2jyk8NapJlCSg
0XBIudR32oMb2pGS5r74uLFDAdVAZLFuVPjY1Ba6ZlwMhakUxQb2obUqzGBJAgp5
zfhxRU9bgv4w9RYdX5Cib2+0uaezMyf16Gfb5oghvCNQC1laXWtDQe9TkUv+6a8/
E47Gwbz1fVRFChnuJKN68ODhejdi+I9rxqa8Za+BJhA6g82HTi/JrNIh8q1OlyD/
mjrNYrztuH0RQNf52cm9HhhFFcqyH5zys4glbLUDkzc8r50ElcABpnoG+T5vS2U5
4tta2F1Jbth6zlITrD8gEKbnGRQbxxt/AdSaRvdfrWC5ARMzUKR14LTk8EjMNPJU
ZQIDAQAB
-----END PUBLIC KEY-----
```

Now, these keys work pretty differently. The public key is used to encrypt, while the private key
is used to decrypt. You don't encrypt with the private key or decrypt with the public key - you'll
see why as we go on. So let's say you're Sally, and you want to send Harry a secret message about a
certain brown fox.

```sh
$ openssl rsautl -encrypt -pubin -inkey harry-public-key.pem -in secret.txt -out dearharry.txt
```

-   `rsautl` - RSA Utility
-   `-encrypt` - we're encrypting using a public key.
-   `-pubin` - tells OpenSSL we're inputting a public key.
-   `-inkey harry-public-key.pem` - path to the public key we're using.
-   `-in secret.txt` - file to encrypt.
-   `-out dearharry.txt` - where to save the encrypted file.

Let's look at `dearharry.txt`

```
õÒIˆc
nËÁú∞ò¥7Ñ¯'ΩkÈQ¥òù"âˆ˘≠r/I÷›wE]“Ï’/í·2ƒã´À1U>¥G‡áÈíªát‡∆¥‡'Ñ3&∂ÙÊ3§(ê≤
üƒlùDHWáMê7Odn-ù_©q2ˆwÆædà4êØ¶œ4BŒAˇ)
≠},ç∏ìY$‡òé˙ﬂ)hGóUÖS›z˘cãC¨—ÁRö.Ó+§Ω€u˝	»›NΩ+x…›©tÓöﬂ´ﬂXhë:ﬁ>ìáCÀ¯ä>»7W"GŒ-W¢Â:Å£<^YÌƒ7¢I9ç+VMê”7ZÂr˝¡¶û,Ä“ÈY, ÏE~
```

That's a big mess of garbage! Because of the nature of private/public keys, even though Sally encrypted
this with the public key, she is unable to decrypt this file. Because we encrypted it with Harry's
public key, only his private key can decrypt it. There is no way to recover the message without it.

```sh
$ openssl rsautl -decrypt -inkey harry-private-key.pem -in dearharry.txt
the quick brown fox jumped over the lazy dog
```

It worked! This means Sally can send Harry a secret message that no one will be able to see, without
them ever needing to share a secret password. Like AES, this is considered more or less impossible
to crack.

## What it's Used For

-   When you connect to a secure website, it uses this to figure out how to communicate privately,
without ever agreeing on a shared secret in the open.
-   Secure communications use this to get messages
from point A to point B without being intercepted or tampered with.

## The Problems

-   It's much slower than symmetric encryption. This is gotten around by using asymmetric encryption
to privately negotiate a symmetric key to use.
-   It's really only useful for sending messages, not for storing secrets.

# Opening up Encryption

My purpose in writing this was ultimately to try to explain why opening up encryption so that, as an
example, allowing a law enforcement officer with a warrant to tap into encrypted communication is simply
not feasible. Let's contrast keeping something safe with encryption versus keeping it safe with a
lock. People like to make this comparison, but it's not really apt. Locks live in the world of
physics, and while the lock itself may be secure, it's still vulnerable to physics - you can get
through it in any number of ways. Obviously, you could steal the key, but it's not easy and risks
identifying an attacker. You could pick the lock, you could blow it off with explosives, or cut
through the locking mechanism.

Another important thing to note is that stealing a physical key makes
it likely for the perpetrator to be noticed by the owner, picking a lock is conspicuous and
suspicious, and of course explosives or power tools will draw eyes. Cyberattackers don't have to
deal with this so much. Attacks can be conspicuous, or they can be covert - but most cyberattackers
can attack very, _very_ quietly if they want to (at least compared to explosives 😉). Basically,
if you're going to compare it to something physical, imagine that every theif could turn invisible.

Encryption doesn't work through physics, or through trust - it works through mathematics. It's not
vulnerable to physics or workarounds. If you want a physical metaphor, it'd be like, instead of
having a lock on your filing cabinet, having a wand that can turn it into an unbreakable rock. No
one else can change it back from a rock. No one can even tell it used to be a filing cabinet.
Thousands of invisible thieves can all gather around and try to figure it out for weeks or even
years on end, and they won't be able to open the metaphorical rock.

That felt like a silly metaphor, but here's the thing - there's no true physical analogue of
encryption. I'll make one more attempt. It's like tapping the phone conversation of the only two
people in the world who know a secret language. Doesn't matter how long you watch it, you won't
figure out what they're talking about.

Putting a back door in encryption, a way to "tap" digital encrypted communications, would be an
insane logistical nightmare to begin with. Why?

First off, making it illegal would be incredibly
ineffective. As I mentioned, powerful encryption is open-source. This means that, even if there's
nowhere you can download the openssl executable, you could make it yourself. Going back to the magic
rock metaphor, this is like if everyone had the ability to create magic rock wands at will. Even if
they wiped every trace of it from the main internet (insanely difficult), it would be all over the
place on the dark net (a hyper-secure part of the internet famously used for online drugs/weapons
vending, exchange of illegal services, and anonymous escrow bank accounts). It would be about as
difficult as banning profanity in a society where everyone wore masks 100% of the time.

Second, every bank, company, and blog would need to upend their security infrastructure. This would
take years to roll out (at best) and cost billions of dollars (at best).

Third, it puts all security at a single point of failure. A single mistake by a government employee
could ruin everything. As I mentioned, the weakness that encryption and locks both share is that
someone could steal the key. But it's even more dangerous because, since an encryption key is data,
it can be copied without signs of tampering. If it was stolen, it's likely no one would know. Even
if they did, it can be shared among friends, then friends of friends, then posted on the internet
somewhere. Trust in private communication is ~~eroded~~ annhilated. The government has to release
a new key and every company and individual in the country has to switch over - bringing us back to
point 2. No one trusts that their bank communication is confidential. Or their WiFi. Or their
Facebook login. There is no privacy on the internet. There are no secrets. Any time you type in a
password, you may as well be painting it on the side of a bus. The internet dies. The industry
tanks. We enter a second great depression, and technology regresses decades. The criminals,
terrorists, and hackers all laugh, because they never stopped using true encryption, because _why
would they._

And that's why encryption is important.
