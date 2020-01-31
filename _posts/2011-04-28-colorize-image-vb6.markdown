---
author: tanner_h
date: 2011-04-28 18:41:36+00:00
excerpt: '"Colorization" in image processing can refer to one of several things.  One
  form of "colorization" is taking any image - including full-color ones - and applying
  a uniform color for dramatic or artistic effect.  This is the type of colorization
  filter provided by software like Photoshop and GIMP, and it''s also the effect this
  project implements.'
layout: post
slug: colorize-image-vb6
title: How to Colorize an Image (in VB6)
redirect_from:
 - /3552/colorize-image-vb6
 - /3552/colorize-image-vb6/
---

"Colorization" in image processing can refer to one of several things.  Most commonly, to _colorize_ an image is to take an image without color (like a black and white photograph) and artificially apply color to it.  One example of this is the old [Three Stooges](http://en.wikipedia.org/wiki/Three_Stooges) movies which were originally shot in black-and-white, but [re-released several years ago in color](http://en.wikipedia.org/wiki/Film_colorization).  Colorization of an entire movie is expensive and time-consuming, and a lot of human intervention is required to make things look right.

Another form of "colorization" is taking any image - including full-color ones - and colorizing the image for dramatic or artistic effect.  This is the type of colorization filter provided by software like Photoshop and GIMP, and it's also the effect my source code provides.

![Enslaved poster - original](images/Enslaved-Odyssey-to-the-West-normal-600x375.jpg)

Here's the original image (a poster for Enslaved: Odyssey to the West).

![Enslaved poster - blue colorization](images/Enslaved-Odyssey-to-the-West-blue-original-saturation-600x375.jpg)

...and here's the same poster, colorized.

Colorization works by retaining certain data about each pixel's color (luminance and possibly saturation) while ignoring other data about color (hue).  In the demonstration above, each pixel in the second picture has the exact same saturation and luminance as the top picture, but all hue values have been replaced with blue.

Different programs implement colorization differently.  Most require you to specify hue and saturation values, with luminance being optional.  I really like the effect created when you keep the saturation values from the original image.  If you force saturation values to an arbitrary number - like Photoshop or GIMP - the colorized image looks either drab or blown-out.

![Enslaved poster - orange, original saturation](images/Enslaved-Odyssey-to-the-West-orange-original-saturation-600x375.jpg)

Here's another colorization - this time to orange.  Saturation values are unchanged.

![Enslaved poster - orange, 50 percent saturation](images/Enslaved-Odyssey-to-the-West-orange-saturation-50-600x375.jpg)

Here's the same image, but with saturation forced to 50 percent (Photoshop style).  See how the characters and background blur together?  The nice contrast between the background buildings and the character on the right is no longer present.

![Enslaved poster - orange, 100 percent saturation](images/Enslaved-Odyssey-to-the-West-orange-saturation-100-600x375.jpg)

...and here's the image again, but with saturation forced to 100 percent.  This looks terrible, IMO.

I think the top image in this set offers the most interesting colorization... but since I wrote this code, I could be biased... :)

Full sample code is provided, and - like all code on this site - it's fast enough to run in real-time.  

![Colorize program screenshot](images/colorize-program-screenshot-600x528.jpg)

*Here's a screenshot of the GUI attached to the sample code.*

**[Download a sample app and source code from GitHub.](https://github.com/tannerhelland/vb6-code/tree/master/Colorize-effect)**
