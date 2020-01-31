---
author: tanner_h
date: 2013-09-19 18:22:13+00:00
excerpt: It's taken nearly six months, but PhotoDemon 6.0 is finally ready for release.  I've already talked about some of the great features this release includes, like powerful selection tools, EXIF and other metadata support, Curves and other new tools, so I'd recommend glancing through the linked article if you're curious.  Since that article was written, a number of other features have been added or improved...
layout: post
slug: photodemon-60-beta
title: PhotoDemon 6.0 beta is live
redirect_from:
 - /5106/photodemon-60-beta
 - /5106/photodemon-60-beta/
---

**Note: this is an old article!  [PhotoDemon now has its own website at photodemon.org](https://photodemon.org).**

![Chroma key (green screen) is one of many new tools in this release.](images/PD_chroma_key_after-600x350.jpg)

*Chroma key (green screen) is one of many new tools in this release.*

## Download

[**PhotoDemon 6.0 beta** (6.2mb - 19 September 2013)](https://photodemon.org/download/)

Remember: if you're an advanced user, you never have to wait for a beta release.  You can always download PhotoDemon's latest development release from [its GitHub page (source code)](https://github.com/tannerhelland/PhotoDemon), or from [this nightly build permalink (program only)](https://photodemon.org/download/).

## Overview

It's taken nearly six months, but PhotoDemon 6.0 is finally ready for release.  I've [already talked about some of the great features this release includes](2013/08/01/photodemon-60-preview), like powerful selection tools, metadata (EXIF) support, Curves and other new tools, so I'd recommend glancing through the linked article if you're curious.

Since that article, a number of other features have been added or improved: 

  * All tools now support save/load presets, reset to default, randomize, and automatic save/load of last-used settings.  These items are all accessible from a new "command bar" at the bottom of each tool dialog.

![From left-to-right, the command bar includes buttons for: reset, randomize, saved presets, and save current settings as preset.  Last-used settings are automatically saved and loaded by the dialog.](images/PD_curves_commandbar-600x392.jpg)

From left-to-right, the command bar includes buttons for: reset, randomize, saved presets, and save current settings as preset.  Last-used settings are automatically saved and loaded by the dialog.

  * Three new blur tools: motion, radial, and zoom blur.  These tools [outperform similar tools in GIMP and Paint.NET](2013/09/18/performance-photodemon-gimp-paintnet).

![PhotoDemon's new radial blur tool is 4x faster than Paint.NET's, and 30x faster then GIMP's - and at high angles, it produces significantly better output.](images/PD_radial_blur-600x344.jpg)

PhotoDemon's new radial blur tool is 4x faster than Paint.NET's, and 30x faster then GIMP's - and at high angles, it produces significantly better output.

  * Much faster Gaussian and Box blur tools (20x improvement!)

![The updated Gaussian Blur tool now provides quality settings for improved performance.  For most photos, the difference between "good" and "best" will be indistinguishable, but "good" will be some 20x faster.](images/PD_gaussian_blur-600x344.jpg)

The updated Gaussian Blur tool now provides quality settings for improved performance.  For most photos, the difference between "good" and "best" will be indistinguishable, but "good" will be some 20x faster.

  * A new [chroma key](http://en.wikipedia.org/wiki/Chroma_key) ("green screen") tool with performance comparable to professional tools, including full support for edge blending.  Find it in the Image -> Transparency -> Make color transparent menu.

![Before color removal; image courtesy http://dimula73.blogspot.com/2013/03/new-user-interface-for-krita-color-to.html](images/PD_chroma_key_before-600x350.jpg)](http://www.tannerhelland.com/5106/photodemon-60-beta/pd_chroma_key_before/)

Before color removal; image courtesy [http://dimula73.blogspot.com/2013/03/new-user-interface-for-krita-color-to.html](http://dimula73.blogspot.com/2013/03/new-user-interface-for-krita-color-to.html)

![After color removal.  Note that the tool creates a 32bpp image, which you can then composite using any photo editing software.](images/PD_chroma_key_after-600x350.jpg)

After color removal.  Note that the tool creates a 32bpp image, which you can then composite using any photo editing software.

  * A new Language Editor makes contributing new translations fast and easy.

![The new Language Editor makes it easier than ever to get involved in translation.  Please contact me if you can help!  (You will receive full credit for your work.)](images/PD_Language_Editor-600x365.jpg)

The new Language Editor makes it easier than ever to get involved in translation.  Please [contact me](contact/) if you can help!  (You will receive full credit for your work.)

  * New variable-strength Sharpen tool

![Previously, PhotoDemon only provided set "Sharpen" and "Sharpen More" functions.  The new tool allows for floating-point adjustments, which allow for much more nuanced fixes.  (Unsharp Masking is still available too, obviously!)](images/PD_sharpen_tool-600x344.jpg)

Previously, PhotoDemon only provided set "Sharpen" and "Sharpen More" functions.  The new tool allows for floating-point adjustments, which allow for much more nuanced fixes.  (Unsharp Masking is still available too, obviously!)

  * New Oil Painting tool

![Same photo as the screenshot at the top of this page, but oil-ified.](images/PD_Oil_Painting-600x387.jpg)

*Same photo as the screenshot at the top of this page, but oil-ified.*

  * Minor improvements to many tools, including polar coordinate conversion, perspective correction, wave distort, ripple distort, figured glass, tile image, posterize, rotate, custom filters, histogram.

![The perspective tool now supports both forward and reverse transforms.  Reverse transforms allow you to simply trace a crooked object, and have it automatically straightened by the program.](images/PD_perspective_distort-600x395.jpg)

The perspective tool now supports both forward and reverse transforms.  Reverse transforms allow you to simply trace a crooked object, and have it automatically straightened by the program.

![The histogram offers new render options, which can be helpful for identifying areas of channel overlap.](images/PD_new_histogram-600x533.jpg)

The histogram offers new render options, which can be helpful for identifying areas of channel overlap.

  * Any tool with a "color" option now allows you to pick a color directly from the image by clicking the preview.

  * Much better support for high-DPI screens, including tablets.

  * Faster viewport rendering for 32bpp images.

Again, these new features are only a fraction of what 6.0 includes.  [Please check out the 6.0 preview article](2013/08/01/photodemon-60-preview) for news on all the other new tools and improvements.

## Acknowledgments

This 6.0 release represents six months of hard work from a variety of contributors.  While I am very grateful to all of PhotoDemon's talented contributors, a few deserve special mention.  Thank you to:

  * [Frank Donckers](http://www.planetsourcecode.com/vb/scripts/BrowseCategoryOrSearchResults.asp?lngWId=1&blnAuthorSearch=TRUE&lngAuthorId=2213335741&strAuthorName=Frank%20Donckers&txtMaxNumberOfEntriesPerPage=25) for again providing the German, French, and Dutch translations, and for contributing many pieces of code to the new Language Editor, including the Google Translate interface.  Amazing stuff.

  * [GioRock](http://www.planetsourcecode.com/vb/scripts/BrowseCategoryOrSearchResults.asp?lngWId=1&blnAuthorSearch=TRUE&lngAuthorId=77440558266&strAuthorName=GioRock&txtMaxNumberOfEntriesPerPage=25) for the Italian translation, and for detailed testing of many small translation items.  It takes a ton of work to get all of PD's text translating properly, and GioRock debugged many items for me, which benefits users of every language.

  * [Kroc Camen](http://camendesign.com/) for a new IDE-safe mouse interface class, derived from his own [open-source VB project](https://github.com/Kroc/MaSS1VE).  Kroc also reviews many of PD's individual commits, where he catches many small items I overlook.

  * [Robert Rayment](http://www.planetsourcecode.com/vb/scripts/ShowCode.asp?txtCodeId=66991&lngWId=1) for helping me profile and optimize a number of PD's more taxing functions, and for many suggestions on tweaks and improvements.  Many of the performance improvements available in this new version are a result of Robert's help.  Please check out his own [VB image editor](http://www.planetsourcecode.com/vb/scripts/ShowCode.asp?txtCodeId=66991&lngWId=1) if you can.

## Known bugs

  * <del>EXIF data is not maintained with certain combinations of preferences (delay loading EXIF + export full data when saving).  This is caused by a metadata caching issue, and will be fixed by release.</del>  Fixed!

  * <del>ExifTool plugin is slightly out of date.  It will be updated to its latest version upon 6.0's release.</del>  Fixed!

  * <del>Metadata menus sometimes become disabled even when metadata is available.  This will be fixed by release.</del>  Fixed!

  * <del>OK and Cancel buttons are not currently translated.  This will be fixed by release.</del>  Fixed!

  * <del>Some hotkeys don't fire unless the main form is first clicked.  This is a known problem with VB, and will _hopefully_ be fixed by release.</del>  Fixed!

  * Master language file is missing a few minor text entries.  This will be fixed by release.

The beta version was released before these small items were fixed, so it still contains these bugs.  Developers can download updated source code, with these fixes, [from GitHub](https://github.com/tannerhelland/PhotoDemon).

## Official release timeline

Barring any major bugs, the official 6.0 release should happen within several weeks.  Feature-wise, it will be identical to this beta release.  The only changes will be minor bug fixes and performance improvements.  Automatic update notifications for existing PhotoDemon installs will also go live at that point.
