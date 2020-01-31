---
author: tanner_h
date: 2013-02-27 19:10:58+00:00
excerpt: Another PhotoDemon update is nearing completion, and I need help testing it.  Download a free copy, give it a spin, and let me know what you think.  Lots of new features in this release, including French, German, and Dutch language support, distortion tools, upgraded Blur and Sharpen tools (including a new Smart Blur), JPEG/PNG optimization, and more.
layout: post
slug: photodemon-5-4-beta
title: 'PhotoDemon 5.4 Beta Now Available '
redirect_from: 
 - /4738/photodemon-5-4-beta
 - /4738/photodemon-5-4-beta/
---

**Note: this is an old article!  [PhotoDemon now has its own website at photodemon.org](https://photodemon.org).**

## Summary

**PhotoDemon 5.4 is nearing completion, and I need help testing it.**  

Version 5.4 provides a bunch of new features, including French, German, and Dutch (Flemish) language support.  If you can help translate PhotoDemon into another language, please let me know!  The translation process is very simple, and it requires no programming experience or special software.

Version 5.4 also includes nine new distort tools, tons of new file format features including specialized PNG and JPEG optimization, improved memory management, a new plugin manager, real-time Gaussian, Smart, and Box blur tools with variable radius, a full Unsharp Mask tool, vignetting, median filtering, adding film grain, automatic cropping, contour tracing, a new Batch Wizard, redesigned tool interfaces, and more.  Please download the beta and let me know if you find any bugs.

## Download

[**Download PhotoDemon v5.4 beta** (2.32mb - 18 March 2013)](https://photodemon.org/download/)

Remember - if you are an advanced user, you can always download the most recent development build of PhotoDemon's source code from [its GitHub page](https://github.com/tannerhelland/PhotoDemon).

## List of what's new and improved in v5.4 (so far)

  * **Official support for multiple languages.**  This is the biggest addition in version 5.4, and I can only claim partial credit for it.  Primary credit goes to Frank Donckers, a fellow VB programmer and the one who prototyped the initial translation engine.  Frank also supplied the translations for French, German, and Dutch (Flemish), so I owe him an enormous debt of gratitude.

  * **Vastly improved file format support.**  JPEGs now support automatic EXIF rotation on import, and a variety of options on export (Huffman table optimization, progressive scan, thumbnail embedding, specific subsampling).  TIFF exporting supports CMYK encoding and a number of compression schemes (none, PackBits, LZW, CCITT 3 and 4, zLib, and more).  PNG exporting supports variable compression strength, interlacing, and background color chunk.  PPM exporting supports RAW or ASCII encoding.  BMP and TGA now support RLE encoding.  For ICO files, all icons inside the file can now be loaded (instead of just the first one).

  * **Nine new Distort-style tools.**  Add and remove lens distortion.  Swirl.  Ripple.  Pinch and whirl.  Waves.  Kaleidoscope.  Polar conversion (both directions).  Figured glass (dents).

  * **New and improved standard tools, including Box Blur, Gaussian Blur, Smart Blur, and Unsharp Masking.**  Each of these functions now supports variable radii (up to hundreds of pixels), and all have been heavily optimized.  Gaussian Blur is the fastest VB-only true gaussian ever written.  (Not a joke.)

  * **Tons of new tools, including Film Grain, Color Balance, Vignetting, Autocrop, Median, Modern Art, Trace Contour, Shadow/Midtone/Highlight, Monochrome -> Grayscale conversion, Film Noir, and Comic Book.**  All tools include real-time previews.  A number of existing tools received big updates as well - particularly Gamma Correction, Dilate, Erode, Monochrome Conversion, and Printing.

  * **New Batch Process wizard.**  This replaces the old Batch Convert tool, which was an interface nightmare.  The new tool supports a number of new features, including drag/drop support of batch lists, live image previews, and tons of file renaming options (prefix, suffix, case conversion, removing text, conversion of spaces to underscores for web).

  * **Universal color depth support at import and export time.**  PhotoDemon can now write 1, 4, 8, 24, and 32bpp variations of every supported file format.  Color depth detection is automatic at save time - the program will count the number of colors in an image and automatically save to the most appropriate color depth.  Alternatively, you can set a preference to manually specify color depth at save time.  This also works for grayscale images; for example, the JPEG encoder will now detect grayscale images and write out 8bpp JPEGs accordingly.  Alpha thresholding is also available when saving 32bpp images to 8bpp (e.g. PNG to GIF).

  * **New pngnq-s9 plugin for optimizing PNG files.**  [Pngnq-s9](http://sourceforge.net/projects/pngnqs9/) is an optimized and feature-rich variant of the original [pngnq](http://pngnq.sourceforge.net/) optimization library.  Pngnq-s9 works by converting 32bpp PNG files to 8bpp with a heavily optimized palette, including support for variable alpha channels.  File size savings of over 50% are common.  See the Options -> Plugin Manager -> pngnq-s9 menu for a full list of tunable parameters.

  * **New plugin manager and plugin downloader.**  Plugins can now be individually enabled/disabled, and missing plugins can be automatically downloaded.  All plugin installation and activation/deactivation can be applied without a program restart.

  * **Many canvas and interface improvements.**  Larger effect and tool previews.  Persistent zoom-in/zoom-out buttons.  Image URLs and files can now be directly pasted as new images.  Improved drag/drop support, including drag/drop from common dialogs.  New "Safe" save behavior to avoid overwriting original files.  New Close All Images menu.  New algorithms for auto-zoom when images are loaded, meaning much better results at all screen sizes.  Tool and file panels can now be hidden.  Higher-quality dynamic icons for the program, taskbar, child windows, and Recent Images list.  Improved support for low screen resolutions.

  * **Many performance improvements.**  More aggressive memory management means lower resource usage.  Program loading has been heavily streamlined, and now happens in less than a second on modern hardware.  Image loading is much faster and more robust, including better support for damaged or incomplete image files.

  * **Much more robust and comprehensive error handling.**  When loading multiple images, the program will now suppress warnings and failures (such as invalid files) until all images have been loaded.  Many subclassing issues have been resolved - so no more surprise crashes!  Overall this release should be extremely stable.

  * **Many miscellaneous bug fixes and improvements.**  For a full list, see the commit log at [https://github.com/tannerhelland/PhotoDemon/commits/master](https://github.com/tannerhelland/PhotoDemon/commits/master)

## Known bugs

Here is a list of known bugs with the current beta.  These bugs will be fixed before the final release.

  * When a new language is selected, some text may not be translated.  This is not a problem with the translation engine - it is a problem with the translation files, which are still being finalized.  All text will be translated in the final release.

  * When using a language other than English, some text may overflow its boundaries or disappear off the page.  This is a known problem that is still being worked on.  All text - in any language - should fit properly in the final release.
