---
author: tanner_h
date: 2012-11-28 19:53:07+00:00
excerpt: PhotoDemon v5.2 is now available.  New features include selection tools, arbitrary rotation, HSL adjustments, CMY/K rechanneling, many new user preferences, multiple monitor support, and more...
layout: post
slug: photodemon-5-2-update
title: Announcing PhotoDemon 5.2 - Selections, HSL, Rotation, HDR, and More
redirect_from:
 - /4616/photodemon-5-2-update
 - /4616/photodemon-5-2-update/
---

**Note: this is an old article!  [PhotoDemon now has its own website at photodemon.org](https://photodemon.org).**

## Summary

PhotoDemon v5.2 is now available.

New features include selection tools, arbitrary rotation, HSL adjustments, CMYK support, new user preferences, multiple monitor support, and more.  

**[Download the update here](https://photodemon.org/download/).**

![PhotoDemon 5.2](images/PhotoDemon_5.2_selections_and_HSL-600x367.jpg)

## New Feature: Selection Tool

Selections have been one of the top-requested PhotoDemon features since it first released, so I'm glad to finally be able to offer them.  A lot of work went into making selections as user-friendly and powerful as possible.

Three render modes are provided.  On-canvas resizing and moving are fully supported, as are adjustments by textbox (see screenshot above).  Everything in the Color and Filter menus will operate on a selection if available, as well as the Edit -> Copy command. 

(Note: as of this v5.2, selections are not yet tied into Undo/Redo, and selections will not be recorded as part of a Macro.  These features will be added in the next release.)

## New Feature: Crop to Selection

![](images/Crop-to-Selection1.png)

Finally!

## New Feature: HSL Adjustments

![](images/HSL-Adjustments.png)

PhotoShop and GIMP users should be happy about this tool.

## New Feature: Arbitrary (Free) Rotation

![](images/Arbitrary-Rotation.png)

Arbitrary rotation comes courtesy of the FreeImage library.  A 3-shear method is used: very fast, very high quality.

## New Feature: CMY/K Rechanneling

![](images/CMYK-rechanneling.png)

Both CMY and CMYK rechanneling are now available.

## New Feature: Sepia (W3C formula)

![](images/fall_scene_sepia.jpg)

Here's the sepia version of the photo from the Rechannel screenshot.  I still prefer PhotoDemon's "Antique" filter for most photos, but this sepia formula (from the W3C spec) provides a pleasant, flat alternative.

## New Feature: Preferences Dialog (rewritten from scratch)

![](images/Preferences-Dialog-600x436.png)

Preferences, preferences, and more preferences.  The old Preferences dialog was pretty lame, so it was due for an overhaul.  Tons of new settings have been added, and they are now organized by category.

New preferences include:

Interface:

  * Render drop shadows between images and canvas (similar to [Paint.NET](http://www.getpaint.net/))
  * Full or compact file paths for image windows and Recent File shortcuts
  * Improved font rendering on Vista, Windows 7, and Windows 8 (via Segoe UI)
  * Remember the main window's location between sessions

Loading and Saving:

  * Tone map imported HDR and RAW images
  * Options for importing all frames or pages of multi-image files (animated GIFs, multipage TIFFs)

Tools:

  * Automatically clear selections after "Crop to Selection" is used

Transparency handling:

  * Pick your own transparency checkerboard colors
  * Pick from three transparency checkerboard sizes (4x4, 8x8, 16x16)
  * Allow PhotoDemon to automatically remove empty alpha channels from imported images

All preferences from v5.0 remain present, and there is now an option to reset all preferences to their default state - so experiment away!

## New Feature: Recent File Previews (Vista, Windows 7, Windows 8 only)

![](images/Recent-File-Previews.png)

Now that recent file previews are available, I honestly can't use any software that *doesn't* provide the feature.  It makes locating the right file significantly easier - especially with digital camera filenames like IMG_0366.jpg.

## New Feature: Multi-Image File Support (animated GIFs, multipage TIFFs)

![](images/Multipage-Import-Tool.png)

PhotoDemon will now recognize when you try to load image files that are actually composed of multiple images.  You are given the option to import every image, or just the first one (which is what most other software does).  The default behavior can be changed in the Edit -> Preferences menu.

## New Feature: Waaaay better transparency handling, including adding/removing alpha channels

It's hard to overstate how much better transparency support is in v5.2 compared to v5.0.  Images with alpha-channels are now rendered as alpha in all viewport, filter, and tool screens.  When printing, saving as 24bpp, or copying to the clipboard, transparent images are automatically composited against a white background.  As mentioned previously, user preferences have been added for transparency checkerboard color and sizes.

PhotoDemon also allows you to add or remove alpha channels entirely.  Here's an example of an image with an alpha channel, and the associated "Image Mode" setting:

![](images/Image-Mode-Web-600x369.png)

Note how the top-level "Mode" icon has changed to match the current mode - this saves you from having to go to the sub-menu to check.  I'm a big fan of small touches like this.

And here it is again, after clicking the "Mode -> Photo (no transparency)" option:

![](images/Image-Mode-Photo-600x370.png)

No more alpha!

Finally, PhotoDemon now validates all incoming alpha channels.  If an image has a blank or irrelevant alpha channel, PhotoDemon will automatically remove it for you.  This frees up RAM, improves performance, and leads to a much smaller file size upon saving.  (Note: this feature can be disabled from the Edit -> Preferences menu if you want to maintain blank alpha channels for some reason.)

## New Feature: Custom "Confirm Unsaved Image(s)" Prompt

![](images/Unsaved-Changes-Prompt.png)

This is the new "unsaved images" prompt in PhotoDemon.  A preview is now provided - again, very important for digital photos with obscure names - and the options have been reworked to make them as crystal-clear as possible.  Also handy is the "Repeat this action for all unsaved images" option, which will either save or not save all unsaved images per your request.

## Improved Feature: Edge Detection

![](images/Find-Edges.png)

Edge detection now allows for on-black or on-white processing.  Generally speaking, on-white is used for artistic purposes, while on-black is used for technical and research ones.  (Thanks to [Yvonne Strahovski](http://en.wikipedia.org/wiki/Yvonne_Strahovski), who appears in the sample image above.)

## New Feature: Thermograph Filter

[This Wikipedia article](http://en.wikipedia.org/wiki/Thermography) describes thermography in great detail.  PhotoDemon's thermography filter works by correlating luminance with heat, and analyzing the image accordingly.  Here's a sample, using a picture of the lovely [Alison Brie](http://www.imdb.com/name/nm1555340/), of _Mad Men_ and _Community_ fame:

![](images/Sample-Thermograph-Filter-600x401.jpg)

## New Feature: JPEG 2000 (JP2/J2K), Industrial Light and Magic (EXR), High-Dynamic Range (HDR) and Digital Fax (G3) image support

PhotoDemon now supports importing the four image types mentioned above, and it also supports JPEG 2000 exporting.

## Other New and Improved Features:

  * Much faster resize operations, thanks to [an updated FreeImage library (v3.15.4)](http://freeimage.sourceforge.net/news.html)
  * Multiple monitor support during screen captures (File -> Import -> Screen Capture)
  * Many miscellaneous interface improvements, including generally larger command buttons, text boxes, labels, and more uniform form layouts.
  * Many new and improved menu icons.
  * Heavily optimized viewport rendering. PhotoDemon now uses a triple-buffer rendering pipeline to speed up actions like zooming, scrolling, and using on-canvas tools like the new Selection Tool. Even when working with 32bpp images, all actions render in real-time.
  * Bilinear interpolation is now used during Isometric Conversion. This results in a much higher-quality transform. Hard edges are still left along the image border to make mask generation easy for game designers.
  * Vastly improved image previewing when importing from VB binary files.
  * Better text validation throughout the software.  Invalid values are now handled much more elegantly.
  * More accelerator hotkey support, including changes to match Windows standards (such as Ctrl+Y for Redo, instead of the previous Ctrl+Alt+Z).
  * Update checks are now performed every ten days (instead of every time the program is run).
  * All extra program data - including plugins, preferences, saved filters and macros - have been moved to a single /Data subfolder.  If you run PhotoDemon on your desktop, this should make things much cleaner for you.
  * PhotoDemon's current and max memory usage is now displayed in the Preferences -> Advanced panel.
  * Tons of miscellaneous bug fixes, tweaks, and optimizations. For a full list of changes, visit [https://github.com/tannerhelland/PhotoDemon/commits/master](https://github.com/tannerhelland/PhotoDemon/commits/master)

## In Conclusion...

Not bad for two months work, eh?  I hope you enjoy all the new features in 5.2., and [please remember to donate if you find the software useful](donate/)!
