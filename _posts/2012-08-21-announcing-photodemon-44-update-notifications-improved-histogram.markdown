---
author: tanner_h
date: 2012-08-21 17:11:28+00:00
excerpt: PhotoDemon version 4.4 is now available.  Updates in this version include an all-new automatic update notifier.  Helpful Undo/Redo text that describes what you are about to Undo/Redo.  A redesigned histogram, including per-channel rendering, logarithmic histograms, a new interface, and no more modal-window locking.  A new grayscale conversion interface, including two new algorithms and real-time previews.  And the usual batch of bugfixes and optimizations.
layout: post
slug: announcing-photodemon-44-update-notifications-improved-histogram
title: Announcing PhotoDemon 4.4 - Now With Update Notifications, Improved Histogram,
  and More
redirect_from:
 - /4310/announcing-photodemon-44-update-notifications-improved-histogram
---

**Note: this is an old article!  [PhotoDemon now has its own website at photodemon.org](https://photodemon.org).**

## Summary

PhotoDemon v4.4 is now available. It has a lot of cool new features. [Download it here](https://photodemon.org/download/).

## New Feature: Update Notifications

The most important update in version 4.4 is the addition of an automatic update notifier.

![PhotoDemon's new update notifier](images/UpdateNotifier_solo.jpg)

By default, PhotoDemon will check for updates whenever the software is run. Automatic update checks can be disabled from the Edit -> Preferences menu. You can also manually check for updates by going to Help -> Check for Updates.

I'm not sold on the layout of the update notification form - particularly the center alignment of the version numbers, which looks off due to the white space on the right-hand side - so its appearance may change in future versions, but at least this first draft conveys all the essential information.

Finally, note that this is merely an update **notifier**, not an automatic updater - clicking the "Yes" button will only open the PhotoDemon download page in your browser. It will not download the update for you, and it will not overwrite your current copy of the software. This is my preferred behavior for portable applications, but I am open to suggestions for better methods.

## New Feature: Helpful Undo/Redo Text

The left-hand bar in v4.4 has been redesigned from version 4.3:

![Comparison of v4.3 and v4.4 left-hand bar](images/side-bar-4-3-vs-4-4.jpg)

v4.3 is on the left, v4.4 is on the right

The new, more compact version is in preparation for adding additional tools to the bottom section of the left-hand bar. It was also done as part of the new "friendly text" version of the Undo/Redo buttons:

![new Undo/Redo interface](images/undo-redo-with-new-text-display.jpg)

I tried displaying the full text of the Undo/Redo action in the Undo/Redo buttons themselves, but as some of the descriptions are rather long, the button text would get pushed onto multiple lines (or off the button entirely!) making them look terrible. So the current implementation is: **hover** over the Undo/Redo button to see what action will be performed. As you can see, the Edit menu also contains a full-text description of Undo/Redo behavior.

## Redesigned Histogram

With version 4.4, I don't think it's biased to say that PhotoDemon provides the best image histogram tool in the business:

![PhotoDemon 4.4's redesigned histogram](images/new_histogram_interface.jpg)

Individual channels can now be hidden or displayed in any combination. (The histogram will automatically adjust its maximum and minimum values accordingly.) This is useful for comparing just two color channels, for example, or comparing a single color channel against luminance.

The histogram now provides a "use smooth lines" option. This enables two features: antialiased lines (which VB does not do natively, so it's a custom implementation), and cubic spline interpolation. Here's an example of the aesthetic difference this makes:

![Comparison of histogram render methods](images/histogram_smooth_comparison.jpg)

The new histogram interface provides a logarithmic rendering option. Images that are very dark or very bright will blow out the histogram at one end or the other, making it very difficult to see what's happening in those ranges. Take the histogram of [this FF7 fan art from pixiv.net user マップ](http://www.pixiv.net/member_illust.php?mode=medium&illust_id=21635864), for example:

![Image in need of a logarithmic histogram](images/histogram-needing-logarithmic-values.jpg)

![Logarithmic histogram in action](images/logarithmic-histogram-in-action.jpg)

Classic features like displaying the values of the histogram level under the cursor are still present, and you can still export the histogram image to an 8-bit PNG, GIF, or BMP file.

Finally, as of version 4.4 PhotoDemon's histogram window is now **non-modal**. This means that you can leave the histogram window open while loading/saving/manipulating images, and the window will automatically refresh itself when necessary. Perform a filter or color operation and the histogram will update to reflect those changes; Undo a previous action and it will also update, making it very useful for comparing the effects of various filters.

As part of these updates, the histogram code has been newly refactored and optimized, so it's fast and extremely low-resource, even when left open during image operations. All histogram data is pre-calculated, so when you change rendering options (such as enabling/disabling channels or switching between logarithmic and regular representation) the new histogram is instantly redrawn without requiring a recalculation of the raw data.

I'm not done with histogram updates, but v4.4 provides a great improvement over v4.3.

## Redesigned Grayscale Interface and New Grayscale Algorithms

The grayscale conversion form has been completely redesigned in v4.4:

![Redesigned grayscale interface](images/old-vs-new-grayscale.jpg)

*Special thanks to [pixiv user ぴよな*ティア](http://www.pixiv.net/member_illust.php?mode=medium&illust_id=23671187) for the image in the preview.*

Grayscale conversion was one of the last features to lack an instant-preview option, but no longer - you can now see real-time previews of the various grayscale algorithms.

I have also ported over all seven of the grayscale conversion algorithms from [my standalone grayscale project](3643/grayscale-image-algorithm-vb6/), some of which were not present in PhotoDemon.  The full list of available grayscale conversion methods now includes:
	
  * Averaging
  * ITU standard (adjusting for cone density in the human eyes)
  * Desaturation (HSL color space)
  * Decomposition to maximum or minimum values
  * Single color channel reduction
  * Reduction to specific # of gray shades
  * Reduction to specific # of gray shades with dithering

PhotoDemon defaults to the ITU standard method, which is the best choice for people who have no idea what these various options mean.  :)  For a full discussion of how these methods work and why some are preferable to others, see my aforementioned [in-depth grayscale article](3643/grayscale-image-algorithm-vb6/).

Finally, the reduce-to-specific-number-of-shades option can now be used to reduce an image to black and white (two shades).  Previously it required three shades or more.  That said, I still advise using PhotoDemon's specific "convert to black and white" menu option, which provides more control over 2-color reduction.

## Other miscellaneous updates and bugfixes

Other updates in v4.4 include:
	
  * The system hand cursor is now automatically applied to all clickable objects.  This was previously done manually, and because VB isn't smart about sharing resources, a hand cursor was stored in multiple places throughout the .exe.  The new automated feature meant I could remove those references, so the new v4.4 .exe is actually smaller than v4.3, despite including a bunch of additional features.  Windows Vista/7 users will also get a much prettier hand icon.
	
  * Batch conversion now has a more robust error handler.  This is in preparation for the addition of an all-new batch conversion wizard, which didn't make the cut for 4.4 but should be included in 4.5
	
  * Miscellaneous bug fixes related to save prompting, MDI maximizing, and more.  See a full list of updates at [PhotoDemon's commit page on github](https://github.com/tannerhelland/PhotoDemon/commits/master).

## In Conclusion...

I hope you enjoy the changes in version 4.4.  As always, feel free to [contact me](contact) with any feedback you might have.
