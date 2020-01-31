---
author: tanner_h
date: 2009-01-26 03:26:35+00:00
layout: post
slug: image-blending-transparency
title: Manual Image Blending/Transparency
redirect_from:
 - /490/image-blending-transparency
 - /490/image-blending-transparency/
---

Real-time transparency has become so commonplace in modern games and PC applications that it's almost taken for granted.  However, the specific formula that performs this now-ubiquitous effect is worth understanding.

Transparency is simply a weighted average between the color values of two pixels.  As an example, consider the following two colors:

**RGB(255, 0, 0)**

**RGB(0, 0, 255)**

At 50% transparency - or a pure blending between these two colors - we simply add the individual color amounts together and divide by two.  This gives us a new color -

**RGB(127, 0, 127)**

The sample app provides a slider for variable transparency, which uses a slightly more complicated formula.  (Each input color is weighted according to the desired level of transparency.)

![Squall and Rinoa meet a large flower (insert Garden joke of your choice :)](images/manual_transparency.jpg)

As you'd expect, your programming language probably provides a built-in function for blending images, which is likely much faster than manually blending each pixel.  However, if you need to blend values manually, this is how you do it.

**[Download the sample app and source code from GitHub](https://github.com/tannerhelland/vb6-code/tree/master/Transparency-2D)**
