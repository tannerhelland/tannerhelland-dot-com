---
author: tanner_h
date: 2009-03-01 22:56:21+00:00
excerpt: 'This little program demonstrates two key graphics programming principles: 1) simple "painting" code - basically, connecting a series of lines together as the user drags their mouse around, and 2) an implementation of a built-in Windows function for filling a contiguous region of an image.  (Photoshop users will know this as the "paint bucket" tool.)'
layout: post
slug: fill-image-regions
title: Code for Filling Image Regions 
redirect_from:
 - /649/fill-image-regions
---

This little program demonstrates two basic graphics programming principles:

1) Simple "painting" code - basically, connecting a series of lines together as the user drags their mouse around.

2) An implementation of the built-in Windows API function "ExtFloodFill", which can fill a contiguous region of an image.  (Photoshop users may know this as the "paint bucket" tool.)

ExtFloodFill requires the following declaration (VB format):

    Private Declare Function ExtFloodFill Lib "gdi32" (ByVal hDC As Long, ByVal x As Long, ByVal y As Long, ByVal crColor As Long, ByVal wFillType As Long) As Long
    
To use the program, draw several lines using the left mouse button, then fill contiguous regions (with random colors) via the right button.  

![fill_screenshot](images/fill_screenshot-300x252.png)

**[Download the sample app and source code from GitHub](https://github.com/tannerhelland/vb6-code/tree/master/Fill-image-region)**

For a much more powerful (and complicated) region-fill implementation, you might review [the source code for the fill tool](https://github.com/tannerhelland/PhotoDemon/blob/master/Classes/pdFloodFill.cls) in [PhotoDemon, my open-source photo editor](https://photodemon.org).