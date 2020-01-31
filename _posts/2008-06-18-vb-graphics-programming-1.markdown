---
author: tanner_h
date: 2008-06-18 02:31:12+00:00
layout: post
slug: vb-graphics-programming-1
title: 'VB Graphics Programming: Part 1 (Pure VB)'
redirect_from:
  - /40/vb-graphics-programming-1/
  - /vb6/vb-graphics-programming-1/
---

**Pure VB Pixel Routines**

First, let's discuss the basics of per-pixel graphics programming using only built-in Visual Basic functions.  I recommend that even hardened VB veterans glance through this document, as it provides the foundation for the advanced graphics principles discussed in the next three tutorials.  We will discuss the only VB per-pixel graphics functions (Point and PSet), and after this is done you may know a lot more than you ever wanted to about VB graphics... 

Most of you have probably heard of the "horrible twins of PSet and Point" (_as quoted by Matt Hart, the legendary VB programmer_). These two routines are usually the first per-pixel methods introduced to VB programmers (since they come included as part of the language), but - perhaps inevitably - they are also the slowest way to do things.  Avoid ever using these routines for per-pixel image processing (though they do have some uses in non-pixel-sized work). I include them here only for completeness; I would never recommend using them in an actual image processing program because they are _so_ extremely slow.

Why are they so slow? We'll discuss that later, after we've looked at their syntax.

**I - Getting the Color of an Individual Pixel**

You can use the Point event in VB to get the color of a specified pixel. The format is as follows:

    Dim Color as Long
    Color = PictureBox.Point(x,y)

PictureBox is the name of the picture box or form you want to retrieve the pixel from, and (x,y) are the pixel's coordinates.

For example, if you wanted to get a color from spot (35, 42) of picture box "Picture1", you would use the following:
    
    Color = Picture1.Point(35,42)

It doesn't get much simpler than that, folks.

So now the question is "what do I do once I've gotten the color?" After all, it comes in Long type, which is some strange number from -2 billion to +2 billion...and that really doesn't lend itself to easily adjusting the color of that pixel.

Thus the challenge is figuring out how to change one 4-byte number into three 1-byte numbers (red, green, and blue).

While this may sound easy, the theory behind doing this requires some knowledge of binary encoding…which is far too large a topic to be covered here. Luckily for you, here are three functions that will automatically do RGB color extraction for you:
    
    Public Function ExtractR(ByVal CurrentColor As Long) As Byte
       ExtractR = CurrentColor And 255
    End Function
    
    Public Function ExtractG(ByVal CurrentColor As Long) As Byte
       ExtractG = (CurrentColor \ 256) And 255
    End Function
    
    Public Function ExtractB(ByVal CurrentColor As Long) As Byte
       ExtractB = (CurrentColor \ 65536) And 255
    End Function

To utilize these functions, use the following syntax:
    
    Dim R as Byte, G as Byte, B as Byte
    
    Dim Color as Long
    
    Color = PictureBox.Point(0, 0)
    
    R = ExtractR(Color)
    G = ExtractG(Color)
    B = ExtractB(Color)

Pretty neat, eh?

This is the first method we'll use for getting a pixel's data and breaking it down into its red, green, and blue components.  Now let's quickly mention how to set this data back into a picture box.

**II - Setting the Color of an Individual Pixel**

Setting a pixel's color is almost identical to getting its color. You use the VB event "PSet," which stands for "Pixel Set."
    
    PictureBox.PSet (x,y), Color

Again, PictureBox is the name of the picture box or form you want to set the pixel to and (x,y) are the pixel's coordinates. The only difference here is that we also include the color that we want to set. So, using the example above, if you wanted to set a color to pixel (35, 42) of picture box "Picture1" you would use the following:
    
    Picture1.PSet (35,42), Color

It is worth noting that Color is of type Long, which creates the same problem we discussed above - how to change three separate red/green/blue values into a single 4-byte number. Fortunately, VB has a built-in command called `RGB()` that does this conversion for us. To illustrate it's use, let's use the same example saying that you want to change the color of the pixel at (35,42) to pure red:
    
    Picture1.PSet (35,42), RGB(255, 0, 0)

The first RGB parameter is red, then green, last blue, so `RGB(255,0,0)` will set the color to pure red.  Easy!

**III - Using Point and PSet to Edit an Image**

First, a little disclaimer: entire books have been written on the theories behind GP and there are entire programming disciplines whose job is nothing but optimizing graphics routines.  So, while what I'm about to show you in code is a nice method, be advised that GP is an extremely complicated field and to truly succeed in it you must be willing to do a little research.  I have chosen a well-optimized and very standard method for my sample programs because it is easy to understand while still offering good results.  But, for this first tutorial, don't be disappointed if the results aren't particularly incredible or lightning-fast.  That's what the next three tutorials are for!

[Download the PSet/Point example program](https://github.com/tannerhelland/vb6-code/tree/master/Brightness-effect/Part%201%20-%20Pure%20VB6)

The sample project demonstrates how to change the brightness of an image using a standard linear brightness algorithm. The code is simple and well-commented. Read through the comments and make sure that you understand how everything works.

**IV - Why are Point and PSet So Slow?**

If you've tried out the sample code, you're probably not impressed…and rightfully so!  Point and PSet - though easy to use - are extremely slow. Can you imagine trying to work with images 4 or 5 times the size of the demo one?  Not so cool.

So why are these two functions SO slow?  To illustrate it, let's follow the path your computer takes for changing the color of a single pixel using Point and PSet as you just saw done in the sample program. _(Author's Note: I base these conclusions on general programming knowledge, not known facts; so while I'm pretty sure that this explanation is accurate, I could be wrong on some of the details. I invite and encourage input on making this section 100% accurate.)_
	
  1. Upon encountering a Point command, VB's first task is to do a whole crapload of error checking. This involves things like making sure that the pixel you want is within the image's boundaries, making sure that the PictureBox exists, seeing if an image has been loaded or if you're working with a blank image, etc. This step is speed killer #1 - but the advantage is that Point will never crash your machine, thankfully.
	
  2. Once VB has decided that there is actually a pixel at point (x,y), it now has to figure out where to get the pixel color from.  This changes depending on both the status of AutoRedraw and whether or not you've updated the image since loading it. VB will usually go to the 'Image' property, but in certain cases AutoRedraw may tell it to go to the 'Picture' property.  (If that doesn't make any sense, forget about it!)  This step is speed killer #2 - but again, you never crash your machine and you always get predictable results.
	
  3. After VB knows where the pixel data resides, it can now go and get the pixel information. This step is all handled in memory, so this is really fast.
	
  4. After VB gets the color of this pixel, it must transfer that information into the variable specified by the original Point command.  This is all but instantaneous - no speed problems here.
	
  5. Once a variable of type Long contains the color of the pixel, we must parse that long into its red, green, and blue components. This step is speed killer #3, because we gotta do three 'Ands' and two 'Divides' for every single pixel. For an image like the sample one, that's 400x300 or 120,000 pixels... meaning there's a grand total of 360,000 'Ands' and 240,000 'Divides.' This step is a very, very bad one for speed - the 'Ands' are fast, but the 'Divides' are extremely slow (times 240,000).
	
  6. Once we have a red, green, and blue component, we change these values to the new values specified by the look-up table. This step is very fast because, again, it's nothing more than simple memory transfers.
	
  7. Next comes the PSet step.  This process is almost identical to Point, so I'm going to abbreviate its steps.  First, it does the error checking.  Speed killer #4 here.
	
  8. VB will automatically assign the new color to its appropriate location within the 'Image' property.  This is fast - again, it's all done in memory.
	
  9. Now VB has to decide whether or not to refresh the image.  If AutoRedraw is set to false, VB will attempt to redraw the entire image after each pixel has been set.  Do not do this - EVER - while working with per-pixel programming routines.  If AutoRedraw is set to true, VB will only redraw the entire image after you explicitly tell it to or after you finish the loop containing the PSet calls.  Redrawing the image is very slow because your computer has to copy the information for thousands of pixels from the Picture or Image property to wherever the screen data is located (either VRAM or RAM - this is yet one more thing your computer has to figure it; it too takes time). Although your RAM is one of the faster parts of your computer, it will be slowed down by lots of huge memory chunk transfers (like graphics).  This is speed killer #5.

Steps 1, 2, 5, 7, and 9 are what's slowing down your PSet/Point-based graphics program. Visual Basic is very nice in that it does almost all of your error checking for you, but there is a definite speed trade-off.  In other programming languages and per-pixel routines, many of these error checking steps are removed - which is one of the reasons why other languages and functions are generally faster but more dangerous to use. In the next three tutorials we will discuss alternate methods of doing graphics that cut out some of these "speed killer" steps.

**V - Conclusion**

Hope that all made sense to you!  Does it feel good knowing you can now program any graphics routine using nothing but VB?  Hope it does - but don't get too comfortable yet.

To be totally honest, I hope that you completely forget that PSet and Point even exist - at least as far as per-pixel image processing is concerned - after reading the next three tutorials.  Both are extremely slow and... well, just bad programming for image processing.  VB6 is good for a lot of things, but its pixel interfacing is a total joke.

Thankfully, there are three more tutorials that will show you better, faster ways to do graphics programming - but at least you now know how to use PSet and Point if the need ever arises.

**[Continue to Part 2: Basic API Pixel Routines](2008/06/17/vb-graphics-programming-2)**

