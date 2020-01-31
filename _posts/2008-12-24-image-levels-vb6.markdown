---
author: tanner_h
date: 2008-12-24 22:57:23+00:00
excerpt: When this code was first written, it was (as far as I knew) the first non-GPL open-source implementation of a real-time image level adjustment.  There have since been many other implementations (including a much more powerful version in my own PhotoDemon photo editor), but I believe this first version still demonstrates a nice, simple, Photoshop-equivalent approach to the problem.
layout: post
slug: image-levels-vb6
title: Real-time Image Levels (input/output/midtone) 
redirect_from:
 - /341/image-levels-vb6
 - /341/image-levels-vb6/
---

When this code was first written, it was (as far as I knew) the first non-GPL open-source implementation of a real-time image level adjustment.  There have since been many other implementations (including a much more powerful version in my own [PhotoDemon photo editor](https://photodemon.org)), but I believe this simple version still demonstrates a nice, simple, Photoshop-equivalent approach to the problem.

Image levels provide better control over an image's luminance than strict brightness/contrast methods, but not quite as much control as a [well-built image curves dialog](336/image-curves-vb6/). Adjusting an image with input/output/midtone levels is primarily designed to brighten or darken an image without losing detail at either end of the luminance spectrum. I've included simple histogram drawing code (as the screenshot shows) so you can see the effect that adjusting levels has on an image's histogram. The code is well-commented and fast, and easily portable to any language of your choosing.

![The included histogram code is also a good reference.](images/image_levels-600x510.jpg)

The included histogram code is also a useful reference.

**[Download the sample app and source code from GitHub](https://github.com/tannerhelland/vb6-code/tree/master/Levels-effect)**

For a much more advanced version of this tool, including support for auto-leveling, you might check out [the source code of PhotoDemon's Adjustments > Levels tool](https://github.com/tannerhelland/PhotoDemon/blob/master/Forms/Adjustments_Levels.frm).  It exposes a number of advanced options (and faster performance) relative to the simple standlone sample implementation linked above.

[![PhotoDemon screenshot](images/PD_levels_screenshot.png)](images/PD_levels_screenshot.png)

*Screenshot from PhotoDemon's Adjustments > Levels tool*