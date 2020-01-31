---
author: tanner_h
date: 2008-06-18 02:31:22+00:00
layout: post
slug: vb-graphics-programming-3
title: 'VB Graphics Programming: Part 3 (Advanced API)'
redirect_from:
  - /42/vb-graphics-programming-3/
  - /vb6/vb-graphics-programming-3/
  - /42/vb-graphics-programming-3
  - /vb6/vb-graphics-programming-3
---

**Advanced API Pixel Routines**

Next comes two advanced ways of getting and setting pixels in Visual Basic: the API routines of `GetBitmapBits`/`SetBitmapBits` and `GetDIBits`/`StretchDIBits`.  If you haven't already, I strongly recommend reading the previous two tutorials, ["Pure VB Pixel Routines"](2008/06/17/vb-graphics-programming-1/) and ["Basic API Pixel Routines,"](2008/06/17/vb-graphics-programming-2/) as they provide the foundation for the advanced graphics principles discussed in this section.

Assuming that you now understand how to use both Visual Basic and the API to get per-pixel data, it's time to move to the next - and most difficult - section of these tutorials.  Next we are going to discuss the API routines of `GetBitmapBits`/`SetBitmapBits` and `GetDIBits`/`StretchDIBits`.  Both sets of routines are very fast and very powerful, but they come with a strong disclaimer - **pay close attention to any warnings on this page**.  Because these API routines directly interface the heap (dynamically allocated memory), you can easily crash both the VB IDE and/or Windows with a page fault or worse if you use them incorrectly.  Believe me - it's not a pretty sight to watch your entire machine freeze because you accidentally allocated your array to the wrong size.  (But it gives you a good taste of programming in non-BASIC languages, heh heh.)

But on the happy side of things, these are about as fast as graphics get in VB.  There are ways to use CopyMemory, in-line assembly language, and other freakish routines to get slightly faster effects, but they are not designed specifically for graphics programming so I'm going to avoid them here.

On to the programming!

**I - Declaring the Necessary API Functions**

At this point in your VB career you are probably used to interacting with images one pixel at a time (using something like the afore-taught `.Point`/`.PSet` or `GetPixel`/`SetPixel`/`V`).  These functions are simple to use, but that ease comes at the cost of speed. Many things cause these functions to be slow ([as discussed in the first page of this tutorial](2008/06/17/vb-graphics-programming-1/)), so you must be wondering - is there a way to remove some of those speed barriers?

Enter `GetBitmapBits` and `SetBitmapBits`.  The big advantage of these two API calls is this: rather than extracting or setting each pixel in an image individually, we pass each of these functions an array and let them fill the whole thing at once with the picture's pixel data (or set the picture's pixel data all at once with the information in the array).  This is obviously much more efficient.  The trade-off, of course, is that these techniques involve a little more programming and significantly more risk.  If the array dimensions are off by a mere _1 byte_ all kinds of things can happen - the picture won't appear at all, your program will shut itself down, or VB will freeze.  But these only happen if you're careless and don't heed my warnings, so pay close attention and you'll be fine.

We start by declaring a whole bunch of things:
    
    Private Type Bitmap
       bmType As Long
       bmWidth As Long
       bmHeight As Long
       bmWidthBytes As Long
       bmPlanes As Integer
       bmBitsPixel As Integer
       bmBits As Long
    End Type
    
    Private Declare Function GetObject Lib "gdi32" Alias "GetObjectA" (ByVal hObject As Long, _
      ByVal nCount As Long, ByRef lpObject As Any) As Long
    
    Private Declare Function GetBitmapBits Lib "gdi32" (ByVal hBitmap As Long, ByVal dwCount As Long, _
      ByRef lpBits As Any) As Long
    
    Private Declare Function SetBitmapBits Lib "gdi32" (ByVal hBitmap As Long, ByVal dwCount As Long, _
      ByRef lpBits As Any) As Long

This might seem a little extreme, so let me go through each of these one at a time.

The `Bitmap` type is required for the `GetObject` call - if you'll look at the `GetObject` declaration, you'll notice that the last parameter is of type `Any`. This is where we will be passing our `Bitmap` object. As for the individual elements of the `Bitmap` type, typical graphics programming only cares about four out of the seven variables. They are:
	
  * `bmWidth` - the width of the bitmap, in pixels
  * `bmHeight` - the height of the bitmap, in pixels
  * `bmWidthBytes` - the width of a bitmap **in bytes**. If a bitmap is 24 _bits_-per-pixel (bpp), that means that each pixel occupies 3 _bytes_. So in this color mode, `bmWidthBytes` would be (`bmWidth` * 3). If a bitmap were 16 bpp, each pixel would occupy 2 bytes. In that color mode, `bmWidthBytes` would be (`bmWidth` * 2).
  * `bmBitsPixel` - the number of _bits_ per pixel in the image. In 24bpp mode, the number is 24. In 16bpp mode, the number is 16. Pretty straightforward. Divide this number by 8 to get the number of _bytes_ per pixel.

The other three variables aren't needed for getting and setting pixels; we simply include them to ensure that our `Bitmap` type matches the Windows `Bitmap` type.

Next we have the `GetObject` call.  The purpose of this API call is to...well, get an object.  You'll see how this works in a moment.
	
  * `hObject` is an object (containing a picture) that we want to get information about - most likely `PictureBox.Image` or `Form.Image`.  The properties of `hObject` will be transferred into `lpObject` (see below).
  * `nCount` is the size of the type that is going to receive the information (in our case, the size of the `Bitmap` type).
  * `lpObject` is the variable that is going to hold all of the information that we get from `hObject` (a variable of the `Bitmap` type we've just declared, in fact).  Notice that it is passed `ByRef` - this allows the API call to edit that variable directly.

`GetBitmapBits` and `SetBitmapBits` have identical parameters, which in turn are almost identical to the `GetObject` parameters.
	
  * `hBitmap` represents an object containing a picture (like `hObject` above, most likely `PictureBox.Image`)
  * `dwCount` is the total size of the array holding the image's pixel data
  * `lpBits` is the starting address of the place in memory where we want to place the image data (almost always the first spot of an array). Notice, again, that it is declared as `ByRef` - this allows the API call to edit the array directly (which is a good thing, because that's how we get the image data!).

Okay - that's a whole lot of information in a small space, so take a quick break to make sure you understand those declarations.  If some of this is a little hazy, that's okay, because we're about to see how they work.

**II - Getting Pixels Using GetBitmapBits**

Ready?  If so, here's how we use `GetBitmapBits`:
    
    Dim bm As Bitmap
    
    GetObject PictureBox.Image, Len(bm), bm
    
    Dim ImageData() as Byte
    ReDim ImageData(0 To (bm.bmBitsPixel \ 8) - 1, 0 To bm.bmWidth - 1, 0 To bm.bmHeight - 1)
    
    GetBitmapBits PictureBox.Image, bm.bmWidthBytes * bm.bmHeight, ImageData(0, 0, 0)

Surprisingly, this procedure is very straightforward.  First, we declare a `Bitmap` object and call the `GetObject` function.  When called, `GetObject` will analyze the specified `PictureBox` and assign the appropriate values to our `Bitmap` object, which we can then use to prepare our array to receive the image's pixel data.

Once we have all the picture's information available to us in the form of a `Bitmap` object, we declare an array. This `ImageData` array is of critical importance - we're going to use it to hold all of the picture's pixel information.  To make sure it is the right size, we use `ReDim` to make its dimensions just perfect:
	
  * The first dimension will contain the values of each pixel's red, green, and blue values. (`bm.bmBitsPixel` should equal 24 because your computer is in 24 bit color mode; thus we get 24/8 = 3 bytes per pixel. Because we start the dimension at zero, we subtract one from the upper bound to give us three total spots: 0, 1, and 2, which correspond to red (2), green (1), and blue (0))
  * The second dimension will be used to address the x coordinates of the image's pixels.
  * The third dimension will used to address the y coordinates of the image's pixels.

**SIDE NOTE ABOUT 'GETOBJECT'**: You may be wondering why we use the `GetObject` call at all - couldn't we just resize the `ImageData` array using the picture box's `ScaleWidth` and `ScaleHeight` properties?  In theory, you could.  However, VB5 does strange things to the `ScaleWidth` and `ScaleHeight` properties depending on what is stored there.  For example, the same image might report different `ScaleWidth` and `ScaleHeight` properties at different execution times.  In my experience, JPEGs are notoriously bad at this - when you load one, VB5 sometimes thinks that the picture's width is one pixel less in the picture box than it is in memory.  Honestly, I have no idea as to why VB5 has this problem.  VB6 seems to work fine.  `GetObject` is always accurate so I use it instead, and I recommend that you do too.  There is no measurable speed difference between these two mechanisms.

**SIDE NOTE ABOUT DECLARING YOUR ARRAY**: Arrays supplied to `GetBitmapBits` (and later in this tutorial, `GetDIBits`) must have a width that is a multiple of **4**, _e.g._ 4, 8, 16, 256, 360, etc.  If your image has a width that is a multiple of four, no worries - but if it is not a multiple of four, you will need to adjust your code accordingly.  See the bottom of this page for details (in the section titled "VI - OPTIONAL: The Infamous 4-Byte Alignment Issue").

**ANOTHER SIDE NOTE ABOUT DECLARING YOUR ARRAY**: You can use any number of dimensions in your array, so long as the **total size** is accurate. For example, you could also do something like `ReDim ImageData(0 to bm.bmWidth * bm.bmHeight * 3 - 1)` and the function would still work fine. The API call could care less about how the array is declared - all it gets is the address of the first element in the array and the number of bytes that it's allowed to work with. The way the array is dimensioned is only for your convenience.  I like the above way because it makes editing the image very easy. This issue will be discussed further in the next section of this tutorial.

**WARNING!!** This `ReDim` statement is where you can really screw your computer.  If `ImageData` is too small, `GetBitmapBits` will attempt to put the picture data in unallocated memory - causing a general protection fault, a page fault, or some other nasty illegal operation.  Make sure that `ImageData` is the right size!

The `GetBitmapBits` call itself is very straightforward: it takes the array (in this case, `ImageData()`) and fills it with the pixel data located in `PictureBox`.  Now you can edit the values any way you want.  For example, the following loop would invert all of the pixels in the image:
    
    'First, get the image data using the above code section
    
    Dim X as long, Y as long
    
    For X = 0 to PictureBox.ScaleWidth - 1
    For Y = 0 to PictureBox.ScaleHeight - 1
    
       'Invert the R value
       ImageData(2, X, Y) = 255 - ImageData(2, X, Y)
       
	   'Invert the G value
       ImageData(1, X, Y) = 255 - ImageData(1, X, Y)
       
	   'Invert the B value
       ImageData(0, X, Y) = 255 - ImageData(0, X, Y)
	   
    Next Y
    Next X

Really, `GetBitmapBits` is as easy as `GetPixel` if you understand the API structure.

**III - Setting Pixels Using SetBitmapBits**

`SetBitmapBits` is almost identical to `GetBitmapBits`:
    
    Dim bm As Bitmap
    
    GetObject PictureBox.Image, Len(bm), bm
    
    SetBitmapBits PictureBox.Image, bm.bmWidthBytes * bm.bmHeight, ImageData(0, 0, 0)
    
    If PictureBox.AutoRedraw Then
       PictureBox.Picture = PictureBox.Image
       PictureBox.Refresh
    End If

Everything is the same as `GetBitmapBits`, except that we aren't resizing the array (because it is already the right size and resizing it would erase all of its information!).  The last `If`/`Then` statement is included because `SetBitmapBits` won't automatically initialize the `AutoRedraw` event, so we have to tell it to replace the `Picture` property (what is shown on the screen) with the `Image` property (what is stored in memory).

I hope you're finding this easier than expected!  In fact, it's almost too easy... so of course, there is a slight problem with this method: **both `GetBitmapBits` and `SetBitmapBits` only work in 24/32-bit color mode (16.7 million colors).** Actually, they work in 16 and 8 bit color modes too, but the image data no longer occupies 3+ bpp (bpp = bits per pixel) so editing the image data is significantly more complicated.  It can be done, but you have to write a function to translate 2 bits into 3 as well as transferring the data into a separate array while you edit it.  Then, to draw it, you have to translate the 3 bits back into 2 bits and then transfer your editing array back into the original one.  It's messy and time-intensive, so I wouldn't recommend this method.

So of course, someone is going to ask "but how can I do fast graphics in 16 or 8 bit color mode?" That is what DIB sections are for, so if you want to know about them then keep reading.

(Personally, I would recommend using DIB sections for all of your graphics programs because you'll never get unexpected color-mode errors with them, and it’s a great way to add additional functionality to your graphics program.  I have only discussed BitmapBits because they make for an excellent introduction to DIB sections.)

**IV - A Crash Course in Declaring DIB Sections**

DIB section stands for 'Device Independent Bitmap.'  The name is pretty self-explanatory: DIBs are simply a way of interacting with bitmaps in any color mode or on any computer and getting consistent results.  There are actually two varieties of DIBs - OS/2 encoded and Windows encoded, so I guess "device independent' isn't totally accurate... but that's okay.

DIBs share many characteristics with BitmapBits.  The calls share certain parameters and the underlying logic is very much the same.  However, DIB sections have several major differences you need to be aware of: they're slightly more confusing to use, they require more code, and they return the image data upside-down.  The most important difference, however, is that DIB sections work in _any_ color mode - and, as a bonus, the StretchDIBits call is much more powerful than SetBitmapBits. Below are the required DIB section declarations:
    
    Private Type BITMAP
       bmType As Long
       bmWidth As Long
       bmHeight As Long
       bmWidthBytes As Long
       bmPlanes As Integer
       bmBitsPixel As Integer
       bmBits As Long
    End Type
    
    Private Declare Function GetObject Lib "gdi32" Alias "GetObjectA" (ByVal hObject As Long, _
      ByVal nCount As Long, ByRef lpObject As Any) As Long
    
    Private Type RGBQUAD
       rgbBlue As Byte
       rgbGreen As Byte
       rgbRed As Byte
       rgbAlpha As Byte
    End Type
    
    Private Type BITMAPINFOHEADER
       bmSize As Long
       bmWidth As Long
       bmHeight As Long
       bmPlanes As Integer
       bmBitCount As Integer
       bmCompression As Long
       bmSizeImage As Long
       bmXPelsPerMeter As Long
       bmYPelsPerMeter As Long
       bmClrUsed As Long
       bmClrImportant As Long
    End Type
    
    Private Type BITMAPINFO
       bmHeader As BITMAPINFOHEADER
       bmColors(0 To 255) As RGBQUAD
    End Type
    
    Private Declare Function GetDIBits Lib "gdi32" (ByVal hDC As Long, ByVal hBitmap As Long, _
      ByVal nStartScan As Long, ByVal nNumScans As Long, lpBits As Any, lpBI As BITMAPINFO, _
      ByVal wUsage As Long) As Long
    
    Private Declare Function StretchDIBits Lib "gdi32" (ByVal hDC As Long, ByVal x As Long, _
      ByVal y As Long, ByVal dWidth As Long, ByVal dHeight As Long, ByVal SrcX As Long, _
      ByVal SrcY As Long, ByVal SrcWidth As Long, ByVal SrcHeight As Long, lpBits As Any, _
      lpBI As BITMAPINFO, ByVal wUsage As Long, ByVal RasterOp As Long) As Long

Quite the mess of declarations, isn't it? You should notice some similarities between these declarations and the BitmapBits ones. Here's a quick explanation of the DIBits calls:
	
  * The first type and declaration are just the same old `GetObject` stuff - you already know all about that.
  * The next type, `RGBQuad`, represents basic pixel data - red, green, and blue values, along with an alpha channel.

**SIDE NOTE ON ALPHA CHANNELS**: For those who are interested: both DIBs and regular bitmaps can contain transparency information.  If you have (what used to be, heh) an expensive monitor and video card and run them at 32-bit color mode, that extra byte contains transparency data (a number from 0-255, 0 being opaque and 255 being transparent).  So technically, 32-bit bitmaps and DIBs could be used like GIFs or PNGs and displayed transparently.  There's actually an API call with Win2K/ME/XP called `AlphaBlend` that's similar to `BitBlt`/`StretchBlt` except that it utilizes an alpha channel (this method is similar to DirectX and a transparent key color); you can read all about the `AlphaBlend` call at MSDN.

  * The `BITMAPINFOHEADER` type contains all of a particular bitmap's information, unlike the stripped-down version we use for `GetObject`.  This is what makes DIB sections "Device Independent" - by knowing all of that extra information about the bitmap we can display it accurately on any device at any color resolution.
  * Lastly, the `BITMAPINFO` class combines a header and an array of `RGBQUAD`s (used for the palette in 8-bit images).  This header is capable of holding data for DIB sections of any color depth - from 1bpp to 32bpp.  Again, this is part of making DIB sections "Device Independent."  It also comes in handy when using 8bpp color modes because you can directly edit the palette for super-fast graphics effects.

The `GetDIBits` call is somewhat more complicated than the `GetBitmapBits` one, so let's go through it one part at a time.
	
  * `hDC` is the same as it was in `GetPixel` - it is the handle/"address" of the _device_ we want to get the pixel data from. Most likely, this is `PictureBox.hDC` or `Form.hDC`.
  * `hBitmap` is the _location_ of the pixel data itself. This is most commonly `PictureBox.Image` or `Form.Image`
  * `nStartScan` is the line we want to start reading the pixel data from.  This will always be 0, unless for some odd reason you want to read the data from the middle of the image.
  * `nNumScans` is the number of horizontal lines that you want to read from the image.  This will always be the height of the image (in pixels), unless you want to extract every-other-line or something strange like that.  (Scanlines also come in handy for doing fast image rotations, but I'm not going to discuss those here.)
  * `lpBits` is the same as it was in `GetBitmapBits`.  This is the array that the image's data will be copied into.
  * `lpBI` is a `BitmapInfo` variable that contains all of the desired information of the bitmap we are want to get.  This includes the width, height, and - important! - the color depth.  This is how we let Windows know that even though the computer may be in 16bpp or 8bpp color modes, we want the bitmap information to be in 24bpp mode (color depth is handled via the `.bmBitCount` property).
  * Last is the `wUsage` variable, which is related to referencing source-DC-based palettes. Because this tutorial focuses only on 24-bit (i.e. non-paletted) image processing, we're going to ignore this variable completely - just always leave it as zero.

We're almost done!

Unfortunately, if you thought `GetDIBits` was long-winded, you're not going to like `StretchDIBits`.  `StretchDIBits` is a very powerful call, but this means there are a lot of parameters.  If you are familiar with `BitBlt` and/or `StretchBlt` this part will probably make a lot of sense to you.  The `StretchDIBits` parameters are:
	
  * `hDC`: same as `GetDIBits`
  * `x`: the x coordinate of the top-left corner you want to draw the pixels to
  * `y`: the y coordinate of the top-left corner you want to draw the pixels to
  * `dWidth`: the desired width of the destination image.  This is usually the same size as the image you got the data from, although you can stretch or shrink the destination size if you wish.
  * `dHeight`: the desired height of the destination image.  Refer to the `dWidth` notes.
  * `SrcX`: the x coordinate of the top-left pixel in the source array (for us, `ImageData()`) that you want to start taking the pixels from. Usually zero, but you can change this value to only take a portion of the source image.
  * `SrcY`: the y coordinate of the top-left pixel in the source array that you want to start taking pixel data from.  Refer to the `SrcX` notes.
  * `SrcWidth`: the desired width of the pixel selection from the source image. This is usually the same size as the original image, although you can stretch or shrink the source size if you wish.
  * `SrcHeight`: the desired height of the pixel selection from the source image. Refer to the `SrcWidth` notes.
  * `lpBits`: same as `GetDIBits`. This is the array that the pixel data will be taken from (again, `ImageData()`)
  * `lpBi`: same as `GetDIBits`. This is the `BitmapInfo` variable that contains all of the correct parameters for our pixel data.
  * `wUsage`: same as `GetDIBits` - leave it as zero.
  * `RasterOp`: a raster operation, exactly the same as you would use for `BitBlt` or `StretchBlt`. There is a complete list of `RasterOp` constants listed in the VB help files (or MSDN collection), but the most common one is `vbSrcCopy`, which will simply copy the pixels from the source array to the destination picture box.

**V - Using DIB Sections**

Now that your brain has had some time to digest all of those declarations, let's demonstrate the `GetDIBits` call.  Here's a full-blown example of how to get an image's data using the `GetDIBits` call, minus the declarations above:
    
    'Routine to get an image's pixel information into an array dimensioned (rgb, x, y)
    Public Sub GetImageData(ByRef SrcPictureBox As PictureBox, ByRef ImageData() As Byte)
    
    'Declare variables of the necessary bitmap types
    Dim bm As Bitmap
    Dim bmi As BITMAPINFO
    
    'Now we fill up the bmi (Bitmap information variable) with all the necessary data
    bmi.bmHeader.bmSize = 40 'Size, in bytes, of the header (always 40)
    bmi.bmHeader.bmPlanes = 1 'Number of planes (always one)
    bmi.bmHeader.bmBitCount = 24 'Bits per pixel (always 24 for image processing)
    bmi.bmHeader.bmCompression = 0 'Compression: none or RLE (always zero)
    
    'Calculate the size of the bitmap type (in bytes)
    Dim bmLen As Long
    bmLen = Len(bm)
    
    'Get the picture box information from SrcPictureBox and put it into our 'bm' variable
    GetObject SrcPictureBox.Image, bmLen, bm
    
    'Build a correctly sized array.
    ReDim ImageData(0 To 2, 0 To bm.bmWidth - 1, 0 To bm.bmHeight - 1)
    
    'Finish building the 'bmi' variable we want to pass to the GetDIBits call
    bmi.bmHeader.bmWidth = bm.bmWidth
    bmi.bmHeader.bmHeight = bm.bmHeight
    
    'Now that we've filled the 'bmi' variable, we use GetDIBits to take the data from SrcPictureBox and put
    '  it into the ImageData() array using the settings specified in 'bmi'
    GetDIBits SrcPictureBox.hDC, SrcPictureBox.Image, 0, bm.bmHeight, ImageData(0, 0, 0), bmi, 0
    
    End Sub

We're almost done with DIB sections - all that's left is `StretchDIBits`.

The procedure required to set up our variables for `StretchDIBits` is almost identical to the procedure we used for `GetDIBits`. In fact, everything up to the actual `GetDIBits` call is the same - everything except the `ReDim ImageData()` line, of course.  (If we ReDimmed the array before setting it, we would erase all of the pixel data!).  Here's a full example:
    
    'Routine to set an image's pixel information from an array dimensioned (rgb, x, y)
    Public Sub SetImageData(ByRef DstPictureBox As PictureBox, ByRef ImageData() As Byte)
    
    'Variables for the necessary bitmap types
    Dim bm As Bitmap
    Dim bmi As BITMAPINFO
    
    'Fill the bmi (Bitmap information variable) with appropriate values
    bmi.bmHeader.bmSize = 40
    bmi.bmHeader.bmPlanes = 1
    bmi.bmHeader.bmBitCount = 24
    bmi.bmHeader.bmCompression = 0
    
    'Calculate the size of the bitmap type (in bytes)
    Dim bmLen As Long
    bmLen = Len(bm)
    
    'Get the picture box information from DstPictureBox and put it into our 'bm' variable
    GetObject DstPictureBox.Image, bmLen, bm
    
    'Now that we know the object's size, finish building the temporary header to pass to StretchDIBits
    bmi.bmHeader.bmWidth = bm.bmWidth
    bmi.bmHeader.bmHeight = bm.bmHeight
    
    'Use StretchDIBits to take the data from the ImageData() array and put it into SrcPictureBox using
    '  the settings specified in 'bmi'
    StretchDIBits DstPictureBox.hDC, 0, 0, bm.bmWidth, bm.bmHeight, 0, 0, bm.bmWidth, bm.bmHeight, _
      ImageData(0, 0, 0), bmi, 0, vbSrcCopy
    
    'Since this doesn't automatically initialize AutoRedraw, we have to do it manually
    'Note: set AutoRedraw to 'True' when using DIB sections. Otherwise, you may get unpredictable results.
    If DstPictureBox.AutoRedraw Then
       DstPictureBox.Picture = DstPictureBox.Image
       DstPictureBox.Refresh
    End If
    
    End Sub

And there you have it - a complete explanation of how to get image data from any picture in any color mode and how to set that same data back into a picture once you're done editing it.

**VI - DIB Sections in Action**

[Download the DIB example program](https://github.com/tannerhelland/vb6-code/tree/master/Brightness-effect/Part%203%20-%20DIBs)

This .zip file shows these exact routines - cut and pasted out of this tutorial into a form - being used to adjust the brightness of an image.  Quite a bit better than `GetPixel` and `SetPixel` or `.Point` and `.PSet`, aren't they?

It may surprise you, but in the next tutorial we're going to get this program running even faster - we're going to use some DIB section tricks to make it run in real-time.

Before we continue, however, I am including an optional section regarding the infamous 4-bit alignment issue associated with DIB sections.  If you are interested in using DIB sections only casually, this issue may not apply to you.  If, however, you plan on using DIB sections extensively, this issue is critical.  DIB sections have trouble if you use them on an image whose width is not a multiple of 4.  We'll discuss how to deal with this problem in the optional section below.

[**Continue to Part 4: even more graphics performance optimizations**](2008/06/17/vb-graphics-programming-4/)

**VI - OPTIONAL: The Infamous 4-Byte Alignment Issue**

As you may know, all versions of Windows at the time of this writing (95, 98, ME, NT4, 2000, XP) are 32-bit operating systems.  This means that memory within Windows is split up into 32-bit, or 4-byte, chunks.  Normally this means very little to a VB6 programmer, but when using DIB sections we must take this into account.

Because DIB sections are designed to be fast, they're optimized for speed in many ways.  One such way is that they require any arrays associated with them to be 4-bytes (or 32 bits) wide.  This allows the arrays to line up in memory exactly - without any trailing bytes - which in turn allows Windows to access the information more quickly, since it doesn't have to re-align each horizontal line of the image to match up with 32-bit memory spaces.

As it turns out, this isn't a problem for images whose width is already a multiple of 4: **800**x600, **32**x32, **1920**x1080, etc.  All standard image/screen sizes are multiples of 4 for a reason.

Sometimes, however, it's necessary to work with images whose width may not be divisible by 4 (_e.g._ 29, 30, and 31 instead of 32).  This creates serious problems with DIB sections - try plugging such an image into the code above and you'll see what I mean.

So how do we solve such a problem?  There's no good way, to be honest.  Two main options exist:

1) Resize the image to make it have a width that's a multiple of 4.

2) Manually force the array containing the image data to have a width that's a multiple of 4.

The first option is preferable, but if that's not available to us then we have to do some hardcore adjusting of the array we use (`ImageData()` in this tutorial).  This requires `CopyMemory` and a `For` loop - both of which are time killers, which is contrary to the whole point of this tutorial.

So in the interest of space and brevity, I'm not going to go through the intricacies of this method in this tutorial.  An easier fix - and my preferred method - is to use a 2-dimensional array to receive the image data instead of a 3-dimensional one, like so:

    ArrayWidth = (bm.bmWidth * 3) - 1
    ArrayWidth = ArrayWidth + (bm.bmWidth Mod 4)
    ArrayHeight = bm.bmHeight
    ReDim ImageData(0 To ArrayWidth, 0 To ArrayHeight) As Byte

This method works well, but accessing individual pixels is slightly more cumbersome:
	
  * Red is in location (x * 3 + 2, y)
  * Green is in location (x * 3 + 1, y)
  * Blue is in location (x * 3, y)

Using a temp variable to store the x * 3 value actually makes this faster than the 3d array used in the tutorials.  As such, this is my favorite method.  It is also the method I use in my open-source photo editor, [PhotoDemon](https://photodemon.org).

Streams, mentioned in the next tutorial, also need to be 4-byte aligned.

[**Continue to Part 4: even more graphics performance optimizations**](2008/06/17/vb-graphics-programming-4/)
