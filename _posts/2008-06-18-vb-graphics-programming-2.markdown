---
author: tanner_h
date: 2008-06-18 02:31:17+00:00
layout: post
slug: vb-graphics-programming-2
title: 'VB Graphics Programming: Part 2 (Beginning API)'
redirect_from:
  - /41/vb-graphics-programming-2/
  - /vb6/vb-graphics-programming-2/
  - /41/vb-graphics-programming-2
  - /vb6/vb-graphics-programming-2
---

**Basic API Pixel Routines**
Next, let's discuss the basics of per-pixel graphics programming using the simple API routines of `GetPixel` and `SetPixel`/`SetPixelV`.  If you haven't already, I recommend reading [the previous page, "Pure VB Pixel Routines,"](2008/06/17/vb-graphics-programming-1) as it provides the foundation for the advanced graphics principles discussed in this and the next two sections.

Assuming that you now understand how to use built-in Visual Basic functions to get per-pixel data, it is time to extend that information a little bit further to include the Windows API.  For those who don't know, the Windows API is a collection of dynamically linked libraries (so-called 'DLL files') that contain commonly used programming routines.  These routines, or "interfaces" (API = Application Programming Interface) range from I/O to networking to multimedia, and they generally work much faster than the intrinsic Visual Basic routines.  The API that we are going to be looking at is called "GDI32," which stands for Graphic Device Interface: 32-bit version.  (This dll is included with every Windows OS since Win95, so no matter what OS you are using with VB 5/6 this method will work.)

GDI32 is a collection of - surprise, surprise - routines commonly used in graphic and image manipulation.  This includes brushes for drawing, bit-block transfers (`BitBlt`) for painting image sections, and what we're most interested in for this tutorial: several important ways to get and set pixel data.  We will start by looking at three functions in particular: `GetPixel`, `SetPixel`, and `SetPixelV`.

**I - Declaring the Necessary API Functions**

Because the GDI32 functions aren't an integral part of the Visual Basic programming language, we have to **declare** them in the General Declarations section just as we would a variable or a type.  The syntax each of our API function declarations is as follows:

    Private Declare Function GetPixel Lib "gdi32" (ByVal hDC As Long, ByVal x As Long, ByVal y As Long) As Long
    Private Declare Function SetPixel Lib "gdi32" (ByVal hDC As Long, ByVal x As Long, ByVal y As Long, ByVal crColor As Long) As Long
    Private Declare Function SetPixelV Lib "gdi32" (ByVal hDC As Long, ByVal x As Long, ByVal y As Long, ByVal crColor As Long) As Byte

For those unfamiliar with API declarations, these might look imposing at first - but don't worry.  They're all pretty darn straightforward.
	
  * `Private` simply means that we only want to use these functions within the current code block. If we were to use `Public` instead of `Private`, we could use these function calls in any module, class module, or form in the current project.
	
  * `Declare Function "FunctionName"` simply lets VB know that we plan on using a function titled `GetPixel` or `SetPixel`.
	
  * `Lib "gdi32"` is short for _Library "C:\Windows\System\gdi32.dll"_ - it tells Visual Basic which dynamically-linked library (DLL) contains the code for the 'FunctionName' we just declared.

The values inside of the parentheses are nothing more than variable declarations, just as you would see for a standard sub or function.
	
  * `hDC` stands for "Handle Device Context." This is the computer's way of saying 'address of an object.' This variable tells us what picture box we want to draw on (like `PictureBox1.hDC`)
	
  * `X` and `Y` are the location - in pixels - of the pixel we want to work with. API calls always work in pixels, so you should too.  If your picture boxes use twips, inches, or any measurement other than pixels, these calls won't work.
	
  * `crColor` in `SetPixel` and `SetPixelV` is the color that we want to set pixel (x,y) to.  This is identical to the 'Color' part of the `PSet` call.  (I'm not entirely sure why this is typically declared as "crColor"; you could call it anything you wanted, but convention seems to stick to "crColor." Go figure...)

Looks familiar, eh? You should be able to recognize some major similarities between these calls and `Point`/`PSet`. If you don't, you may want to reread the [previous tutorial page](2008/06/17/vb-graphics-programming-1).

**II - Using Our New Friend, GetPixel**

Now that we've told Visual Basic everything it needs to know about our "GDI32" functions, we can use them anywhere and everywhere we want to!  Yay!

Let's demonstrate.  If you wanted to get a color from pixel (35, 42) of picture box "Picture1", you would use the following:

    Dim Color as Long
    Color = GetPixel(Picture1.hDC, 35, 42)

I hope this looks painfully easy, because that's exactly what it is.

Now that you've gotten your color into a variable of type `Long`, you still have to [extract the individual red, green, and blue components](2008/06/17/vb-graphics-programming-1) just like before. I'm not going to repeat all that stuff, so just cut and paste those functions out of the last tutorial if you need them.

**III - Setting Pixels Using SetPixel and SetPixelV**

Again, setting a pixel's color is almost identical to getting its color:
    
    Dim APIReturnValue as Long
    APIReturnValue = SetPixel(PictureBox.hDC, x, y, Color)

OR
    
    SetPixel PictureBox.hDC, x, y, Color

OR
    
    Dim APIReturnValue as Byte
    APIReturnValue = SetPixelV(PictureBox.hDC, x, y, Color)

OR
    
    SetPixelV PictureBox.hDC, x, y, Color

Ahhh! Four different ways to do exactly the same thing!  Seems a little weird, doesn't it?  Let me explain why this is.

Every function returns a value of some type.  If you'll scroll back up and look at the `SetPixel` and `SetPixelV` declarations, you'll notice a slight difference between the two: `SetPixel` is of type `Long` and `SetPixelV` is of type `Byte`. This is because `SetPixel` returns the color that it was able to set (for example, if you tried to set `RGB(0, 0, 1)` in 8- or 16-bit color mode, `SetPixel` would likely only be able to set `RGB(0, 0, 0)` instead), while `SetPixelV` only returns whether or not the pixel was set (1 or 0).  Because `SetPixelV` only has to return a boolean value instead of a `Long` (though they're stored identically in memory), I prefer to use it.  However, `SetPixel` could be useful in color modes other than 24-bit, because you could determine the difference between the color you wanted to set and the color that actually got set, as mentioned above.

This is the difference between `SetPixel` and `SetPixelV`.  The reason for the other two declarations is whether or not we care what value `SetPixel`/`SetPixelV` returns.  If we don't care, it is easier to just use the second form of the call - the one without the extra variable declaration.  If, however, we want to know what value they return, we need to use the first form.

Now you know four different ways to set pixels using the API!  Use that to impress your friends... :)

Let's quickly demonstrate a specific example using `SetPixel`/`SetPixelV`. Using our example from the last tutorial, let's say that you want to set pixel (35,42) of the picture box titled "Picture1" to the value of variable 'Color:'
    
    SetPixelV Picture1.hDC, 35, 42, Color

Again we note that `Color` is of type `Long` - you could use the `RGB()` function just as you did in part 1.  In that case, you could write:
    
    SetPixelV Picture1.hDC, 35, 42, RGB(255, 0, 0)

To set pixel (35, 42) of "Picture1" to pure red.  See how easy the API calls are to use?  Once declared, they are no harder than than `PSet` and `Point` - and, as you're about to see, they're significantly faster.

**IV - Using GetPixel and SetPixel to Edit an Image**

[Download the GetPixel/SetPixel example program](https://github.com/tannerhelland/vb6-code/tree/master/Brightness-effect/Part%202%20-%20API%20-%20GetPixel%20and%20SetPixel)

This sample project is identical to the last one, except it swaps out `PSet` and `Point` for `SetPixel` and `GetPixel`.  Compare the results of this program to the `PSet`/`Point` one - notice a pretty significant difference?  As a good programming exercise, build a small function to time how long each method takes and compare the results.  The API calls can be anywhere from 3-10x faster than `PSet` and `Point` - a welcome improvement for no extra work.

**V - In Conclusion: The Need for Speed - GetPixel/SetPixel vs. Point/PSet and Beyond...**

I hope that you're beginning to see the advantages of well-used API calls within your Visual Basic programs.  If you can master using the Windows API, your VB capabilities are endless.  `GetPixel`/`SetPixel` are just the tip of the iceberg, too - the next tutorial will show you a method 10-50x faster than this one!  Get excited!!

But before we head into the next tutorial, let's think of ways that `GetPixel` and `SetPixel`/`SetPixelV` could be improved.

For one, we still have to manually extract the red, green, and blue values out of a `Long`-type variable - this is not only annoying, but it's slow as well.  Things would go faster if we could somehow get Windows to separate the `Long` variable for us.

Also, there is this problem of having to use `GetPixel`/`SetPixel` for every single pixel.  Any way you slice it, running two functions for each of our 120,000 pixels is a pretty slow proposition.  What if there was a way to get the data for every single pixel at once - that way, we'd only have to use a single API call to get ALL of our pixel data.  Now _that_ would be fast!

Well believe-it-or-not, our next tutorial will explain how to do just that - get Windows to give us all of an image's pixel data at once, nicely parsed into its red, green, and blue components.  These are commonly referred to as **DIB sections**, the most powerful API graphics call you can use from within VB.


**[Continue to Part 3: Advanced API Pixel Routines](2008/06/17/vb-graphics-programming-3)**
