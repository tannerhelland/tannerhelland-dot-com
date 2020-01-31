---
author: tanner_h
date: 2008-06-18 02:31:28+00:00
layout: post
slug: vb-graphics-programming-4
title: 'VB Graphics Programming: Part 4 (Optimizations Checklist)'
redirect_from:
  - /43/vb-graphics-programming-4/
  - /vb6/vb-graphics-programming-4/
---

This last section of my graphics programming tutorials takes a different approach from the previous three sections.  Instead of discussing specific graphics routines, I'm going to give you my "Top 10 List of Graphics Code Optimizations."  This checklist of optimization techniques will provide a simple, straightforward mechanism for speeding up your graphics application.  We'll start with the easiest ways to speed up your code and end with the most dramatic (but effective) ways.  My hope is that you can take slow graphics-related code, adjust it according to this checklist, and end up with a much faster version with minimal impact to code readability or complexity.

**Tanner's Top 10 List of Graphics Optimizations**

**10. Compile to native code, enabling every advanced optimization.** While it may seem obvious, this is the easiest - but oft forgotten - way to speed up your graphics code.  Enabling one optimization in particular: 'Remove Array Bound Checks,' will significantly speed up DIB section code, as it is heavily dependent on arrays.  When you check that box, VB stops checking array locations for validity (_i.e._ if you try to access location `(x,y)` in an array, VB won't check to see if `x` or `y` falls within the declared range of the array).  This optimization comes at a trade-off, of course; any code involving arrays could now be as much as 10-15x faster.  Unfortunately, if you try to access an invalid array location, you won't get an error - your code will cause a critical fault and the program will crash.  (If you write decent code, however, errors like this will _never_ occur.  Check your bounds in advance!)

**9. Check your `ScaleMode`: use pixels, never twips.** [VB.Net has completely done away with twips](http://visualbasic.about.com/od/usevb6/a/Vb-Net-Switches-To-Pixel-From-Twip.htm), but ol' VB6 decided to make this silly measurement the default `ScaleMode` setting for forms and picture boxes.

If your code a) doesn't work, or b) does work but is strangely slow, make sure you've set the `ScaleMode` of all relevant picture boxes and/or forms to pixels.  As a general rule of thumb, set every object's `ScaleMode` to pixels even if you don't plan to use it for graphics.  This helps ensure that you'll never fall victim to twips-related errors.

**8. Don't make your code refreshing.** For most graphics-related code, `AutoRedraw` is your friend.  If you have `AutoRedraw` set to false and you use API-based graphics methods on a picture box, VB6 will attempt to refresh the image every time a pixel changes.  For any image larger than 1x1 pixels, this is a problem.  Refreshing an image takes a lot of time, so refresh an image only after you're completely done messing with it.  (There are several exceptions to this rule, but they only apply to experienced users who are doing unconventional tricks with picture boxes; generally speaking, unless using a picture box as the receiver of a buffer, keep `AutoRedraw` on.)

Another thing worth mentioning here is progress bars - if you're using a progress bar to track image processing code, _don't refresh it for every pixel or even every line_.  Refreshing a progress bar is almost as slow as refreshing an image, so if you must use a progress bar then refresh it every 15-20 lines to minimize its impact on your code.

**7. Optimize your variables.** Because graphics programming can involve many variables, here are some tips for avoiding bad variable usage:
	
  * _`Variants` are very slow_.  Do not use `Variant` types unless absolutely necessary.  They're slow to access, slow to calculate, they take up a lot of memory, and you can almost always find a way to write code that doesn't require them.  (Another thing worth mentioning is to never declare your variables like this: `Dim x, y as Long.` In this example, VB6 will declare `x` as a `Variant` and `y` as a `Long`. The proper programming technique is: `Dim x as Long, y as Long`.)
  * _Limit your use of floating-point variables_.  Generally speaking, `Singles` and `Doubles` are slower, `Longs` and `Integers` are faster.  In every Visual Basic case I've researched (there are exceptions in other languages, particularly ASM, and under different hardware configurations), floating-point/decimal math is slower than integer/whole number math.  Therefore, avoid decimals if possible.  For example, `Red = Red * 1.5` may be slower than `Red = (Red * 15) \ 10`.
  * _`Longs` are fastest_.  Because VB6 was designed for 32-bit systems, it heavily favors `Long`-type variables.  This means that in most cases, `Long` variables will be executed faster than `Integer` or `Byte` variables - and significantly faster than `Single`, `Double`, or `Variant` ones (typically ~3-5x faster than `Single` ones, and moreso for the other data types).  Use `Longs` unless you absolutely need to conserve memory by using `Integers` or `Bytes`.  (This is especially important for looping variables; because they get accessed so many times, always use `Long`-type variables for your loops.  [VBFibre - the famous VB optimization site](http://www.persistentrealities.com/vbfibre/index.php?category=3&item=13&t=vbfibre) shows the difference between using a `Single` and a `Long` as `For...Next` variables.)
  * _Avoid type conversions_.  Regardless of what type of variable you use, keep it consistent.  When you intermix variable types, any programming language slows down - a line like `Integer = Long` requires VB to temporarily change `Long` into an `Integer`, and that takes time.  (Note: this doesn't apply to DIB section arrays - they must always be of type `Byte`.)

**6. In-line optimization: fix your math.** In-line optimization refers to optimizing your code one line at a time. This often involves using faster math functions and better programming techniques. There are many tips I could list under this category, but here are some of the most critical math optimizations you can do for VB6 code:
	
  * _Watch for dividing code_.  Two points here: 1) when possible, use \ instead of /. You may not know this, but these functions are different in VB6.  Backslash represents integer divide - it ignores any decimals that arise from the division, while frontslash allows for decimal math.  If you're only interested in the integer results of division, use backslash.  It will be faster.  2) Don't divide if you don't have to.  Dividing is the slowest of the four basic math functions so avoid it if you can.
  * _Avoid calling functions and subs within `For/Next` or `Do/While` loops_.  Though convenient, functions and subs in VB6 are slower than manually inserting that code into the loop.  The slow-down generally isn't noticeable unless you're calling functions from within a loop, because then the speed loss is accentuated thousands of times over.
  * _Lengthy math equations take a lengthy time to process_.  Short lines of math allow the compiler to better optimize their order and purpose.  One giant line of code might impress your friends, but VB6 can't optimize it nearly as well as a bunch of smaller lines.

For a much more in-depth discussion of VB optimization techniques, visit VBFibre at [http://www.persistentrealities.com/vbfibre/index.php](http://www.persistentrealities.com/vbfibre/index.php).  Every VB6 programmer should spend some time there - it's the most accurate and well-explained information ANYWHERE about VB6 optimizations.  Phenomenal site, donate if you can.

**5. Use look-up tables.** Few things can speed up code as dramatically as a look-up table.  For those who don't know, consider the following code example (used to invert a pixel's color):
    
    For x = 0 to 99
    For y = 0 to 99
    
       'Color = GetPixel()… goes here
    
       'RGB extraction goes here
    
       R = 255 - R
       G = 255 - G
       B = 255 - B
    
       'SetPixel()… goes here
    
    Next y
    Next x
    
For every pixel, VB has to do three 'Subtract' functions. This is bad coding - for this simple 100x100 picture example that's over _30,000_ 'Subtracts.'  Try the following code instead:
    
    Dim LookUpTable(0 to 255) as Byte
    
    'Fill the look-up table with every possible color value and it's corresponding inverted value
    For x = 0 to 255
       LookUpTable(x) = 255 - x
    Next x
    
    For x = 0 to 99
    For y = 0 to 99
    
       'Color = GetPixel… goes here
    
       'RGB extraction goes here
    
       R = LookUpTable(R)
       G = LookUpTable(G)
       B = LookUpTable(B)
    
       'SetPixel… goes here
    
    Next y
    Next x
    </code>

With this code, VB only does 256 'Subtracts' and then uses the table of values to change R, G, and B for each pixel.  This makes a big difference in execution time - so use look-up tables every chance you get.

(There is one disclaimer associated with look-up tables in VB6: unless you follow step 10 of this tutorial (particularly the "Remove Array Bound Checks" option), look-up tables can accidentally slow down code that works on small images.  Note that the steps of this tutorial are in order for a reason!)

An excellent example of look-up tables can be found in this [real-time brightness sample program](https://github.com/tannerhelland/vb6-code/tree/master/Brightness-effect/Part%204%20-%20Even%20faster%20DIBs).

**4. Forget about `PSet` and `Point` - use the API.** If you haven't read the previous three sections of these tutorials, now is the time to do it.  `PSet` and `Point` are terrible choices for per-pixel image processing.  Use `GetPixel` and `SetPixel`/`V` for a huge speed increase.

**3. Forget about `GetPixel` and `SetPixel`/`V` - use DIB sections.** While `GetPixel` and `SetPixel`/`V` are nice, they're still slow.  DIB sections (or BitmapBits) will give you significantly better results.

**2. DIB Sections do better in streams.** If you read these tutorials in order, you'll remember that tutorial three discussed how to declare an `ImageData()` array.  Specifically, a method like `Redim ImageData(0 to 2, 0 to Width, 0 to Height)` is used.  While this creates an easy-to-use array, its possible to speed it up by declaring it differently.  `Redim ImageData (0 to (Width * Height * 3))` gives us an array the _exact same size_ as the first statement, but we use only one dimension instead of three - making our array more than 3x faster for VB to access (and for large arrays, the gain can surpass 10x).  The only problem with this is that we can no longer access direct pixels or colors, but for many graphics functions (like the 'Invert' example on (5), or brightness, or contrast, etc.) we do the same thing to every color within a pixel so it doesn't matter.  For example:
    
    For x = 0 to (Width * Height * 3) - 1
       ImageData(x) = 255 - ImageData(x)
    Next x

would invert an image just the same as the example in optimization (5).  The reason I call this method a "stream" is that we treat the image as a continuous stream of values, not as separate pixels or colors. For a more in-depth example of this, see the [real-time brightness sample program](https://github.com/tannerhelland/vb6-code/tree/master/Brightness-effect/Part%204%20-%20Even%20faster%20DIBs).

(One additional disclaimer is in order: make sure to read **Section VI: the infamous 4-byte alignment issue** in the previous tutorial.  Image streams must be declared in a way that adheres to this rule, which limits them to working on images whose width is a multiple of 4.)

**1. If you do all this and your program is still too slow, try something extreme.** I hate to say it, but if you've done everything above and your program is still too slow, you may be out of luck with traditional methods. Here are some advanced techniques you might consider:
	
  * _Consider switching to SafeArrays._ This archive from the old [Students of Game Design](http://web.archive.org/web/20070629111052/http://www.studentsofgamedesign.com/vb_safearrays.php) site is an excellent tutorial detailing the structure and use of "SafeArrays", the internal VB format for arrays.  SafeArrays won't give you a speed increase in editing your array information, but they will get and set pixel information faster than `GetDIBits` and `Set`/`StretchDIBits`.  If your code requires a large amount of getting and setting pixels, SafeArrays may give you the performance boost you need without a lot of extra coding (as they are structured almost identically to the arrays returned by `GetDIBits`).
  * _Look into assembly language extensions._ [Planet-Source-Code](http://www.planetsourcecode.com/) has several excellent programs by Robert Rayment demonstrating how to use ASM (assembly language) within VB to create graphics routines slightly faster than traditional VB methods. Assembly language is often the fastest programming language available to Windows programmers (next to machine language, but you don't want to write that :) ), and with some clever work you can use it within your VB6 program.  Be forewarned, however, that this is most definitely not an easy thing to do - but it may give you a little extra speed.
  * _Search the net for 3rd party SDKs or ActiveX controls dealing with graphics (DirectX, OpenGL, ActiveX controls, etc.)_.  In almost every case, DirectX, OpenGL, or similar SDKs (software development kits) won't help your per-pixel graphics code to be any faster.  They may, however, provide you with hardware support for your effect.  For example, DirectX provides hardware acceleration for gamma correction, which will be much faster than trying to perform gamma correction in code.  Also, you could buy a VB-compatible OCX or DLL written in another language that does your effect for you.  This can, however, be an expensive option.
  * _Learn another programming language._ The sad but true fact is that some other programming languages provide faster graphics programming techniques via pointers and other tricks.  Even java contains many powerful image editing routines as part of the language, so if you're really desperate than you can try learning (or rewriting your project) in another programming language.  Also, if you rewrite your routine in C/C++ you could compile it into a DLL and use that from VB, should you want to.
  * _Go to the library and check out some graphics programming books._ Some of my favorite programming techniques were learned from non-VB graphics programming books.  Even if you don't understand the code associated with a book, you can still learn a lot about different filters, optimization routines, etc.  If your library doesn't have anything good, search Amazon.com - you'll be amazed at how many graphics programming books are out there.
  * _Use your imagination._ Sometimes the best optimizations are written by programmers who aren't planning on writing a good optimization.  Your ingenuity is your best programming tool - try to think of new, clever ways to speed up your code. If you think up something great, be sure to let me know about it!

As a demonstration of many of these techniques, feel free to check out my [open-source photo editor](https://photodemon.org), which uses these techniques (and many more) to achieve Photoshop-like levels of performance in VB6.

And that, my friends, this is the end of these tutorials.  It's taken me many, many hours to write these up, so I hope you've gained something from reading them.  If you have any comments, questions, suggestions, ideas for future tutorials, or want to send me a generous donation, visit [my contact page](contact).

Happy programming!
