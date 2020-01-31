---
author: tanner_h
date: 2013-09-30 22:50:45+00:00
excerpt: After a successful (and relatively bug-free!) beta testing session, PhotoDemon 6.0 is ready for you to download.
layout: post
slug: photodemon-60-live
title: PhotoDemon 6.0 is now live at photodemon.org
redirect_from: 
 - /5203/photodemon-60-live
 - /5203/photodemon-60-live/
---

**Note: this is an old article!  [PhotoDemon now has its own website at photodemon.org](https://photodemon.org).**

![The final splash screen for version 6.0.  Thank you again to all the talented contributors that made this release possible!](images/splash_2013-600x424.jpg)

*The final splash screen for version 6.0.  Thank you again to all the talented contributors that made this release possible!*

After a successful (and relatively bug-free!) beta testing session, PhotoDemon 6.0 has been deemed "ready for mass consumption".  Normally this is where I would put a download link, but let me instead refer you to the new home of all things PhotoDemon: [photodemon.org](https://photodemon.org/)

I thought it was finally time for PD to get its own online home, and [photodemon.org](https://photodemon.org/) is the result.  The site still has a few pieces left to assemble (most notably the Features section, which is only about half done), but I didn't want that to delay the availability of 6.0's release.

You can download version 6.0 from [the "Downloads" section of the new site](https://photodemon.org/download/), or from this direct link:

[Download PhotoDemon 6.0 (.zip file, 6.3 mb)](https://photodemon.org/download/)

Functionally, this release is very similar to [the 6.0 beta](2013/09/19/photodemon-60-beta) that launched two weeks ago.  The primary changes from the beta are miscellaneous bug fixes, performance improvements, and cosmetic adjustments.

If you are upgrading from version 5.4, you're going to notice a lot of new things!  You can get a full write-up of all the improvements [here](2013/09/19/photodemon-60-beta), or if you're in a hurry, here is the abbreviated list of updates:

  * All tools now support save/load presets, reset to default, randomize, and automatic save/load of last-used settings.
  * Italian language support.
  * Vastly improved support for non-US locales and non-English users.
  * Advanced selection tools, including rectangular, elliptical, and line selections.
  * All selection types now support feathering, live move/resize, interior/exterior/border types, and antialiasing.
  * Selection actions are fully integrated into Undo/Redo, and selections can be saved to disk.
  * Full preservation of all types of image metadata (EXIF, XMP, IPTC, etc).  Metadata can be browsed via a new metadata browser.
  * Official RAW image format support; more than 20 RAW filetypes are now supported.
  * Three new blur tools: motion, radial, and zoom blur.  Also, big improvements to Gaussian and Box Blur.
  * A new chroma key (“green screen”) tool with performance comparable to professional tools, including full support for edge blending.
  * New Perspective tool, with support for forward and reverse transforms.
  * New Photo Filter tool, with support for 50 digital photo filters (Wratten-type).
  * New Curves tool.  Supports adding, moving, and removing an unlimited number of nodes.
  * New Channel Mixer tool.
  * New Canvas Resize tool.
  * New Spherize tool (for wrapping images around spheres).
  * New Vibrance tool.
  * New Pan and Zoom, Poke, Shear, and Squish distortion tools.
  * A new Language Editor for translators.
  * New variable-strength Sharpen tool.
  * New Oil Painting tool.
  * Many improvements to the Batch Wizard, including dedicated options for batch resizing.
  * Minor improvements to many tools, including polar coordinate conversion, wave distort, ripple distort, figured glass, tile image, posterize, rotate, custom filters, histogram, resize.
  * Any tool with a “color” option now allows you to pick a color directly from the image by clicking the preview.
  * Much better support for high-DPI screens, including tablets.
  * Support for transparent clipboard images, allowing you to move layered images between GIMP and PhotoDemon.
  * Filters and other long-running actions can now be canceled mid-action by pressing ESC.

## Acknowledgments

This 6.0 release represents six months of hard work from a variety of contributors.  While I am very grateful to all of PhotoDemon's talented contributors, a few deserve special mention.  Thank you to:

  * [Frank Donckers](http://www.planetsourcecode.com/vb/scripts/BrowseCategoryOrSearchResults.asp?lngWId=1&blnAuthorSearch=TRUE&lngAuthorId=2213335741&strAuthorName=Frank%20Donckers&txtMaxNumberOfEntriesPerPage=25) for again providing the German, French, and Dutch translations, and for contributing many pieces of code to the new Language Editor, including the Google Translate interface.  Amazing stuff.

  * [GioRock](http://www.planetsourcecode.com/vb/scripts/BrowseCategoryOrSearchResults.asp?lngWId=1&blnAuthorSearch=TRUE&lngAuthorId=77440558266&strAuthorName=GioRock&txtMaxNumberOfEntriesPerPage=25) for the Italian translation, and for detailed testing of many small translation items.  It takes a ton of work to get all of PD's text translating properly, and GioRock debugged many items for me, which benefits users of every language.

  * [Kroc Camen](http://camendesign.com/) for a new IDE-safe mouse interface class, derived from his own [open-source VB project](https://github.com/Kroc/MaSS1VE).  Kroc also reviews many of PD's individual commits, where he catches many small items I overlook.

  * [Robert Rayment](http://www.planetsourcecode.com/vb/scripts/ShowCode.asp?txtCodeId=66991&lngWId=1) for helping me profile and optimize a number of PD's more taxing functions, and for many suggestions on tweaks and improvements.  Many of the performance improvements available in this new version are a result of Robert's help.  Please check out his own [VB image editor](http://www.planetsourcecode.com/vb/scripts/ShowCode.asp?txtCodeId=66991&lngWId=1) if you can.

## Enjoy!

I hope you enjoy version 6.0.  If you have any feedback, please [send me a message](contact/).  I'd love to hear from you.
