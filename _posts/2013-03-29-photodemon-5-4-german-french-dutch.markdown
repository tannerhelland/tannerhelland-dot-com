---
author: tanner_h
date: 2013-03-29 16:18:28+00:00
excerpt: PhotoDemon 5.4 is complete.  New features include language support (German, French, and Dutch), a full-featured batch processing wizard, shadow/highlight correction, nine new distort tools, vignetting, median noise removal, JPEG and PNG optimization, and more.
layout: post
slug: photodemon-5-4-german-french-dutch
title: PhotoDemon 5.4 is live - now with German, French, and Dutch language support
redirect_from:
 - /4893/photodemon-5-4-german-french-dutch
 - /4893/photodemon-5-4-german-french-dutch/
---

**Note: this is an old article!  [PhotoDemon now has its own website at photodemon.org](https://photodemon.org).**

## Summary

**PhotoDemon 5.4 is complete.  [Download it here](https://photodemon.org/download/).**

New features include language support (German, French, and Dutch), a full-featured batch processing wizard, shadow/highlight correction, nine new distort tools, vignetting, median noise removal, JPEG and PNG optimization, and more.  

![Kaleidoscope is probably the least practical (but most fun!) new tool in 5.4.  :)](images/Kaleidoscope-600x343.jpg)

*Kaleidoscope is probably the least practical (but most fun!) new tool in 5.4.  Also, German!*

## Highlight feature: support for multiple languages!

This is the biggest addition in version 5.4, and I can only claim partial credit for it.  Primary credit goes to Frank Donckers, a fellow VB programmer who prototyped the initial translation engine for me.  As if that isn't incredible enough, Frank also supplied the translations for French, German, and Dutch (Flemish), so I owe him an enormous debt of gratitude.  Thank you, Frank!

One of the neatest aspects of this feature is the ability to change the language at run-time via the Language menu.  Unlike every program I have ever used, _no restart is required_.  PhotoDemon will dynamically change the program's entire language immediately, and if you change your mind, you can switch to any other language at any time.

I hope these three languages are only the beginning.  

**If you speak a language other than English, please consider contributing a new PhotoDemon translation!  No programming knowledge is required, and you will receive full credit for your work.**  [Contact me for more details.](contact)

## Nine new Distort-style tools

Add and remove lens distortion. Swirl. Ripple. Pinch and whirl. Waves. Kaleidoscope. Polar conversion (both directions). Figured glass (dents).

![The new Ripple tool.  All distort tools use resampling for improved image quality, and all provide real-time previews.](images/Ripple-600x342.jpg)

*The new Ripple tool.  All distort tools use resampling for improved image quality, and all provide real-time previews.*

![The new Figured Glass tool uses Perlin Noise to provide a warped glass look to images.](images/Figured_glass-600x343.jpg)

*The new Figured Glass tool uses Perlin Noise to provide a warped glass look to images.  (Note: the source image is a promotional photo for ABC's [Once Upon a Time](http://en.wikipedia.org/wiki/Once_Upon_a_Time_%28TV_series%29).)*

## Vastly improved file format support

![The new JPEG export dialog.  Optimization is a lossless way to reduce file size - very handy for JPEGs headed to the web.](images/JPEG_export.jpg)

*The new JPEG export dialog.  Optimization is a lossless way to reduce file size - very handy for JPEGs headed to the web.*

JPEGs now support automatic EXIF rotation on import, and a variety of options on export (Huffman table optimization, progressive scan, thumbnail embedding, specific subsampling). TIFFs support CMYK encoding and a number of compression schemes (none, PackBits, LZW, CCITT 3 and 4, zLib, and more). PNG exporting supports variable compression strength, interlacing, and background color chunk preservation.  PPMs can be exported with RAW or ASCII encoding. BMP and TGA files now support RLE encoding. And for icons, animated GIFs, and multipage TIFFs, all images inside a file can now be loaded (instead of just the first one).

These format settings can be accessed from the Tools -> Options menu, and the new Batch Process tool also provides direct access.

## Revamped standard tools, including Box Blur, Gaussian Blur, Smart Blur, and Unsharp Masking.

![Smart blur can be used to smooth out specific features, like skin, while leaving edges and fine details intact.  (Image of the lovely and talented Rashida Jones, via Glamour)](images/Smart_blur-600x344.jpg)

*Smart blur can be used to smooth out specific features, like skin, while leaving edges and fine details intact.  (Image of the lovely and talented [Rashida Jones](http://en.wikipedia.org/wiki/Rashida_Jones), [via Glamour](http://www.glamour.com/beauty/blogs/girls-in-the-beauty-department/2011/11/6-beauty-tips-to-steal-from-ra.html))*

PhotoDemon is now a much better photo editor, thanks to the revamp of its core convolution filters.  Larger tool dialogs make it easier to see the result of your actions.  Better performance means real-time previews, even at enormous radii (up to 200px for all filters, plus 500px for box blur!).  And all convolution algorithms now use specialized edge handling code to make sure every part of the image - from center to border - is handled correctly.

Also, the program's Gaussian Blur is now a _true_ gaussian blur.  There are no shortcuts, no estimations, and it's still fast enough to preview in real-time.

## New advanced color tools, including Shadow/Midtone/Highlight adjustments, color balancing, and monochrome-to-grayscale recovery

![Shadow / Midtone / Highlight correction allows for detailed recovery of light and dark parts of an image.  Thanks to deviantart user deviantsnark for the sample image.](images/Shadow_midtone_highlight-600x340.jpg)

Shadow / Midtone / Highlight correction allows for detailed recovery of light and dark sections of an image.  Thanks to [dA user deviantsnark for the Borderlands wallpaper.

![Color balance provides a per-color way to adjust the hue of an image (versus hue / saturation adjustments, which apply equally to all colors).  Thanks to dA user LadyGT for the beautiful artwork.](images/Color_balance-600x343.jpg)

Color balance provides a per-color way to adjust the hue of an image (versus hue / saturation adjustments, which apply equally to all colors).  Thanks to [dA user LadyGT for the beautiful Tomb Raider artwork](http://ladygt.deviantart.com/art/Tomb-Raider-Reborn-Contest-357986979?q=gallery%3Aladygt%2F393688&qo=0).

## New stylize tools, including Film Grain, Vignetting, Modern Art, Trace Contour, Film Noir, and Comic Book

![Vignetting refers to the rounded halo around the edges of the image.  The new tool allows you to add halos of any size, softness (how blurry the edges are), transparency, and color, and it can automatically fit the effect to any aspect ratio.  Thanks to dA user chrismickens for the great Mad Men artwork.](images/Vignetting-600x343.jpg)

Vignetting refers to the rounded halo around the edges of the image.  The new tool allows you to add halos of any size, softness (how blurry the edges are), transparency, and color, and it can automatically fit the effect to any aspect ratio.  Thanks to [dA user chrismickens for the great Mad Men artwork](http://browse.deviantart.com/art/Mad-Men-s-Sexy-Joan-Holloway-131741607).

![PhotoDemon now allows you to add artificial film grain to any image.  This effect was famously used in the Mass Effect trilogy of games to create a more gritty, realistic look.](images/Film_grain-600x342.jpg)

PhotoDemon now allows you to add artificial film grain to any image.  This effect was famously used in the Mass Effect trilogy to create a more gritty, realistic look.

![Contour tracing uses a stack of unique algorithms to "paint" the edges of an image.  It is also a useful edge detection tool.](images/Trace_contour-600x344.jpg)

Contour tracing uses a unique stack of algorithms to "paint" the main features of an image.  It is also a useful edge detection tool.

## Noise removal via Median Filtering

![Median filtering serves two main purposes: removal of image noise (unwanted pixel variance), and recovery of damaged images.  The severely damaged image above is courtesy Wikipedia; the after image is pure PhotoDemon (note that it recovers better than the Wikipedia example!).](images/Median_filter-600x344.jpg)

Median filtering serves two main purposes: removal of image noise (unwanted pixel variance), and recovery of damaged images.  The severely damaged image above is [courtesy Wikipedia](http://en.wikipedia.org/wiki/Median_filter); the after image is PhotoDemon's correction (note that it recovers more than the Wikipedia example!)

## Automatic image cropping

![If an image has empty space around the edges - like this Firefox wallpaper - Autocrop can automatically crop it for you.  The feature supports thresholding, so it works equally well on lossy formats like JPEG.](images/Autocrop-600x203.jpg)

If an image has empty space around the edges - like this Firefox wallpaper - Autocrop can automatically remove it for you.  Autocrop supports thresholding, so it works just fine on JPEGs.

## New Batch Process Wizard

If I had to pick a personal "favorite" new feature in this release, it would be the brand-new batch processing wizard.  This tool is a highlight of PhotoDemon's emphasis on usability, and I researched more than a dozen other image batch processing tools while building it.  I could be biased, but I believe PhotoDemon is now the best general-purpose image batch processor available on the web.

![The first page of the new Batch Process wizard.  This step is by far the most intricate, and a ton of work went into exposing full functionality without overwhelming the user.  To my knowledge, PhotoDemon is the only batch processor that allows you to create your own batch list from any number of source directories spread across any number of drives.](images/Batch_process_page_1-600x368.jpg)

The first page of the new Batch Process wizard.  This step is by far the most intricate, and a ton of work went into exposing full functionality without overwhelming the user.  To my knowledge, PhotoDemon is the only batch processor that allows you to create your own batch list from any number of source directories spread across any number of drives.

Drag-and-drop is now supported when building the list of images to be processed - not only from within the dialog, by dragging between list boxes, but also from Windows Explorer.  Live previews make it much easier to find the images you want, while helpful instructions on the left-hand side expose some of the more nuanced functionality.

![Once a list of images has been created, you can optionally choose to apply photo editing actions to each image.  Unlike other batch processors, PhotoDemon allows you to use any photo editing actions provided by the program.](images/Batch_process_page_2-600x368.jpg)

Once a list of images has been created, you can optionally choose to apply photo editing actions to each image.  Unlike other batch processors, PhotoDemon allows you to use **any photo editing actions** provided by the program - not just a tiny subset.

Page 2 is the barest page of the new wizard.  The current version allows you to skip photo editing actions (if you want to just do a batch rename or format conversion, for example), or you can apply any recorded macro.  In the next release, I will add a set of "one-click" presets for common actions, like resizing, or optimizing images for the web.

![Once you've created a list of images and chosen any photo editing actions, an output image format can be set.  New to this version, PhotoDemon can retain original image formats - allowing you to apply actions to mixed PNG/JPEG collections, for example.  Alternatively, you can select a single output format, with access to the program's full range of detailed format settings.](images/Batch_process_page_3-600x368.jpg)

Once you've created a list of images and chosen any photo editing actions, an output image format can be set.  New to this version, PhotoDemon can retain original image formats - allowing you to apply actions to mixed PNG/JPEG collections, for example.

Page 3 asks you to choose an output format.  If you want to retain original image formats, that's cool too - PhotoDemon now supports this!    Alternatively, you can select a single output format, with access to the program's full range of detailed format settings.  In the example above, you can see all the options available for JPEGs, including new support for optimization (lossless file size reduction), thumbnails, progressive encoding, and specific subsampling.

![The last step of the wizard asks you to choose a location to save all the processed files.  If desired, a number of rename options are also available.](images/Batch_process_page_4-600x368.jpg)

The last step of the wizard asks you to choose a location to save all the processed files.  If desired, a number of rename options are also available.

The final page asks you to select an output folder where PhotoDemon can save the processed images.  New to this release is a wide range of renaming options - things like adding custom text to each filename, removing text from each filename, changing case, and replacing spaces with underscores for web-bound images.  Additionally, original filenames can be retained, or PhotoDemon can just use ascending numbers.

So that's the new batch wizard!  I'd love feedback from power users, as there are a lot of moving parts to the batch tool, and while I have been very thorough in my own testing, it's impossible to test every combination of variables.  So if you find anything that doesn't work, please let me know.

## Improved features: Gamma Correction, Dilate, Erode, Monochrome Conversion, Histogram and Printing

As is usual with each PhotoDemon update, a number of existing tools received redesigns or new features.  Gamma correction now displays live gamma curves, and each color component (red, green, and blue) can be adjusted individually.  Dilate and Erode use a new algorithm that's significantly more optimized, meaning sizes up to 200px radius can be previewed in real-time.  Monochrome conversion supports any two color (not just black and white), while the printing and histogram dialogs were completely overhauled to make them more user-friendly.

![The new gamma correction dialog.  The old dialog forced users to correct only one channel at a time.  The new one allows for correcting all three, with a live preview of the new curves.  Thanks to dA user Kouken for the Persona fan art.](images/Gamma-600x343.jpg)

The new gamma correction dialog.  The old dialog forced users to correct only one channel at a time.  The new one allows for correcting all three, with a live preview of the new curves.  Thanks to [dA user Kouken for the Persona fan art](http://kouken.deviantart.com/art/Persona-3-and-4-Bookmark-Set-173075422).

## Universal color depth support at import and export time

PhotoDemon can now write 1, 4, 8, 24, and 32bpp variations of every supported file format.  By default, when saving images, color depth detection is completely automated – the program will count the number of colors in an image and automatically select the most appropriate color depth for the output file. Alternatively, you can set a preference to manually specify color depth at save time.  This also works for grayscale images; for example, the JPEG encoder will now detect grayscale images and write out 8bpp JPEGs accordingly.  Alpha thresholding is also available when saving 32bpp images to 8bpp (e.g. PNG to GIF).

![When saving a 32bpp image with a complex alpha channel to a simple format like GIF, the program has to reduce the alpha channel to binary values.  A new threshold dialog helps you find the perfect value.](images/Alpha_thresholding-452x600.jpg)

When saving a 32bpp image with a complex alpha channel to a simple format like GIF, the program has to reduce the alpha channel to binary values.  A new threshold dialog helps you find the perfect value.

This feature was a nightmare to implement, as PhotoDemon supports a huge variety of file formats, and each one has a detailed list of color depths it does or does not support.  Full support for transparency adds a whole other layer of complexity.  But now that the feature is completely implemented and rigorously tested, I can't imagine it any other way.  Color depth is not something users should have to worry about, and automatic handling should be a feature of every photo editor (rather than pestering you for color depth every time you save... *cough* [GIMP](http://www.gimp.org/) *cough*).

## New feature: pngnq-s9 plugin for optimizing PNG files

At the request of [a good friend](http://camendesign.com/), PhotoDemon now provides integrated support for the [pngnq-s9](http://sourceforge.net/projects/pngnqs9/) variety of the famous [pngnq](http://pngnq.sourceforge.net/) library.  For the uninitiated, pngnq provides a way to reduce 32bpp PNG files to 8bpp while still preserving complex alpha channels, allowing for file size reductions of up to 75%.  Pngnq provides superior results over other tools by using a neural network to reduce image colors, unlike the brute-force median cut algorithm used by software like pngquant.  [See here for a gallery of sample images](http://pngnq.sourceforge.net/pngnqsamples.html) if you're curious.

Pngnq-s9 is a further improvement over stock pngnq, including cool features like YUV color space matching for better results, and the ability to preserve alpha values of 0 and 255.  When saving 32bpp PNG files to 8bpp, PhotoDemon will now lean on pngnq-s9 to do the heavy lifting.  

In the next version of PhotoDemon, pngnq-s9 support will be integrated into the batch process wizard as a new "optimize for web" option.  For now, if you want to test out the feature, head to Tools -> Options -> Saving, and change the "set outgoing color depth" option to "ask me what color depth I want to use".  Then save a 32bpp PNG image to 8bpp and compare the file size.

## New plugin manager and plugin downloader

Sometimes it makes sense for PhotoDemon to use an existing open-source project instead of me writing a new feature from scratch.  These support libraries are included as "plugins", and there are four of them in current version.  Each one provides indispensable features (like scanner support) at a fraction of the cost involved to write such a feature from scratch.

Some of these plugins expose additional functionality, but it has always been a challenge for PhotoDemon to expose these additional features to the user.  So the program now has a detailed plugin manager, where advanced users can change settings on a per-plugin basis, including activating or deactivating plugins as necessary.  The manager also tracks availability and version numbers of each plugin.

![It is now much, much easier for the program to keep its plugins up-to-date.  Advanced users may also find it useful to enable or disable plugins while testing various features.  All changes happen in real-time - no restart required.](images/Plugin_manager-600x362.jpg)

It is now much, much easier for the program to keep its plugins up-to-date.  Advanced users may also find it useful to enable or disable plugins while testing various features.  All changes happen in real-time - no restart required.

![The pngnq-s9 page of the plugin manager.  Advanced or esoteric plugin features can be adjusted here, which keeps the program's main preferences dialog uncluttered.](images/Plugin_manager_pngnq-600x362.jpg)

*The pngnq-s9 page of the plugin manager.  Advanced or esoteric plugin features can be adjusted here, which helps keep the main "Options" dialog uncluttered.*

## Many canvas and interface improvements

Larger effect and tool previews. Persistent zoom-in/zoom-out buttons. Image URLs and files can now be directly pasted as new images. Improved drag/drop support, including drag/drop from common dialogs. New “Safe” save behavior to avoid overwriting original files. New Close All Images menu. New algorithms for auto-zoom when images are loaded, meaning much better results at all screen sizes. Tool and file panels can now be hidden. Higher-quality dynamic icons for the program, taskbar, child windows, and Recent Images list. Improved support for low screen resolutions.

## Program-wide performance improvements

More aggressive memory management means lower resource usage. Program loading has been heavily streamlined, and now happens in less than a second on modern hardware. Image loading is much faster and more robust, including better support for damaged or incomplete image files.

## More robust and comprehensive error handling

When loading multiple images, the program will now suppress warnings and failures (such as invalid files) until all images have been loaded. Many subclassing issues have been resolved – so no more surprise crashes!  Overall this release should be extremely stable.

## Many miscellaneous bug fixes and improvements

This article is already way too long, so I won't bore you with a list of all the minor fixes and improvements.  For a full list, see the commit log at [https://github.com/tannerhelland/PhotoDemon/commits/master](https://github.com/tannerhelland/PhotoDemon/commits/master)

## In Conclusion...

This release was a lot bigger than I'd like future releases to be.  The biggest delay came from adding language support, as that affected every piece of text in every part of the program (nearly 10,000 words in total!).  Now that language support is complete, I foresee future releases being much tidier and quicker.

A developer's work is never done, and a roadmap for version 5.6 is already being worked on.  Some features that didn't make the cut for 5.4 - like improvements to the selection tool, or a "smart resize" option - were cut at the last minute, and they will be among the first features added to 5.6.  The batch process wizard will see a number of additions, and I'd love to add some advanced multilanguage features, like a way for casual users to fix or adjust translations on-the-fly.  I also think I'm finally ready to tackle the monumental task of writing a user manual... should be fun!

As always, the best way to stay abreast of PhotoDemon development is the official code repository at [https://github.com/tannerhelland/PhotoDemon](https://github.com/tannerhelland/PhotoDemon)

But for now, I hope you enjoy all the new features in 5.4, and **[please remember to donate if you find the software useful](http://www.tannerhelland.com/donate/)**.
