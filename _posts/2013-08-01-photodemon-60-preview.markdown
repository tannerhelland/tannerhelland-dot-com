---
author: tanner_h
date: 2013-08-01 16:15:04+00:00
excerpt: The next version of PhotoDemon is getting better and better, and while it's not quite ready for an official beta release, I thought it would be fun to share some of its big new features, including Italian language support, state-of-the-art Selection tools, metadata (EXIF) support, a new curves tool, photograph perspective correction, digital Wratten filters, and much more...
layout: post
slug: photodemon-60-preview
title: PhotoDemon 6.0 preview and progress report
redirect_from:
 - /4996/photodemon-60-preview
 - /4996/photodemon-60-preview/
---

**Note: this is an old article!  [PhotoDemon now has its own website at photodemon.org](https://photodemon.org).**

![PhotoDemon's new splash screen.  I'd say this is a "huge" improvement over the old one, but that might be understating it... :)](images/2013_splash_2-600x424.jpg)

*PhotoDemon's new splash screen.  I'd say this is a "huge" improvement over the old one, but that might be understating it...*

## overview

It's been awhile since I posted any news on PhotoDemon, but not because work has slowed - just the opposite, in fact!  The development version of PD is cranking ahead full-steam, and thanks to a number of outside contributors, the next version will include a wider set of improvements than any previous version.  There's still quite a bit of testing and fine-tuning to do, so this article does not include a downloadable beta release - rather, the article is meant to serve as a preview of the upcoming 6.0 release and all the cool new features it provides.  (Of course, developers or anyone with access to Visual Basic 6.0 can compile the latest version themselves by [visiting PhotoDemon's GitHub page](https://github.com/tannerhelland/PhotoDemon).  New testers and contributors are always welcome!)

First, an explanation on why the next PhotoDemon release will be version 6.0 instead of the expected 5.6.  The next release will break backward compatibility with a number of PhotoDemon files, including any saved macros or filters.  This break is necessary to implement a large overhaul of PhotoDemon's internals - an overhaul that makes the program faster, smaller, more stable, and much easier to develop and maintain.  The goal is to have all of PhotoDemon's specialized file formats (including macros) use XML for storage.  This allows both users and other software developers to read and edit PhotoDemon files from any general-purpose text editor.  This change will also make it much easier to add new macro features without breaking old macro files.  (The current macro format was developed over a decade ago, when the program was only meant for personal use, and it is extremely flimsy and difficult to extend - hence the need for a redesign.)

The downside of this change is that any current macros will need to be re-recorded in version 6.0, as version 4.X and 5.X macros will no longer be supported.  I apologize for this inconvenience, and I promise to do my best to avoid breaking backward compatibility in the future.

The 6.0 release will also include important interface changes - such as a redesigned main menu and tool window - further supporting the switch to a new major version number, and for developers, the program's central action processor has been redesigned from the ground up, making it easier than ever to get involved in development.

So with that out of the way, let's talk about the good stuff, namely: what's coming in 6.0?  Here is a list of features and updates that are already finished and available in the current development build (again, downloadable at [https://github.com/tannerhelland/PhotoDemon](https://github.com/tannerhelland/PhotoDemon)).

## Italian language support

Courtesy of talented contributor GioRock is a new Italian language option for PhotoDemon.  Many thanks to GioRock for this huge contribution.

## Other internationalization improvements

With the help of GioRock and Frank Donckers (you may remember Frank as the developer behind PhotoDemon's language translation engine), a number of other improvements are now available for international PhotoDemon users:

  * The comma "," is now supported as a decimal separator in all tools.  Previously, use of a comma could lead to errors.
  * Translated text is now automatically resized if it is larger than its tool window.  This helps text in verbose languages remain fully readable.
  * Translations that span multiple lines (such as long tooltips) are now automatically handled by the program.  This reduces the burden on translators to manually fit translated text longer than its English equivalent.

![Here is the Options panel in full Italian.  The text of the bottom checkbox on the right-hand panel originally extended past the edge of the dialog, but PhotoDemon has detected that and shrunk the text accordingly.  This requires no work on the part of the translator!](images/PhotoDemon_Italian_Translation-600x423.jpg)

Here is the Options panel in full Italian.  The text of the two checkboxes on the right-hand panel originally extended past the edge of the dialog, but PhotoDemon has detected that and shrunk the text accordingly.  (This required no work on the part of the translator!)

## New feature: advanced selection tools

![The new elliptical selection tool, with live feathering (feathering is the softened selection edges).](images/PhotoDemon_Selection_Overview-600x356.jpg)

*The new elliptical selection tool, with live edge feathering.*

PhotoDemon 6.0 includes a completely redesigned selection tool engine.  At present, the following dedicated selection tools are available:

  * Rectangular and Square selections (with optional rounded corners, including variable corner radii)
  * Elliptical and Circular selections
  * Line selections: unique to PhotoDemon, this tool allows you to select a line-shaped area, very helpful for things like [tilt-shift effects](http://en.wikipedia.org/wiki/Tilt-shift) (see below)

![PhotoDemon's line selection tool was combined with Gaussian Blur to simulate this fake miniature photograph of the city of Jodhpur.  (Photograph and concept taken from this Wikipedia article.)](images/City-fake-miniature-600x400.jpg)

*PhotoDemon's line selection tool was combined with Gaussian Blur to simulate this fake miniature photograph of the city of Jodhpur.  (Photograph and concept taken from [this Wikipedia article](http://en.wikipedia.org/wiki/Miniature_faking).)*

Each selection tool supports the following features:

  * Live selection coordinate and size display
  * On-canvas resizing by click-dragging nodes
  * Selections can be nudged or moved via text entry
  * Shift can be held to lock a 1:1 aspect ratio (e.g. squares or circles)
  * Live smoothing options: none, antialiased, or variable radius feathering (live feathering is only available on Windows 7)
  * Live selection types: interior, exterior, or bordered, with live border radius selection

In addition to these dedicated tools, a new Selection menu is available with additional selection-related features.

![PhotoDemon's new Select menu](images/PhotoDemon_Selection_Menu.jpg)
  
  * Select All and Select None
  * Invert Selection (switch selected and un-selected pixels, with full feathering support!)
  * Grow/Shrink Selection
  * Border selection, which takes the current selection and selects only its border
  * Feather and sharpen selection
  * Load and save selections

Thanks to the selection engine redesign, these features will automatically work with future selection tool implementations, including polygon/free-draw and "magic wand" selections.

Another huge improvement is integrating all selection actions into the Undo/Redo engine.  If you create, move, resize, or apply any other action to a selection, you can now Undo/Redo that operation. 

Selections are now fully integrated into the Record Macro tool.  

Copy and Crop now support selections of any shape, making it trivial to crop circular or rounded-rectangle regions, or copy them for use in another program.  (Feathered selections are automatically converted to 32bpp images, with the feathering applied in the alpha channel.)

Finally, the core Selection tools have been rewritten to use vector coordinates.  This means that selections loaded from file are automatically resized to fit the current image, making them extremely useful for Batch Processing operations.

## New image metadata (EXIF, XMP, IPTC) support

PhotoDemon now includes the marvelous [ExifTool project](http://www.sno.phy.queensu.ca/~phil/exiftool/) as an optional plugin.  ExifTool is the most comprehensive image metadata handler currently available, and PhotoDemon makes full use of its ability to handle every known type of image metadata, from the popular EXIF format (used in JPEGs) to obscure maker notes for all major DSLR brands.

![PhotoDemon's new custom-built Image Metadata browser.  This image is a RAW-format file from an Olympus DSLR.  ExifTool allows us to peruse all the custom Olympus data entries.](images/PhotoDemon_Metadata_Browser-600x374.jpg)

*PhotoDemon's new custom-built Image Metadata browser.  The metadata in question comes from a RAW-format photo taken with an Olympus DSLR camera.  Note that ExifTool allows us to peruse all the non-standard Olympus data entries.*

A new integrated metadata browser automatically sorts metadata by category, and it allows the user to see actual or human-friendly metadata tags.  The browser fully integrates with ExifTool's multilanguage capabilities, sparing translators from any extra work!

When saving images, the Preferences manager now provides options for metadata embedding:

![PhotoDemon's new metadata handling preferences.](images/PhotoDemon_Metadata_Preferences-600x423.jpg)

Unique to PhotoDemon is a privacy-centric metadata option, which aims to remove any personally identifying metadata entries, like serial numbers or GPS coordinates.  By default, the "preserve all relevant metadata" option is recommended, which will remove any metadata not relevant to a file format (such as removing maker notes when saving RAW files to JPEG), but retain all other metadata entries.  Metadata can also be fully stripped from exported files.

Also fun is a new Image -> Metadata -> Map GPS Coordinates option, which becomes available if an image contains GPS data.  This option will automatically map the photo's location in Google Maps.

## New tools: too many to mention!

As always, the next release will include a host of new image editing tools.  Here's a small sampling of the latest additions to PhotoDemon's repertoire:

![PhotoDemon's new interactive perspective correction tool.  Drag the corner nodes to re-visualize the image in real-time, allowing you to do things like fix crooked buildings, as in this photograph from a recent trip to San Francisco.](images/PhotoDemon_Photograph_Perspective_Correction-600x395.jpg)

PhotoDemon's new interactive perspective correction tool.  Drag the corner nodes to re-visualize the image in real-time, allowing you to do things like fix crooked buildings, as in this photograph from a recent trip to San Francisco.

![PhotoDemon's new Photo Filter browser.  To my knowledge, this is the most comprehensive collection of post-production Wratten filters in any software, ever.  The interactive photo filter browser provides 50 custom-built photo filters for fixing every possible lighting situation.](images/PhotoDemon_WrattenFilters-600x282.jpg)

PhotoDemon's new Photo Filter browser.  To my knowledge, this is the most comprehensive collection of digital Wratten filters in any software, ever.  The interactive photo filter browser provides 50 filters, allowing you to make an infinite number of post-production lighting adjustments.

![PhotoDemon's new Curves tool.  It supports unlimited curve points, a live histogram overlay, removal of points by right-clicking them, and fully antialiased curve rendering.  In my opinion, this is the loveliest tool in the program, and the loveliest Curves dialog of any mainstream photo editor.](images/PhotoDemon_Curves_Tool-600x392.jpg)

PhotoDemon's new Curves tool.  It supports unlimited nodes, removing nodes by right-clicking, a live histogram overlay, and fully antialiased curve rendering.  In my opinion, this is the loveliest tool in the program, and the loveliest Curves dialog of any mainstream photo editor.

![PhotoDemon's new Channel Mixer.  This tool comes courtesy of outside contributer audioglider, who contributes multiple tools to this release - please shower him with praise!  (The subject of this photo is the latest addition to my family, a beautiful Australian Shepherd / Shetland Sheepdog mix named Yosuke.)](images/PhotoDemon_Channel_Mixer-600x343.jpg)

PhotoDemon's new Channel Mixer.

![PhotoDemon finally includes a Canvas Resize tool.](images/PhotoDemon_Canvas_Resize.jpg)

PhotoDemon finally includes a Canvas Resize tool.

![PhotoDemon's new Sphere tool lies more in the "Fun" category than the "Practical" one, but that's okay.  For a bit of extra style, the program can render matching background rays onto the canvas, as shown in the screenshot above.](images/PhotoDemon_Spherize-600x342.jpg)

PhotoDemon's new Sphere tool lies more in the "Fun" category than the "Practical" one, but that's okay.  For a bit of extra style, the program can render matching background rays onto the canvas, as shown in the screenshot above.

For sake of brevity, I'll forgo images of the rest of the new tools, namely:

  * Max/min channel
  * Pan and zoom
  * Poke
  * Shear
  * Squish
  * Vibrance 

## Other improvements and additions for end-users

![PhotoDemon's batch wizard now includes dedicated options for common batch operations, such as resizing.  The wizard has also been further streamlined to make batch processing as easy and quick as possible.](images/PhotoDemon_Batch_Wizard_60-600x368.jpg)

PhotoDemon's batch wizard now includes dedicated options for common batch operations, such as resizing.  The wizard has also been further streamlined to make batch processing as easy and quick as possible.

![The Resize Tool has undergone a significant redesign.  Resampling options are now human-friendly, and several how-to-fit options are now provided when changing an image's aspect ratio.  This makes it possible to resize images to a new aspect ratio without unsightly distortion.](images/PhotoDemon_New_Resize_tool.jpg)

The Resize Tool has undergone a significant redesign.  Resampling options are now human-friendly, and several how-to-fit options are now provided when changing an image's aspect ratio.  This makes it possible to resize images to a new aspect ratio without unsightly distortion.

![When flattening an image with transparency (alpha channel), you can now select a background color.  Previously the software always defaulted to white.](images/PhotoDemon_Remove_Alpha_Channel-600x350.jpg)

When flattening an image with transparency (alpha channel), you can now select a background color.  Previously the software always defaulted to white.

  * Transparent images can now be copied/pasted between PhotoDemon and other software.  This means you can take an image with multiple layers in GIMP and paste it into PhotoDemon fully composited.
  * Official RAW image format support; more than 20 RAW filetypes are now supported.
  * 30-40% speed improvements to Gaussian Blur, Smart Blur, and Unsharp Masking thanks to an Integer-only rewrite of the blur engine.
  * Filters and other long-running actions can now be canceled mid-action by pressing ESC.
  * Revamped main window interface, as you can see in the screens above.  The left-hand toolbar is now images-only, while the right-hand one has been expanded.
  * Better validation for all text controls.  Invalid entries are automatically circled in red.
  * Alt+T will now let you switch between preview and non-preview modes in all tools.
  * Many miscellaneous bug fixes, optimizations, and other improvements.  For a full list, see the commit log at [https://github.com/tannerhelland/PhotoDemon/commits/master](https://github.com/tannerhelland/PhotoDemon/commits/master)

## Improvements and additions for developers and contributors

  * PhotoDemon can now provide timing reports for all actions passed through the central software processor.  Simply enable the DISPLAY_TIMINGS constant when compiling.
  * New custom slider/text and up/down controls make it easy to utilize PD's existing validation and translation abilities in your own tool dialogs.
  * A new string-based filter parameter class makes it easy to tie complex tools with many parameters into the software processor (and thus into recorded macros).  No longer do you have to convert param lists to complex custom Variant embeddings.
  * PhotoDemon now includes a high-performance font rendering class, which makes custom font rendering (with AA) much easier to implement.
  * Dev builds, including build number, are now automatically detected by the program, making it easy to see which build you're currently working with.
  * Support tools, including the custom plugin compressor and master translation file generator, are now synched to GitHub in the /Support subfolder.
  * A public histogram-generation routine is now available, so you can tap into PhotoDemon's highly optimized histogram generator for any of your own tools.

## Contributors, developers, and translators still welcome!

As always, PhotoDemon can never have enough external contributors, developers, and translators.  If you can help with any aspect of the 6.0 release, don't hesitate to [get in touch](contact/).  Many features in the 6.0 release wouldn't be possible without outside help, and I'd love to add you to the ever-growing list of talented contributors who make PhotoDemon possible!

If you can't contribute with coding or translations, [donations are another great way to help](donate/).  Thanks in advance for your small monetary contribution to this completely open-source project, which provides a full-featured photo editor (comprising 60,000 lines of code and more than 50,000 words of translated text in five languages) completely free of charge.
