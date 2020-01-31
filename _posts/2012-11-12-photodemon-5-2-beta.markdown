---
author: tanner_h
date: 2012-11-12 20:50:38+00:00
excerpt: Another PhotoDemon update is nearing completion, which means it's time for you to try and break it.  Download a free copy of PhotoDemon today, give it a spin, and let me know what you think.
layout: post
slug: photodemon-5-2-beta
title: Announcing PhotoDemon 5.2 Beta 1 - Testers Needed!
redirect_from:
 - /4598/photodemon-5-2-beta
---

**Note: this is an old article!  [PhotoDemon now has its own website at photodemon.org](https://photodemon.org).**

![PhotoDemon 5.2 beta 1 screenshot](images/PhotoDemon-_5.2_beta1-600x389.jpg)

It's time for another PhotoDemon update.  This update includes many new tools, including PhotoDemon's first on-canvas tool - "Selections".

## Summary

**PhotoDemon 5.2 is nearing completion, and I need help testing it.**  

Version 5.2 provides a bunch of new features, including selections, cropping, HSL adjustment, CMY/CMYK rechanneling, a new Sepia filter (based off the W3C standard), an overhauled preferences engine and interface, and more.  Please download the beta and help me make sure everything is working properly.

## Download

[**Download PhotoDemon v5.2 beta 1** (1.6mb - 12 Nov 2012)](https://photodemon.org/download/)

Remember - if you are an advanced user, you can always download the most recent development build of PhotoDemon's source code from [its GitHub page](https://github.com/tannerhelland/PhotoDemon).

## List of what's new and improved in v5.2 (so far)

  * Selection tool!  It's a hell of a tool, and a lot of work went into making it as user-friendly and powerful as possible.  Three render modes are provided.  On-canvas resizing and moving are fully supported as well.  Everything in the Color and Filter menus will operate on a selection if available, as well as the Edit -> Copy command.  (Note: as of this beta, selections are not yet tied into Undo/Redo, and selections will not be recorded as part of a Macro.)

![PhotoDemon Selection Tool](images/PhotoDemon_selection_HSL_demo-600x451.jpg)

*Here's an example of the selection tool in action.  Note that the HSL adjustment tool is only operating on the selected area.*

  * Image cropping is now possible via the Crop-to-Selection option (in the Image menu).

  * New HSL adjustment tool.  (See above screenshot for sample.)

  * New Rechannel tool.  Live previews, CMY, and CMYK color spaces were added.

![](images/PhotoDemon_rechannel_tool.jpg)

  * New Sepia filter based off the official W3C formula ([available here](https://dvcs.w3.org/hg/FXTF/raw-file/tip/filters/index.html)).  I still prefer PhotoDemon's "Filters -> Antique" effect, but felt it was worthwhile to make both available.

![](images/fall_scene_sepia-600x450.jpg)

  * Vast improvements to PhotoDemon's support for images with transparency.  Images with alpha-channels will now be rendered as alpha in all filter and tool screens.  When printing, saving as 24bpp, or copying to the clipboard, the image will be composited against a white background.  User preferences were also added for transparency checkerboard color and sizes.

  * All-new User Preferences dialog.  Many new options were added, and the Preferences interface is now sorted by category.

![](images/PhotoDemon_new_Preferences_Dialog.jpg)

*Interface-related options in the new Preferences dialog.*

![](images/PhotoDemon_new_Preferences_Dialog_Transparency.jpg)

*As another example, here are the afore-mentioned transparency handling options.*

  * Improved font rendering is now available for users on Windows Vista, Windows 7, and Windows 8.

  * A drop-shadow can now be rendered between the image and the canvas (similar to [Paint.NET](http://www.getpaint.net/)).

  * PhotoDemon is now capable of remembering its window size and position between sessions.

  * Multiple monitors are now supported by the Import -> Screen Capture tool.

  * Many miscellaneous interface improvements.  Additionally, I am testing a new layout in the Color -> Grayscale tool.  This layout style is intended to help users make sense of PhotoDemon's many options.  Let me know what you think, because if this style is popular, I will redo the other tool dialogs to match.

  * Heavily optimized viewport rendering.  PhotoDemon now uses a triple-buffer rendering pipeline to speed up actions like zooming, scrolling, and using on-canvas tools like the new Selection Tool.  Even when working with 32bpp images, all actions should render in real-time on any modern system.

  * Bilinear interpolation is now used in "Convert to Isometric Image".  This results in a much higher-quality transform.  Hard edges are still left along the image border to make mask generation easy for game designers.

  * Many bug fixes and miscellaneous improvements.  For complete details, please visit the commit log at [https://github.com/tannerhelland/PhotoDemon/commits/master](https://github.com/tannerhelland/PhotoDemon/commits/master)
