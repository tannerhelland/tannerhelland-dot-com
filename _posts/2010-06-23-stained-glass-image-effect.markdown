---
author: tanner_h
date: 2010-06-23 00:26:42+00:00
excerpt: I wanted to title this article "a novel method for matrix randomization using
  polygons and custom differential post-processing blending"... but that was a bit
  long, even for me...
layout: post
slug: stained-glass-image-effect
title: Rendering images from random lines (and shapes)
redirect_from:
 - /2306/stained-glass-image-effect
---

I wanted to title this article "_a novel method for matrix randomization using polygons and custom differential post-processing blending_"... but that was a bit long, even for me.

Why such a complex title?

It all started with a strange idea I had today.  I was thinking of common ways to randomize image data (don't ask why), and it struck me that the most common randomization method - varying RGB data of single pixels - is not the most interesting way to go about it.   Why not use lines, triangles, or other polygons to randomize an image?   How would that look?

To test my theory, I wrote a quick program that selects two random pixels in an image, averages their colors, then draws a line of that averaged color between the two points.  When repeated over and over again, such an algorithm leads to some interesting effects...

![](images/GoW3_original1.jpg)

For example, I started with this God of War 3 image...

![](images/GoW3_lines_30.jpg)

...and produced this new image (100,000 iterations of lines with max length 42).

![](images/GoW3_lines_60.jpg)

Here's the same image, but with lines of max length 85.

Kinda cool, right?  I'm not sure what to call this effect... although it looks "furry" to me.  Should we invent a new word - _furrification_?

Once I had lines working, my next curiosity involved polygons.  Here's the same picture, but with triangle randomization:

![](images/GoW3_triangles_30.jpg)

Same parameters as the first line-based randomization above (100,000 iterations, 42 max length).

![](images/GoW3_triangles_60.jpg)

Same parameters as the second line-based image above (100,000 iterations, max length 85).

This is also a cool effect, especially when you watch it in action.  (The program refreshes the screen every 100 iterations.)

While I didn't go to the trouble of implementing additional polygons, the code is primed and ready for it.  In fact, it would be trivial to draw polygons of any segment count.

Once I had my newly randomized images, I decided to pop into GIMP and do a bit of post-processing.  It was then that I realized this could be used to create something like a stained glass effect:

![](images/GoW3-stained-glass-30.jpg)

It's trivial to create an image like this - simply open up your base image, then add a triangle randomized copy over the top as a new layer.  Set the layer mode to "difference" and bam: stained glass!

![](images/GoW3-stained-glass-60.jpg)

*Same effect, but with a larger triangle size.*

Other blending modes provide interesting effects - for example, multiply:

![](images/GoW3-multiply-30.jpg)

*Same two images as the first stained glass example - just the blending mode has changed.*

Anyway, I thought this was an interesting exploration in using randomized image copies as overlays.

**[Download the sample application and source code from GitHub](https://github.com/tannerhelland/vb6-code/tree/master/Randomize-effects)**