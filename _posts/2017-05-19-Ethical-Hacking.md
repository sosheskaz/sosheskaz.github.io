---
layout: post
title: What is Ethical Hacking? And Contemporary Cybersecurity Ethics
author: Eric Miller
category: Security
tags: 
---
<img class="col-md-7 pull-right" src="/files/images/posts/2017-05-19/wannacry.png" />

Hackers. They're becoming increasingly important and relevant. From government agencies, to international
hackers and political controversies, to someone stealing your credit card. It's becoming bigger and bigger,
and question of how to deal with them is becoming increasingly important.

For this, I'm going to use a definition of hacking that is a bit more expansive than most. Hacking, as far
as I'm concerned, is deliberately getting unauthorized access to a computer system - whether that is 
reading data, running a program, or changing something. It's a wide definition because the question of 
cybersecurity considers these various methods to be of similar importance. It doesn't matter how someone 
got access to your system - it's a cybersecurity professional's job to prevent it.

Hackers operate outside of ethics and the law. Like other kinds of criminals, their expertise varies
wildly. Some are experts who, while they have the knowledge and skill to operate legally (and very 
profitably), choose instead to take advantage of others. Some are just kids who got their hands on a 
powerful piece of equipment or software and think they're cool. And everywhere in between.

Ethical hackers are people with the skills of sophisticated hackers, who operate legally, in order to 
help people and companies better protect themselves (for a price, of course). Typically, this means 
companies will contract them to try to break into their systems, and write up a report of what they were
able to find. This can take lots of forms, but I'll list a few of them.

* The [OWASP Top 10](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project) is a list of common
and dangerous security flaws in web apps. Ethical hackers will almost always check for these.
* The Phone Call. It's been said that the single most powerful hacker's tool is a phone. It's in peoples'
nature to be helpful, and to not want to make waves. This is called 
[social engineering](https://en.wikipedia.org/wiki/Social_engineering_(security)). The idea is that you
talk people into giving you the information or access you want - it works far more often than you'd think.
* Phishing. Basically, you pretend to be another website in order to get people to give you their usernames
and passwords. This is one of the most common tests they'll do. Some people scoff at this test - their 
employees can't be gullible enough to fall for that! They're almost always wrong. Phishing is dangerously
effective, and very easy to fall for. Recently, there was a phishing scam for 
[Google Docs](https://www.wired.com/2017/05/dont-open-google-doc-unless-youre-positive-legit/) that got a
LOT of people.
* Software vulnerabilities. There are lots of ways for software to make a simple mistake that lets an
attacker get at a lot of things. There are tons of these. Virtually all software has them, and they
haven't been discovered yet - which is kind of terrifying. That's why operating systems and apps have 
"security updates" all the time. They're just finding the bugs that would let an attacker do something
they shouldn't be able to. And there are still countless out there.

Again, these are just a few.

# Cybersecurity Ethics
But that was just a background in some cybersecurity information. Not all of us in IT are cybersecurity
experts, but it's possible for anyone to discover a security flaw. It could be as simple as using some 
software and realizing that there's something you can do that you shouldn't be able to. You've just 
found one of those formerly mentioned software security bugs.

Example time! I know someone who, in the earlier days of Amazon.com, discovered a security bug in 
Amazon's store. He found out that, through doing something a bit weird, he could add an item to his cart,
but have it be added at a much lower price. Specifically, he noticed he could put a $1000 TV in his cart
for the price of $3. Naturally, he called Amazon's customer service to inform them of this bug as soon as
possible. They told him he was mistaken, and that was impossible. They went back and forth. Eventually,
he decided to prove it. He added 3 of the TVs to his cart, for a grand total of $9 + shipping, placed the
order, sent the screenshot, and asked them if they were ***really*** sure that it was impossible. Their
tune changed very quickly, and they thanked him for finding the bug and telling them. As a reward, they
let him keep one of the TVs.

That's a great example of ethical and good behavior, on both sides.

But it's also scary. One person found a bug in Amazon when he was just trying to buy a TV. Anyone can
find a bug like that. And not all of them do the right thing. 

If you're actively looking for those bugs, it's illegal, but if you just happen to find one, it's not.

----

Those in IT have a certain code of conduct when it comes to finding these bugs. Companies do as well. Some
people follow these, some stretch them or don't follow them at all. Some companies behave well, and some
try to sue the people trying to help them.

Here's what *should* happen.

1. Person is using software, finds a bug.
2. Person contacts the vendor, and lets them know what happened, why, and gives all the information they
have.
3. Person informs the company that they will publicly disclose the bug in 30 days.
4. Company thanks person, and gives them a reward.
5. Company patches bug in a few days and rolls out change.
6. Person and/or company announce bug to the world.

Now, at first, this seems a bit confusing. Why would you publicly release it? Why the 30 day delay? Doesn't
that hurt the security overall? What about people who don't update?

This is the gold standard not because it's perfect, but because it's the best system we've found. It does
have issues, especially for those who don't update regularly. But here's why this system is what it is:

The person notifies the vendor what happened so they can fix it, protecting their users. Even innocuous
websites often have sensitive data. If you just have someone's email address and password, you can try 
that login for a plethora of websites. If they reuse passwords, you've got a lot of their accounts. You
may even be able to reset their passwords for other websites. That's why it's so important.

The person gives the company 30 days to fix it before they publish. 30 days is considered enough time to
write a software patch and deploy it, especially if the issue is treated with the due urgency. The threat
of publishing the bug means the company is *forced* to fix it; to act in their users' best interest.

The company thanks the person because they provided a valuable service. Security professionals are good,
but they do have blind spots. And if someone less benevolent had found the bug, it could have cost the 
company thousands of dollars in lost customers and bad PR alone. When someone has provided that kind of
vital service, without solicitation, at the very least a thank-you is in order in my opinion.

Finally, the bug is published. This is so that users of the software know that the previous version was
vulnerable, and that they should upgrade. Security professionals can also look up this information when
helping a client patch up their system. It's not a perfect outcome, but it's the best we currently have.
Fortunately, with auto-updating software catching on, the "legacy" problem is becoming less and less
relevant.

&nbsp;

Google is one of the best companies when it comes to this. They're currently offering $100,000 for anyone
who finds a security bug in ChromeOS.

----

# WannaCry
But recent events have concerned me. This protocol is considered the gold standard in how to treat this
situation because it's considered to get the best possible outcome for most people. It helps us all be
secure, and protects those who operate legally from hackers and bad actors.

Specifically, I was concerned about the recent ransomware, called 
[WannaCry](https://www.wired.com/2017/05/ransomware-meltdown-experts-warned/), that hit many 
organizations,
including Britain's National Health Service (NHS). Ransomware is software that locks up your data or 
another function of a computer until you fork over a ransom to the people who wrote it.

Why am I concerned? Well, it gets to the details. This was a vulnerability in Microsoft's Windows, that
was found by the NSA at some previous time. When the NSA was hacked and many of their tools and much of
their knowledge was leaked to the public, this was picked up by some hackers and used to create the tool.
Fortunately, before the hackers got to it, Microsoft managed to release a patch. Unfortunately, many
people don't update their computers as often as they should. This included the NHS.

So whose fault was this attack? Obviously, the most fault lies, as always, with the hackers who wrote
the WannaCry software. I'd also say the NHS deserves a share of the blame, because they failed to
perform their due diligence. It is their responsibility to protect their own data, and had they updated
their systems. They failed to protect their patients - people who trust them with their lives - because
they didn't keep up with security. They are far from blameless.

I actually blame the NSA relatively little for the damage done to the NHS. Microsoft created the patch,
and rolled it out in an acceptable timeframe. They were just holding on to the information up until that
point.

But they didn't follow the ethical best practices. They didn't even come close. What if, instead of the
WannaCry people discovering the bug in the NSA's data dump, they stumbled upon it themselves, in the
same way the NSA did? And what if the NHS actually had done their due diligence? Britain is considered 
a close ally of the United States - that would have meant that they had effectively been a bystander to
an attack on their ally. If the software also targeted Americans, they'd have been a bystander to an 
attack on their own citizens. That doesn't sit right with me.

Government security agencies are often claimed to be in the business of "doing bad things for good 
reasons". They kill, imprison, interrogate, and spy, supposedly in the interest of protecting the 
citizenry, and we as a society (regardless of individuals' views) have come to accept these facts as 
part of our civil contract. These are actions that would be illegal for citizens to perform, but as a 
government they are given special rights.

Regardless of your views on the ethics of those particular issues, many people would say that the actions
and inactions that these agencies take in the cybersecurity realm fall into the same class of actions -
bad for civilians, but acceptable for governments.

But I'm not sure they do. When they discover a vulnerability, they use it for their own ends. To them,
a security vulnerability is a weapon against their enemies. But when they keep it to themselves, they're
not just leaving their enemies vulnerable, they're leaving their allies, their citizens, and everyone 
else in the world vulnerable.

In my opinion, the government has a fiduciary duty to its citizens. When they hoard these vulnerabilities,
keep these secrets, at best they're gaining tools against the country's enemies, but they're also
knowingly standing by while their citizens, their company, and even other parts of the government are
vulnerable.

Are these tools against enemies really so valuable that they're worth endangering the people the
government is supposed to serve?
