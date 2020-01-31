---
author: tanner_h
date: 2012-09-22 04:41:09+00:00
excerpt: PhotoDemon v5.0 is now available. It's the biggest update PhotoDemon has seen in years, and it's awesome.
layout: post
slug: photodemon-5-0-update
title: Announcing PhotoDemon 5.0 - Everything is Faster, Everything is Better
redirect_from:
 - /4407/photodemon-5-0-update
---

**Note: this is an old article!  [PhotoDemon now has its own website at photodemon.org](https://photodemon.org).**

## Summary

**PhotoDemon v5.0 is now available. It's the biggest update PhotoDemon has seen in years, and it's awesome. [Download it here](https://photodemon.org/download/).**

![](images/5.0b2-600x384.jpg)

## New Feature: All-New Image Subsystem

In version 5.0, the way PhotoDemon stores and processes image data has been rewritten from scratch. What does this mean for you?
	
  * Filters, effects, and all tools are faster than version 4.4.
  * The software uses roughly half the RAM of previous versions.
  * No more upper limit on image sizes. Huge photos (30+ megapixel) should work just fine on any modern PC. The only limiting factor is the amount of RAM (actual and virtual) available on your system.
  * Much faster batch conversions. As an example of how much better version 5.0 is: I ran two identical batch conversions of 138 wedding photos (10 megapixels each, 3872×2592 pixels). The batch conversion was simple – load each image, then save it in another folder at a different JPEG quality. PhotoDemon 4.4 performed the conversion in 2 minutes 21 seconds. PhotoDemon 5.0 does it in 1 minute 11 seconds.
  * Much better OSX and Linux compatibility via [Wine](http://www.winehq.org/). (Wine v1.4 or later is required.)

This sole feature was the largest update PhotoDemon has seen in the past five years. As a teaser, the new subsystem is also compatible with selections and layers, which may make an appearance in a future update...

## New Feature: Alpha-Channel (Transparency) Support

For the first time in the history of the program, PhotoDemon now provides proper transparency support. When images with an alpha-channel are loaded, PhotoDemon will automatically maintain the transparency data for the life of the image. When the image is saved to file, the alpha-channel is added back in, allowing you to do any amount of edits to images without harming the underlying alpha data.

Transformations like resizing and rotating also preserve the alpha channel. (Again, this was a prerequisite to features like layers... see a pattern here?)

## New Feature: Redesigned Interface

Every menu item in PhotoDemon now has a descriptive icon, and menus have been reorganized according to improved design rules. No menu is more than two layers deep, and new accelerators (hotkeys) have been added to popular features.

![](images/PhotoDemon_50_Color_Menu.jpg)

*The redesigned Color menu*

The left-hand bar has been updated once again. Per feedback from users, a dedicated Close and Save As button has been added, along with descriptive text for each button. Tool-tips have also been added to each button. (Thanks to Robert Rayment for the suggestion!)  Finally, the zoom box has been rebuilt with a new, more useful set of zoom values.

![](images/PhotoDemon_50_leftbar_tooltip.png)

*New left-hand bar in 5.0, including descriptive tool-tips.*

All preview boxes have been enlarged on tool, filter, and effect windows. Text has also been enlarged to improve readability. PhotoDemon was originally designed to run on 800x600 resolutions (that was a concern in 2001!) but there's no need for it to remain so compact in 2012.

![](images/find_edges_before_and_after-600x264.png)

*The old and new edge detection tools*

![](images/PhotoDemon_50_CustomFilter-600x451.jpg)

*The old and new Custom Filter tools*

Finally, a new View menu has been added to provide compatibility with other popular photo editors. The new menu is a great place to discover all the useful hotkeys (also called "accelerators") for popular zoom functions. The key listed on the right-hand side of a menu item can be used as a shortcut to that menu - so pressing the "+" key will zoom in, the "-" key will zoom out, and the "0" key will instantly fit the entire image on the screen.

![](images/PhotoDemon_50_View_Menu.jpg)

*The new View menu*

## New Feature: All-New Image Load/Save Engine

PhotoDemon 5.0 uses a completely new system for getting images into - and out of - the program. As you may know, the program relies on an outside library called [FreeImage](http://freeimage.sourceforge.net/features.html) for supporting non-standard image formats like Photoshop files (PSD), Macintosh PICT files (PICT), DirectDraw surfaces (DDS), and more.

FreeImage is an excellent tool, but its implementation in past versions of PhotoDemon was very rudimentary. PhotoDemon relied on FreeImage to do its own image file type detection, configure each image type properly, and prepare it for use within the program. While it was pretty good at guessing these parameters, it was not foolproof, and odd color-depths, transparencies, and mismatched file extensions could result in failed image loads or even program crashes.

So for version 5.0, the FreeImage interface was rewritten from the ground up. When images are loaded, a fallback system is used to identify the file format - first the file header is compared against a database of known filetypes. That works for 95+% of files. If for some reason a header cannot be found (which is the case with some formats, including outliers like CUT, MNG, PCD, TGA and WBMP), the image's file extension is then analyzed. If that fails, PhotoDemon will attempt to blindly load bitmap data and hope for the best. And, if even that fails, PhotoDemon will give the image one final try by passing control off to the Windows' GDI+ system and seeing if it can decipher the file.

This should make PhotoDemon as robust as possible when loading images. (Thanks to Herman Liu for much testing and help with the new image import implementation!)  The full list of file formats supported by PhotoDemon now includes:

Importing:

  * BMP - Windows Bitmap
  * DDS - DirectDraw Surface
  * GIF - Compuserve
  * ICO - Windows Icon
  * IFF - Amiga Interchange Format
  * JNG - JPEG Network Graphics
  * JPG/JPEG - Joint Photographic Experts Group
  * KOA/KOALA - Commodore 64
  * LBM - Deluxe Paint
  * MNG - Multiple Network Graphics
  * PBM - Portable Bitmap
  * PCD - Kodak PhotoCD
  * PCX - Zsoft Paintbrush (uncompressed only)
  * PDI - PhotoDemon Image (the program's native format)
  * PGM - Portable Greymap
  * PIC/PICT - Macintosh Picture
  * PNG - Portable Network Graphic
  * PPM - Portable Pixmap
  * PSD - Adobe Photoshop
  * RAS - Sun Raster File
  * SGI/RGB/BW - Silicon Graphics Image
  * TGA - Truevision Targa
  * TIF/TIFF - Tagged Image File Format
  * WBMP - Wireless Bitmap

Exporting:

  * BMP - Windows Bitmap
  * GIF - Graphics Interchange Format
  * JPG - Joint Photographic Experts Group
  * PDI - PhotoDemon Image (the program's native format)
  * PNG - Portable Network Graphic
  * PPM - Portable Pixel Map
  * TGA - Truevision Targa
  * TIFF - Tagged Image File Format

## New Feature: Color Temperature Tool

A full discussion of color temperature and how it works is available at [this Wikipedia article](http://en.wikipedia.org/wiki/Color_temperature), but a simple description is: color temperature allows you to retroactively adjust the lighting of a photograph.  It's a powerful way to change the mood of a photo, or to adjust lighting to reflect how you remember a scene - versus what the camera actually caught.

![](images/PhotoDemon_50_Color_Temperature_Tool.jpg)

*The all-new Color Temperature tool.  To my knowledge, no other free photo editor provides a tool like this.*

I'm quite proud of this tool, in part because it took [a ridiculous amount of work](4435/convert-temperature-rgb-algorithm-code/) to build.  Other free photo editors like GIMP and Paint.NET lack anything like this, so short of Photoshop, PhotoDemon is one of the only software programs to provide such a feature.

The image below - a promotional poster for the HBO series _True Blood_ - nicely demonstrates the potential of color temperature adjustments.  On the left is the original shot; on the right, a color temperature adjustment using PhotoDemon.  In one click, a nighttime scene can been recast in daylight.

![](images/True_Blood_Color_Temperature_Demo-600x450.jpg)

*Color temperature adjustment in action.*

## New Feature: Black and White (1-bit) Conversion

PhotoDemon already possesses a [powerful grayscale engine](3643/grayscale-image-algorithm-vb6/), with more conversion options than any other tool on the market.  But what if you want to literally convert an image to black and white - as in _just_ black and _just_ white?

Now you can, thanks to a revamped black-and-white tool.

![](images/PhotoDemon_50_BlackWhite_Tool.jpg)

*The new black-and-white tool, rewritten from scratch for 5.0.*

The new tool operates hand-in-hand with a flexible, powerful dithering engine.  The new engine design allows for any combination of dithering and threshold, and if you'd like, you can also have PhotoDemon estimate an ideal threshold value for a given image.  (An ideal threshold is one that leads to an image that's roughly 50% black and 50% white.)

A comprehensive assortment of dithering algorithms is provided, including: Bayer 4x4 and 8x8, False (fast) Floyd-Steinberg, Genuine Floyd-Steinberg, Jarvis/Judice/Ninke, Stucki, Burkes, Sierra-3, Two-Row Sierra, Sierra Lite, and my personal favorite - [Bill Atkinson's](http://en.wikipedia.org/wiki/Bill_Atkinson) classic Macintosh algorithm, which featured prominently in the original Apple Macintosh.  Images treated with this algorithm evoke a certain nostalgia for anyone old enough to remember that era of computing.

![](images/PhotoDemon_50_Atkinson_Dithering_Warehouse_13.png)

*Atkinson dithering, as applied to a screen capture from a Warehouse 13 episode.*

## New Feature: Tile Tool

Have you ever needed to tile an image?  There are a lot of ways to do it.  Most involve copying-and-pasting an image over and over again, then manually arranging those copies into a grid.

I hate tedious tasks like that.  So PhotoDemon has a new tool that makes tiling a trivial operation.

![](images/PhotoDemon_50_TileTool.jpg)

You can tile according to three rules: the current screen size (automatically detected), a set size in pixels, or a set number of tiles.  The tool will automatically convert between each system for you, and it will let you know the size of the final image in both tiles and pixels.

## Other new features and updates in version 5.0

Other updates in v5.0 include:

  * New "Duplicate Image" tool.  Perfect for making a working copy of an image without fear of overwriting the original. (Thanks to Achmad Junus for the suggestion!)

  * Drag-and-Drop compatibility.  Drag images from your desktop or file manager onto PhotoDemon, and it will open them all automatically. (Thanks to [Kroc of camendesign.com](http://camendesign.com/) for the suggestion!)

  * Auto-Enhance overhaul.  All four auto-enhance tools (contrast, highlights, midtones, shadows) have been rewritten from scratch using completely new algorithms.  I think you'll find them way more useful than the old tools.

  * Improved mosaic tool.  Faster, higher quality, and mosaics can now be as large as the image or as tiny as one pixel in either dimension.

  * Improved handling of edge pixels for all convolution filters (blur, soften, sharpen, etc)

  * Improved manual color reduction algorithms (faster and higher quality)

  * New histogram equalization form.  Equalize any combination of color channels (red, green, blue) and luminance with real-time previews.

  * DPI-aware images mean no more distortion at 120dpi - a big improvement for people using "large font" settings.

  * Fixes for users of the "Classic Theme" in modern versions of Windows.  Your menus should look much better in this release.

  * Improved bug reporting system and online form to match.

  * Tons of miscellaneous bug fixes, tweaks, and optimizations.  For a full list of changes, visit [https://github.com/tannerhelland/PhotoDemon/commits/master](https://github.com/tannerhelland/PhotoDemon/commits/master)

## In Conclusion...

I hope you enjoy the many improvements in version 5.0.  As always, feel free to [contact me](contact) with any feedback you might have.
