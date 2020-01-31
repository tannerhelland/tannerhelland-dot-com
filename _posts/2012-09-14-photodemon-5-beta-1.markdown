---
author: tanner_h
date: 2012-09-14 00:54:17+00:00
excerpt: PhotoDemon's biggest update in years is nearing completion, which means it's time for you to try and break it.
layout: post
slug: photodemon-5-beta-1
title: Announcing PhotoDemon 5.0 Beta 1 - Testers Needed!
redirect_from:
 - /4394/photodemon-5-beta-1
---

**Note: this is an old article!  [PhotoDemon now has its own website at photodemon.org](https://photodemon.org).**

![](images/photodemon_50b1-600x450.jpeg)

## Summary

**PhotoDemon 5.0 is nearing completion, and I need help testing it.**  Version 5.0 includes an all-new image subsystem that required rewriting every filter and effect in the program (and some 17,000 lines of code!).  All those changes have made the software significantly faster and smoother, but it might also have broken a few things.  Download the beta and help me make sure everything is working the way it's supposed to.

## Download

[**Download PhotoDemon v5.0 beta 1** (1.53mb - 13 Sept 2012)](https://photodemon.org/download/)

Remember - if you are an advanced user, you can always download the most recent development build of PhotoDemon's source code from [its GitHub page](https://github.com/tannerhelland/PhotoDemon).

## PhotoDemon 5.0: A Bit of Background

As you might know, PhotoDemon has [a long and complicated history](4183/photodemon-image-processor-vb6/) spanning some 12 years.  That longevity has some perks - for example, tons of features - but it also has some downsides.

One of the biggest downsides to being 12 years old is that the software carries with it some bad design choices, made many years ago when I was a young and immature programmer, that have perpetually bogged down the implementation of new and exciting features.  In particular, features like large images, selections, and alpha-channel (transparency) support have all been impossible because of the way PhotoDemon stores and renders images.  Originally, the software was only meant to work on 8-bit images, and 24-bit support was later tacked on as an afterthought.  I took that framework as far as I could go, but upon releasing PhotoDemon to the public earlier this year, I realized that it was time to fix that problem.

Enter version 5.0.

PhotoDemon 5.0 has just about been rewritten from the ground up, and I don't say that lightly.  The software is comprised of some 30,000 lines of code, and version 5.0 involved the writing of _more than half (17,000)_ of those lines.  Why?  Because it was finally time for a completely new image subsystem, one capable of potentially supporting selections, alpha-channels, high bit-depths, layers, and whatever else I might want to someday throw at it. 

(Note: features like selections are not yet part of PhotoDemon.  They will take a good chunk of time to write - but at least now it will be physically possible to add them!)

This new image subsystem is something I'm very proud of.  At a high level, it's basically a specialized image class that stores and tracks all image data, and passes that data between the screen, image files, and various filters and effects.  The subsystem does not rely on anything specific to Visual Basic (the programming language PhotoDemon is written in), meaning it is capable of supporting any features it wants - regardless of whether or not VB actually supports them.  Past versions of PhotoDemon relied on VB's inherent "picture boxes", as they are called, for image storage and processing, and because VB6 is now 14 years old it simply couldn't handle things like large images or transparency.

But no more.

This rewrite has been a massive project, and every single filter and tool (every damn one!) had to be rewritten to accommodate the new technology.  This proved to be a good thing, because I hadn't revisited some of those filters for over a decade, and in the past ten years I've learned a great deal about writing cleaner, better, faster imaging code.  That made this a prime chance to re-engineer every filter and tool in the program to make it as fast and accurate as possible, and I think you'll like the result.

But enough about this - you probably want to know what's actually new in PhotoDemon 5.0.  I won't discuss everything here (some features are still under construction), but here are the highlights.

## List of what's new and improved in v5.0 beta 1


  * Everything is faster - all filters, tools, effects, loading images, saving images, macros, batch conversion, undo/redo.  Seriously - EVERYTHING.

  * Completely rewritten image load/save code.  As an example of how much better the new version is: I ran two identical batch conversions of 138 wedding photos (10 megapixels each, 3872x2592 pixels).  The batch conversion was simple - load each image, then save it in another folder at a different JPEG quality.  PhotoDemon 4.4 did the conversion in 2 minutes 21 seconds.  The PhotoDemon 5.0 beta did it in 1 minute 11 seconds. (Thanks to Herman Liu for much testing and help with the implementation!)

  * Redesigned menus.  Every item has a descriptive icon, and menus have been reorganized according to improved design rules

![](images/photodemon_5_color_menu.png)

  * Drag-and-Drop compatibility.  Drag images from your desktop or file manager onto PhotoDemon, and it will open them all automatically. (Thanks to [Kroc of camendesign.com](http://camendesign.com/) for the suggestion!)

  * MUCH better Wine compatibility for OSX and Linux users.  Undo/Redo and all tools and effects should now work under Wine.  Let me know if you find any that do not. 

  * New "Tile" tool tiles the current image to a target size (in pixels) or number of tiles. (Thanks to Ye Peng for the suggestion!)

![](images/PhotoDemon-5b1-Tile-Tool.jpg)

  * New "Duplicate Image" tool.  Perfect for making a working copy of an image without fear of overwriting the original. (Thanks to Achmad Junus for the suggestion!)

  * Auto-Enhance overhaul.  All four auto-enhance tools (contrast, highlights, midtones, shadows) have been rewritten from scratch using completely new algorithms.  I think you'll find them way more useful than the old tools.

  * Improved mosaic tool.  Faster, higher quality, and mosaics can now be as large as the image or as tiny as one pixel in either dimension.

  * Added previewing to a bunch of forms that lacked it before - Reduce Colors (Quantize), Black and White Conversion, Find Edges

  * Increased size of all preview windows.  They are now much larger, which makes it easier to see how a filter or tool will affect an image.

  * Improved handling of edge pixels for all convolution filters (blur, soften, sharpen, etc)

  * Improved color reduction algorithms (faster and higher quality)

  * Floating-point implementation of histogram equalization means it is now significantly more accurate

  * DPI-aware images mean no more distortion at 120dpi - a big improvement for people using "larger font" settings in Windows

  * No limit on image sizes.  The bigger, the better. (Thanks to Robert Rayment for his help with this bug!)

  * Full GDI+ support for saving and loading.  If the FreeImage plugin can't be found, GIF/JPEG/PNG/TIFF import and export will still be available. (Thanks to Alfred Hellmueller for the suggestion to add GDI+ compatibility!)

  * Turbo JPEG loading while batch conversions are running

  * Improved bug reporting system and online form to match

  * Tons of miscellaneous bug fixes, tweaks, and optimizations
