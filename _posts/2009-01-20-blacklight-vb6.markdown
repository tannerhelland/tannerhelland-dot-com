---
author: tanner_h
date: 2009-01-20 06:25:25+00:00
excerpt: Here's an example of a simulated blacklight effect that looks great on any image with people in it.
layout: post
slug: blacklight-vb6
title: Real-time Blacklight Effect
redirect_from:
 - /381/blacklight-vb6
---

Here's an example of a simulated blacklight effect that looks great on any image with people in it.

![Squall (from Final Fantasy VIII) before and after his blacklight transformation](images/blacklight.jpg)

*Squall (from Final Fantasy VIII) before and after his blacklight transformation*

The formula is simple - assuming you have the R, G, and B values of a particular pixel, the blacklight transformation can be applied like this:

**1) Calculate a luminance value for the pixel**

There is no set way to do this; personally, I prefer a proper human-eye accurate conversion using the formula:

    L = (222 * R + 707 * G + 71 * B) \ 1000

This places proper emphasis on red, green, and blue according to standard cone density in the human eye.  However, a faster (and look-up table friendly) method could be:

    L = (R + G + B) \ 3

For die-hard color perfectionists, luminance could also be calculated by an RGB -> HSL color space conversion, but the scope of that transformation is beyond this article.

**2) Perform the blacklight function**

My blacklight formula uses a "weight" to determine how bright to make the blacklight.  This is a number between 1 and 7, with an optimal value of 2.

Assuming that this weight value is placed in a variable called "fxWeight", the blacklight function is performed by:

    R = Abs(R - L) * fxWeight
    G = Abs(G - L) * fxWeight
    B = Abs(B - L) * fxWeight

...where `Abs()` is an absolute value function.  Basically, the blacklight formula calculates the distance between each color value and the gray value, then multiplies that by the "weight" of the blacklight.

**3) Force all R, G, B values below 256**

As you can see from the code above, if the blacklight weight is high, it is possible for the transformation to set pixels beyond proper unsigned byte range.  So to be safe, ensure that all R, G, B values are below 256.

**[Download the sample app and source code from GitHub](https://github.com/tannerhelland/vb6-code/tree/master/Blacklight-effect)**
