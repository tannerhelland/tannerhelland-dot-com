---
author: tanner_h
date: 2014-02-21 16:43:58+00:00
excerpt: The latest version of PhotoDemon includes an overhauled interface, cool new
  tools (like Content-Aware resize), WebP and JPEG-XR support, and so much more.  
layout: post
slug: photodemon-62-beta-live
title: PhotoDemon 6.2 beta live - testers welcome!
redirect_from:
 - /photodemon-62-beta-live
---

**Note: this is an old article!  [PhotoDemon now has its own website at photodemon.org](https://photodemon.org).**

*(Apologies for the dearth of blog posts over the past few months.  The holidays always throw off my schedule, and it takes some time to get things back in order.  I'll try to make more time for articles!)*

![A new version of PhotoDemon includes an overhauled interface, lots of new tools (including cool things like Content-Aware resize), WebP and JPEG-XR support, and so much more.  Get it here.](images/PD_6-2-beta-600x427.jpg)

The latest version of PhotoDemon includes an overhauled interface, cool new tools (like Content-Aware resize), WebP and JPEG-XR support, and so much more.  [Get it here.](https://photodemon.org/681/photodemon-6-2-beta-is-live/)

A new version of PhotoDemon is about ready to release, and anyone who can help give it a final round of testing is most appreciated.  Download the 6.2 beta here:

[https://photodemon.org/download/](https://photodemon.org/download/)

[The announcement article on photodemon.org](https://photodemon.org/681/photodemon-6-2-beta-is-live/) contains a full run-down of all the new features, but let me mirror a few here for the curious:

## Brand-new interface

![PD_6-2-beta](images/PD_6-2-beta.jpg)

The old MDI "floating-window" interface is gone for good.  In its place is a sleek, lightweight tabbed interface.

## Color-Managed Workflow

![Color_Managed_Workflow](images/Color_Managed_Workflow.jpg)

This was a huge project, and an exciting addition for both casual and professional users.  PhotoDemon now provides a fully color-managed workflow across the entire program (including the main viewport, all tool dialogs, and even small things like color selection dialogs).

## New color selector

![PhotoDemon_Color_Selection](images/PhotoDemon_Color_Selection.jpg)

Major improvement over the stock Windows color selection dialog (which hasn't changed in 20 years).  Many thanks to the open-source photo editor GIMP, whose color selector served as the primary inspiration for this one.

## Comprehensive Resize options

![PhotoDemon_Resize_Dialog](images/PhotoDemon_Resize_Dialog1.jpg)

In past versions, PhotoDemon always required you to resize images using pixel values - but no more!  All resize dialogs (Image Resize, Canvas Resize, etc) now support resizing by pixels, percent, or physical units (inches, cm).

## All-new JPEG export dialog

![PhotoDemon_Export_JPEG_Final](images/PhotoDemon_Export_JPEG_Final.jpg)

![PhotoDemon_Export_JPEG_Final_Metadata](images/PhotoDemon_Export_JPEG_Final_Metadata.jpg)

As the most common image format, JPEGs deserve special consideration.  PhotoDemon's new JPEG export dialog provides many new features, including the ability to have the software automatically determine an appropriate quality setting for you.

## WebP and JPEG-XR support (import and export)

I don't know if anyone uses these formats, but they're there if you need 'em!

## New Autosave feature

![PhotoDemon_Autosave_Dialog](images/PhotoDemon_Autosave_Dialog.jpg)

## New Content-Aware Resize tool

![Initial image, courtesy of Wikipedia (http://en.wikipedia.org/wiki/File:Broadway_tower_edit.jpg).](images/Broadway_tower_before.jpg)

*Initial image, courtesy of Wikipedia ([http://en.wikipedia.org/wiki/File:Broadway_tower_edit.jpg](http://en.wikipedia.org/wiki/File:Broadway_tower_edit.jpg)).*

![Image resized using a standard resize algorithm.  Note the undesirable stretching.](images/Broadway_tower_normal_resize.jpg)

*Image resized using a standard resize algorithm.  Note the undesirable stretching.*

![The same image, resized using a content-aware algorithm.  Uninteresting features (like sky and grass) have been shrunk preferentially, leaving the interesting features (person, castle) intact.](images/Broadway_tower_content_aware_resize.jpg)

*The same image, resized using a content-aware algorithm.  Uninteresting features (like sky and grass) have been shrunk preferentially, leaving the interesting features (person, castle) intact.*

Content-aware resize is a cutting-edge technique for resizing images without distorting their contents.  It was recently added to PhotoShop in version CS4, and nearly all free photo editors lack a comparable tool - but not PhotoDemon!

## Improved tool previews

![updated vignetting tool](images/updated-vignetting-tool.jpg)

Tool dialogs now provide an option to toggle between "fit whole image on screen" and "show image at 100%".  When showing the image at 100%, the image can be click-dragged, so even large images can be fully inspected.  Also, the preview tool now supports "click to set a center point" behavior when relevant.

## Asynchronous image metadata handling

Parsing image metadata occupies a huge chunk of the image load process.  To improve performance, metadata handling is now completely asynchronous, meaning it will operate in parallel with the rest of the image loading process.

## Improved Screen Capture tool

![PhotoDemon_Screenshot_Dialog](images/PhotoDemon_Screenshot_Dialog.jpg)

Individual program windows can now be selected from a list, with or without their window decorations (titlebar, borders, etc).

## And lots more...

Check out the [official beta announcement at photodemon.org](http://photodemon.org/681/photodemon-6-2-beta-is-live/) for a full list of updates and improvements.
