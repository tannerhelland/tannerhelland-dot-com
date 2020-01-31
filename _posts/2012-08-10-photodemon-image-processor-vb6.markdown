---
author: tanner_h
date: 2012-08-10 17:36:34+00:00
excerpt: I've spent 12 years working on an advanced image processing program.  The software is now available under the title "PhotoDemon."  It is fast, free, completely open-source (BSD licensed), and it provides a number of useful features, including macro recording and automated batch conversion.  It's completely portable - meaning it doesn't require installation - and it has no external dependencies.  I'd love to get your feedback on it.
layout: post
slug: photodemon-image-processor-vb6
title: 'Announcing PhotoDemon: A Fast, Free, Open-Source Photo Editor and Image Processor'
redirect_from:
 - /4183/photodemon-image-processor-vb6
 - /4183/photodemon-image-processor-vb6/
---

**Note: this is an old article!  [PhotoDemon now has its own website at photodemon.org](https://photodemon.org).**

![PhotoDemon screenshot](images/PhotoDemon_Sample-600x376.jpg)

*PhotoDemon v4.2 in the midst of a massive batch conversion (1643 files)*

**tl;dr - I've spent 12 years working on an advanced image processing program.  (Think PhotoShop, but without any on-canvas painting tools.)  The software is now available under the title "PhotoDemon."  It is fast, free, completely open-source (BSD licensed), and it provides a number of useful features, including macro recording and automated batch conversion.  You can [download it here](https://photodemon.org/download/).**

I can't often say that a blog post has been 12 years in the making... but believe it or not, this post has taken me that long to write.

Many years ago, when I was but a lowly high school student, I legitimately believed that I alone could produce the world's greatest video game.  It was going to be epic in every possible way - immersive 3D graphics, fully orchestrated musical score, hundreds of pages of witty dialogue.  I was going to program the whole thing myself in Visual Basic 6.0, and it was going to be AWESOME.

(ROFL)

This might shock you, but that game never came to fruition.

Fortunately, my delusional teenage aspirations weren't entirely a waste - I did end up writing [many hours of original music](music-directory) for the game, and I also produced a suite of useful development tools.  One of those tools was called the _GenesisX Image Studio_, after my one-man _GenesisX Production Company_.  (Yes, that name sounded cool to my teenage mind.)  The purpose of _GenesisX Image Studio_ was to convert 24-bit image files to the game's custom 8-bit _Genesis X Format_.

Perhaps you recall, but back in the year 2000 bandwidth was hard to come by, and distributing a game chock full of large 24-bit images over the Internet simply wasn't feasible.  GIF images were still under patent protection so there were concerns about using them, and PNG wasn't widely known or supported.  So I decided to write my own image format, and this was the program capable of converting JPEGs and BMPs to that:

![GXF Compressor screenshot](images/GXF_Compressor_screenshot.jpg)

Here's a screenshot of the GenesisX Image Studio. I know - it burns the eyes a little.  Don't you love the red/black gradient?  It seemed so edgy at the time.  (facepalm)

While the GXF Compressor was hideous to look at, it included some interesting code, including a rather clever interactive palette editor.  That palette editor was at the heart of the _Genesis X Format_.  It worked by taking 256-color images and blending low-frequency colors at a ratio of their occurrences within the image.  This way, it was possible to get a 256-color image down to 128 colors or less with very little degradation; the image would then be RLE compressed and optionally zLib compressed, and it was capable of producing downright tiny files.

![GXF Palette Editor](images/GXF_Palette_Editor.jpg)

The GenesisX Palette Editor.  I'm not sure why I felt the need to plaster a bright red copyright message on the form... I'm fairly certain no one was interested in stealing my painfully amateurish code.

When the ultimate game project associated with this software died, I continued to peck away at the image studio, mostly because I enjoyed learning about image processing and the software already provided a framework for things like loading and saving images, zooming and scrolling them, and a rudimentary set of filters.  Over time, I eliminated the 256-color feature set and focused only on 16 million color support.  Eventually the ridiculous "GenesisX" moniker was dropped, and the project was renamed "DemonSpectre Image Workshop."  (DemonSpectre was my online alias at the time.)

![DemonSpectre Image Workshop](images/Demonspectre_Image_Workshop-600x391.jpg)

By 2002, the project had become slightly less hideous.  The red/black gradient was replaced by the blue/black gradient made famous by InstallShield, and a thoroughly useless logo was added to the left-hand side.  The code base also grew to include a variety of new filters and processing techniques.

In 2002, Microsoft introduced the first version of Visual Studio .NET, effectively obsoleting the COM-based VB6 overnight.  I was in university by then, and had become very aware that VB was not the right language for a programmer who wanted to be taken seriously in the U.S. job market.  So I learned C++, java, and Perl, though I retained a love for classic VB, in large part because it was the language that got me into programming in the first place.

The next 8-9 years saw slow, incremental upgrades to the software, usually the result of a random night or weekend when I was fed up with work and needed to focus on something not-work-related.  Eventually I renamed the software "VB Photoshop" (no copyright problems there!), then later PhotoDemon, a mash-up of my old DemonSpectre moniker and the fact that the software had grown to focus primarily on photo editing.

In fact, my interest in digital photography led to many of the program's best features, since I used PhotoDemon to implement tools that other image editing programs lacked or implemented poorly.  (I'm looking at you, PhotoShop batch conversion!)  Since its inception, PhotoDemon also served as a testbed for my image processing work in other programming languages, because for all its flaws, classic VB is unbeatable as a rapid prototyping language.  I still use it for first-implementation tests of obscure features or filters, simply because I can go from pseudocode to real-time implementation in minutes (versus hours in java, and days/months in C).  And because VB6 compiles down to native code (unlike the interpreted "P-code" of earlier versions), it's perfect for prototyping image processing code, which often needs to execute in real-time.

![PhotoDemon v4.2 menu screenshot](images/PhotoDemon_v4.2_Menu_Screenshot.jpg)

PhotoDemon has come a long way from its original _GenesisX Image Studio_ roots.  The current version looks quite nice, and it includes features I find lacking in other software - such as extensive accelerator ("hotkey") support.  For those who don't utilize accelerators, the menus are designed to maximize discoverability.  IMO they're a significant improvement over most image editing software menus.

Because I continued to receive a surprising amount of traffic to my VB-oriented programming site, I would periodically strip interesting features out of PhotoDemon and publish them independently.  In fact, most of [my open-source programming projects](programming-directory) are merely subsets of PhotoDemon's codebase.  (And it's a surprisingly large codebase - over 30,000 lines - and that's not including the 3rd-party DLLs it relies on for extra functionality.)

Every now and then, I'll receive an email from a poor programmer who's stuck supporting a legacy VB6 application and has consequently stumbled across my site.  These emails always brighten my day, and they're the reason I still provide VB6 projects despite the language being "dead" for more than 10 years.  (Although "dead" is a relative term - Microsoft's extended support lasted until 2008, and they have promised "it just works" compatibility for VB6 applications [FOR THE LIFETIME of Windows 8](http://msdn.microsoft.com/en-us/vstudio/ms788708.aspx).  I know people have their criticisms of Microsoft, but no major tech company is half as good as they are when it comes to supporting legacy software.  Hats off to Microsoft for that.)

Occasionally, these emails will ask me if I have a single project that condenses my many image processing techniques into a single piece of software.  For ten years, my response to this question has been a vague, teasing, "maybe I do - you'll have to wait and see!"  I'm not sure why I've never just tell people about PhotoDemon... probably because they would pester me for copies of the code, and I hate sending out .zip files of large source directories, especially when I haven't made up my mind about how I want to license said code.  

But this summer, as I was sending out yet another one of these vague email responses, it struck me that I'd spent the past ten years hinting at PhotoDemon but never really thinking seriously about when it might live somewhere besides my hard drive.  Wasn't it time to seriously commit to getting the project in a workable state?  (Anyone who knows me shouldn't find this surprising - my motto has always been "better late than never," and boy does this project meet that definition!)

So I committed, then and there, to getting PhotoDemon into a workable state.  My last three months have been spent cleaning up its code base, stripping out useless functions and features, writing documentation, and coaxing it to work with modern Windows visual styles - no small feat, considering VB6 never worked with _Windows XP_ visual styles, let alone Windows 7.

![PhotoDemon current version screen shot](images/PhotoDemon_v4.2_Sample-600x376.jpg)

*PhotoDemon, as it looks in August 2012.  Note the use of Windows 7 visual styles, along with full MDI support.  Also - no hideous background gradient!  :)*

Because I'm a glutton for punishment, I also got PhotoDemon working with modern version control software.  ([Here it is on GitHub](https://github.com/tannerhelland/PhotoDemon).)  I wonder if I'm the first person to try and get a massive VB6 codebase working properly with Git...  Surprisingly, it does work, though it takes some tweaking thanks to VB's strange intermixing of text and binary files.  Maybe someday I'll document what I did.  Then again, maybe not - I'm not sure I want people trying to set up legacy VB projects with GitHub, lol.

After getting the code to a pleasantly robust state, I put up a [preliminary project page](https://photodemon.org) for PhotoDemon on this site.  That was six weeks ago.  Thus far it seems to have been well-received among the VB programmers who frequent my site, and with the help of those programmers, many miscellaneous bugs have been squashed.  After a rigorous few weeks of testing, I think PhotoDemon is finally stable enough to warrant broader use.

And that's why this blog post exists.

Over the next few weeks, possibly months, I plan on releasing a series of "developer diaries" that discuss PhotoDemon's features and design in detail.  I don't know many projects with a 12-year development time that spans from the developer first learning to program to becoming a professional coder, and I think my experiences could be useful for other young programmers looking to embark on their own open source project.  Also, some of PhotoDemon's more advanced capabilities - such as macro recording and playback - represent unique design challenges, and I think it could be worthwhile to discuss the implementation hurdles I faced in hopes of helping other programmers build such features right on their first try.

![PhotoDemon v4.2 print dialog](images/PhotoDemon_v4.2_print_dialog.jpg)

PhotoDemon's current interface aims to find that sweet spot between minimalism and power.  For example, here's the print dialog.  I find most print dialogs to be woefully over-engineered, so this one provides only the options I use on a regular basis.  Also, I just noticed that the "Orientation" label is misaligned vertically.  D'oh!  Better go fix that...

But for now, here's what's worth mentioning: PhotoDemon is stable, and I'd love your feedback on it.  It's designed as a portable app, meaning no installer is required.  Just download the .zip, extract it, and run PhotoDemon.exe.  (Not a Windows user?  PhotoDemon should work with [the latest stable release of Wine](http://www.winehq.org/download/).)

Input is welcome from programmers and non-programmers alike.  To download the full app, use this link:

**[Download PhotoDemon](https://photodemon.org/download/)**

If you want the program AND its complete source code, download it from PhotoDemon's GitHub page:

**[Download PhotoDemon (with complete source code)](https://github.com/tannerhelland/PhotoDemon)**

A GitHub account is not required.  Simply click the "ZIP" button with the cloud-and-arrow icon to download the source in standard VB6 format.  (The ZIP button is just below the project description, in the top-left quadrant of the page.)

Issues can be submitted from the "Help" menu within PhotoDemon, or by visiting [the Issues page](https://github.com/tannerhelland/PhotoDemon/issues?sort=comments&state=open), or by simply [sending me an email](contact).

Stay tuned for posts describing PhotoDemon's (quite large) feature set in detail, as well as in-depth guides for its advanced features, including macro recording and batch conversion.  

Finally, note that PhotoDemon is updated regularly.  I tend to make commits on at least a weekly basis, and often more frequently than that.  For the most up-to-date version of the software, download it from GitHub.

Thanks for your interest, and I hope you enjoy the software.