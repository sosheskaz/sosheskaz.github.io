---
layout: post
title: How Modern Video Works
author: Eric Miller
category: Technology
tags:
---

Video is one of the most important technologies on the internet today. We use it so much we don't
even really think about it anymore. We stream TV shows, watch cat videos, teleconference, and share
on social media. It's become common and mundane, but it took a lot of smart people working very
hard to get to this point. Motion film is a bit over 100 years old, and in that time it's gone from
a strange novelty to a series of multibillion-dollar industries that we interact with every day.

I'm going to go through, starting with the technology of the moving picture and moving through to
modern video encodings.

# The Moving Picture

At the core of video is a relatively simple technology, the moving picture. It sets the stage for
what video would become - a technology based on an illusion. The basic idea of the moving picture is
that when you display a series of still images in rapid succession, the human brain does a few
interesting things. First, it recognizes the series of stills. However, since they're changing so
fast, the brain assumes that it's seeing it wrong and that what's actually happening is real
movement with a high-speed strobe effect caused by lighting. The brain then does a few things before
passing on information it's seeing to the higher brain/consciousness. In an old school film
projector, there is a small time between still images (frames) where the screen is black. This
happens because the projector has to move the physical film to get the next frame. The brain
interprets this as a temporary loss of lighting, and assumes it's irrelevant data, so it ignores it,
rendering us humans incapable of seeing it. The other thing the brain does is it looks at the
discrepancies between frames. Again, it assumes that something's wrong and it changes the data
before passing it to the higher brain. It notices that there isn't smooth movement between the
frames, so it fills it in with whatever it thinks should be there. The result is that, by the time
the information about what the brain is seeing is passed to the higher brain, it goes from looking
like a series of still frames with darkness between them to smooth, fluid motion.

This is all possible because the human eye is a pretty flawed device. There's an
[XKCD comic](https://xkcd.com/1080/) that outlines some of the problems. However, our brains ignore
the flaws and junk data they get in order to turn everything we see from a bunch of nonsense into
a cohesive picture.

This set the stage for how we think about and approach the problem of video, so it's useful to have
an understanding of the basics.

# Still Images

Now we're going to skip past a few decades of film history to the digital age. Before we can talk
about video, we want to understand a few things about how images work.

## Red, Green, and Blue

The human eye can see just a small range of the spectrum of electromagnetic radiation, which we call
the visible spectrum. It accomplishes this by having some biological structures called "Cones". The
human eye has three types of cones (dogs have 2, red and blue, and butterflies have 5, which we
don't have words for). These cones are red, green, and blue. They specialize on detecting a specific
range of wavelengths, detecting the ones closer to what they specialize in much more strongly. For
example, blue and green cones both detect blue, but the blue cones light up way more because they're
more sensitive to that particular wavelength.

So how do we see orange? Like with film, our brains do some heavy editing before sending the
information to our higher brain. When the brain sees orange, it detects that we're sensing a small
amount of red and a small amount of green. By looking at the ratio of red and green signals coming
from the eyes, it can determine where in between those two wavelengths the light is, and tells our
brain the hue it thinks it's seeing.

These facts about the human eye are a boon for computer images, because it means that if we want to
show the color orange, we don't need to actually show orange - we just need to show red and green
in the right ratio in roughly the same place. Each pixel in a computer is, then, made up of three
series of lights - red, green, and blue. It brightens the lights to the right amplitude relative to
each other to fool our brains into thinking they're seeing the full visible spectrum.

That's right, your computer screen is only three colors. The fact that you see color when you look
at pictures on a screen is an optical illusion hard-coded into how human eyes and brains work.

There's a video (below) where a guy puts these colors into
a spreadsheet, with each cell being either red, green, or blue, and uses that to build a full-color
image into an excel spreadsheet that shows how this works pretty well.

<div class="embed-responsive embed-responsive-16by9">
<iframe width="560" height="315" src="https://www.youtube.com/embed/UBX2QQHlQ_I" frameborder="0" allowfullscreen class="embed-responsive-item"></iframe>
</div>

If you've done web development, you've seen hex codes (like #7D3C98, which equates to a dark
purple) which show a bit about how computers handle color under the hood. Red, green, and blue all
have a value ranging from 0 to 255. A hex code represents these three values, encoded in base 16
(hexadecimal) instead of our normal counting system of base 10. For example, 62 in base 10 would be
represented as 3E in base 16. (62 / 16 = 3 Remainder 14. In hexadecimal, 10=A, 11=B, ..., 14=E,
15=F). The hex codes are made up of three numbers, that are shoved together into one piece of data.
Each number is two hexadecimal digits long. So #7D3C98 is really "Red: 7D, Blue: 3C, Green: 98". Or,
in decimal, "Red: 125/255, Green 60/255, Blue: 152/255". These numbers tell the computer how much
power to put into each red, green, and blue light\*.

\* @Nerds, I know LCDs are more complicated than that, but that's an implementation detail and doesn't
really affect the point I'm trying to make.

A picture is then basically a grid of information telling it how much red, green, and blue we need
for each pixel.

## Intra-frame Compression

For still images, we'll usually compress them so that they don't take up so much space and can load
faster. Common examples are things like JPEG, PNG, and TIFF. There are two classes of compression,
lossy and lossless. Lossy changes the image and loses detail, but is much smaller. Lossless
compression is a perfect copy of the image, just takes up less space on disk. JPEG is lossy, PNG and
TIFF are lossless.

# On to Video!

As with everything in computers, everybody had a different standard, and thought theirs was better
than everyone else's, and was so much better that people would line up in droves to use it as the
one universal standard from now on. As with everything in computers, it didn't really go that way.

Anyway, videos have two components, audio and video. These components are independent, and
essentially work separately. For video and audio, there are things called "codecs". A codec is
basically an instruction manual for the computer on how to turn the raw data into pixels on the
screen or vibrations in the speakers. You can't watch or record video or audio that you don't have
a codec for in the same way that you can't understand or speak a language you've never learned.
There are tons of different codecs floating around, but the most popular ones right now are
probably H.264 for video and AAC for audio. Video file formats, like MP4, MKV, MOV, avi, and so on,
don't actually tell the computer how to store or interpret the data (they can do some neat things
with it, but it essentially boils down to using metadata). Instead, they tell the computer where and
how to put the video codec and the audio codec together to turn it back into a video.

## Inter-frame compression

Intra-frame compression can be pretty powerful, but also pretty limited. American movies play at
24 frames per second. If you're watching a 1080p video, this winds up being a **lot** of data. Time
for some quick math.

-   1080 vertical pixels x 1920 horizontal pixels = ~2.1 million pixels per frame.
-   ~2.1 million pixels x 3 bytes of color/pixel (RGB) = ~6.2 million bytes per frame
-   ~6.2 million bytes per frame x 24 frames/second = ~149 million bytes per second
-   ~149 million bytes per second * 8 bits/byte = ~1.2 billion bits per second = 1.2 Gbps

Given this, it should be impossible to stream a full HD movie from Netflix on most peoples'
internet. The natural response would be to use JPEG compression to cut down on the size. JPEG can
reasonably compress 10-20x smaller, which means the video could be taken down to 120Mbps or
60Mbps. That's still a lot, probably won't stream well (or at the very least will stress your
internet connection and computer). People wanted high-quality video, and it simply wasn't feasible
to do with just intra-frame compression.

So in comes inter-frame compression. The core idea is that, in most video, each frame is mostly
similar to the previous one. People's mouths move as they talk, they move their hands, and
occasionally they change position slightly (relative to the previous frame anyway). Instead of
sending the whole image every time, we just send what changed. When you see weird artifacts on
video where the screen looks wrong, but the parts that are changing (like mouths and hands) still
work, that's why - the moving parts are updating, but something's wrong with the "root frame" that
everything is being calculated relative to.

Tom Scott made a great 4-minute video about this that explains it better than I can.

<div class="embed-responsive embed-responsive-16by9">
<iframe width="560" height="315" src="https://www.youtube.com/embed/r6Rp-uo6HmI" frameborder="0" allowfullscreen class="embed-responsive-item"></iframe>
</div>

As an experiment, I converted 30 seconds of video as a sample to H.264 (the most popular video codec
currently), to see how H.264 compares to JPEG compression. Just like my example, it's 1080p, so all
the numbers translate. The file was 1319194 bytes large, or roughly 1.3MB. When converted to a
bitrate (1.3 MB x 8 bits/byte / 30 seconds), it comes out to just 352 kbps. That's about 170 times
smaller than the JPEG-compressed video, and it's definitely streamable over even a slow internet
connection.

One note: It seems like this video compresses pretty well (some don't) but it's still a reasonable
benchmark.

Inter-frame compression is the technology that makes online streaming feasible.

# H.265

I said before that H.264 is the most popular video codec. This is true. It's supported
out-of-the-box on just about every consumer product intended to display video, and it's the most
common codec to get data in. However, there's a new kid on the block. The next iteration of H.264 is
called H.265 or HEVC. Apple announced built-in support for it coming in iOS 11 at WWDC. H.265 has
the same quality as H.264, but takes up much less space. How much smaller? I ran the experiment
again and it came up with a size of 490219 bytes (490 KB). So it's about 2.5 times smaller.

That's pretty boring and mundane (especially compared to H.264 vs JPEG), but it's come at a time
when a 2.5x reduction in space is very helpful. But why? 1080p already streams just fine, so why
does getting those files smaller matter at all? (Granted, if you're on slow internet this is
probably already a godsend, but for the sake of argument)

4K and UHD media. Most places don't record video in 4K yet, because adoption is taking some time in
the market. 4K is twice the horizontal and vertical size of 1080p, which means it's 4 times bigger
in total. If your phone supports 4K video and you've ever used that, you know how much of a pain
that is. With the new codec, we can shave 60% off of not only the file size, but the broadband
connection required to stream it. So the primary burden of capturing 4K video is being alleviated,
and the burden of shelling out to internet providers in order to stream movies is lessened. You can
essentially make a jump in video quality (from 720p to 1080p, 1080p to 1440p, 1440p to 4K) without
needing to pay more for broadband. Alternatively, if you're a content creator, you can compress the
video less aggressively while keeping the same file size.

It's taking its time, but it's coming to market now, especially with Apple's support.
