---
layout: post
title: On the AES Encryption Algorithm
author: Eric Miller
category: Security
---

I wrote this paper for my Information Security class. Original publish date: 20 December 2016

The Advanced Encryption Standard, or AES, is a symmetric algorithm released by the United States National Instritute of Standards and Technology (NIST). It is technically specified in FIPS-197. It is another name for the Rijndael algorithm, though they are distinct; the Rijndael is its own algorithm, but it was selected by the NIST for the AES standard. It can use multiple lengths of key, including 128- 192- and 256-bit keys. It encrypts data in 128-bit blocks. The 128-bit block size allows for easy integration with most file systems (which tend to use block sizes of 512 bits and larger) much easier and more efficient.

AES was developed by the United States government for the purpose of protecting sensitive government documents, but the mathematical concepts and definitions were made available for private sector implementations. Aside from being used for the purpose of protecting federal classified information, it’s become, to a large extent, a global standard for symmetric encryption. In the public sector, AES is approved by the United States (notably the National Security Agency, also known as the NSA) for classified documents up to Top Secret classification.

The development of AES, and the ultimate selection of the Rijndael algorithm, while done by the NIST, was a largely open process. It was open to public comment and scrutiny through every step of the process. The transparency and depth of this process, in addition to its wholehearted adoption by the US government itself, established a high level of confidence in the standard. This was, to a large extent, what fed its popularity and growth in the private sector. 

Being a symmetric key, is frequently used for local protection of data, and protection of data that needs to be accessible using a shared secret. This makes it a popular technology for local disk encryption, such as encrypted documents and even full disk encryption. It’s also often used for home wi-fi routers, to make new connections easy. Despite that, perhaps the most important and ubiquitous use of AES is for fast, secure transmission, such as over TLS (though an asymmetric algorithm is used to share the key). 

As with any cryptographic algorithm or service, it’s important to analyze potential vulnerabilities and ultimately, the resources necessary to bypass it. From a mathematical standpoint, AES has proven to be a robust standard. Of course, the nature of software and computer science are fundamentally different. Over the years, various exploits and vulnerabilities have been found, but none that seriously called into question or impacted the overall security of the standard. While the mathematics have shown to be sound (although there may be mathematical vulnerabilities, there is no known way to “break” the algorithm), implementations and even more, users, can be vulnerable. Ignoring the dangers of social engineering, flaws in the implementation of the open AES standard could be vulnerable. Given that, at some point in the implementation, all of the data can be siphoned, the algorithm can be trusted only as much as the author. This is best indicated by the story of LavaBit, an encryption service that was federally mandated to install an exploit in their service, along with a gag order.



Sources:
[http://csrc.nist.gov/publications/fips/fips197/fips-197.pdf](https://www.schneier.com/blog/archives/2012/03/can_the_nsa_bre.html)

[http://csrc.nist.gov/archive/aes/index2.html](https://www.schneier.com/blog/archives/2012/03/can_the_nsa_bre.html)

[http://www.jscape.com/blog/aes-encryption](https://www.schneier.com/blog/archives/2012/03/can_the_nsa_bre.html)

[https://www.schneier.com/blog/archives/2012/03/can_the_nsa_bre.html](https://www.schneier.com/blog/archives/2012/03/can_the_nsa_bre.html)


