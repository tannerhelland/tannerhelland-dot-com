---
author: tanner_h
date: 2013-01-16 15:55:41+00:00
excerpt: I've been investigating common dialog hooking for PhotoDemon,
  as it would allow me to add support for image previewing right in the dialog itself.
  This isn't as necessary in modern versions of Windows (7 in particular includes
  very good image format support), but it can be helpful for unsupported formats like
  RAW photographs.  Unfortunately, several days of research have shown that it is
  not possible to hook a Vista or Windows 7 style dialog and maintain the modern layout...
layout: post
slug: hooking-modern-windows-common-dialogs-notes
title: 'Hooking modern Windows common dialogs: some notes'
redirect_from:
 - /4709/hooking-modern-windows-common-dialogs-notes
---

Background: [common dialog hooking is used to append your own controls to a Windows common dialog box.](http://msdn.microsoft.com/en-us/library/ms646951%28VS.85%29.aspx)

A good friend recently sent me a number of resources related to hooking common dialog controls. I've been interested in common dialog hooking for [PhotoDemon](https://photodemon.org), as it would allow me to add support for image previewing right in the dialog itself. This isn't as necessary in modern versions of Windows (7 in particular includes a number of GDI+ improvements, making Explorer very robust with standard formats), but it can be helpful for unsupported formats like RAW photographs.

Unfortunately, several days of research have shown that it is not possible to hook a Vista or Windows 7 style dialog and maintain the modern layout. Let me explain with pictures:

![This is the standard common dialog control in Windows Vista and 7 (and presumably 8 as well, though I haven't verified this myself).  The biggest improvements over past common dialogs include breadcrumb navigation at the top, a dedicated refresh button, and a persistent search bar.](images/Vista_7_commondialog-600x394.png) 

This is the standard common dialog control in Windows Vista and 7 (and presumably 8 as well, though I haven't verified this myself).  The biggest improvements over past common dialogs include a dedicated left-hand file tree, breadcrumb navigation at the top, and a persistent search bar.

The common dialog above comes directly from PhotoDemon's current common dialog implementation. This is the native common dialog control on Vista and 7. I very much like it. As a comparison, here is the same dialog in Windows XP:

![Same folder as the previous image.  The XP common dialog provides no breadcrumb nav, folder tree, dedicated refresh, or search bar.  Note also how many TIFF formats do not display correctly - including XP not recognizing the MINISWHITE flag on the CCITT TIFF files.  Kinda interesting.](images/XP_commondialog-600x386.png)

Same folder and images as the previous image.  There is no breadcrumb nav, dedicated refresh, or search bar.  Note also how many TIFF formats do not display correctly - including XP not recognizing the MINISWHITE flag on the CCITT TIFF files.  Kinda interesting.

I strongly prefer the Vista/7-style dialog, particularly the breadcrumb nav and the persistent folder tree on the left.

Unfortunately, it is impossible to hook the Vista/7 dialog and maintain the native Vista/7 appearance. If you attempt to hook it, Windows will ALWAYS drop back to a previous generation common dialog. Here are some images to demonstrate, using a basic image preview hook:

![This is what happens when you attempt to hook a dialog, and all you provide is the OFN_ENABLEHOOK flag.  Not pretty (and the hook doesn't even work right).](images/commondialog_hook_1.png) 

This is what happens when you attempt to hook a dialog, and all you provide is the OFN_ENABLEHOOK flag. Not pretty (and the hook doesn't even work correctly).

![Here is the same dialog, but with the OFN_EXPLORER flag set.  Note that hooking now works properly, but the common dialog itself has been reduced to XP style - the left-hand folder tree is gone, and the top bar has no breadcrumbs or search.](images/commondialog_hook_OFN_EXPLORER.png)

Here is the same dialog, but with the OFN_EXPLORER flag set. Note that hooking now works properly, but the common dialog itself has been reduced to XP style - the left-hand folder tree is gone, and the top bar has no breadcrumbs or search.

Note that the image above uses an older version of the OPENFILENAME struct, namely (this is its declaration in VB):

    
    Private Type OPENFILENAME
        lStructSize       As Long
        hwndOwner         As Long
        hInstance         As Long
        lpstrFilter       As String
        lpstrCustomFilter As String
        nMaxCustFilter    As Long
        nFilterIndex      As Long
        lpstrFile         As String
        nMaxFile          As Long
        lpstrFileTitle    As String
        nMaxFileTitle     As Long
        lpstrInitialDir   As String
        lpstrTitle        As String
        Flags             As Long
        nFileOffset       As Integer
        nFileExtension    As Integer
        lpstrDefExt       As String
        lCustData         As Long
        lpfnHook          As Long
        lpTemplateName    As String
    End Type


If you modify the struct to its newest version ([as described here](http://msdn.microsoft.com/en-us/library/ms646839%28v=vs.85%29.aspx)), you can slightly improve the dialog to look like this:

![The newest version of the OPENFILENAME struct enables the places bar on the left.  I don't find this particularly useful - certainly not as useful as a folder pane - but perhaps some might find it preferable.](images/commondialog_hook_OFN_EXPLORER_new_struct.png)

The newest version of the OPENFILENAME struct enables the places bar on the left. I don't find this particularly useful - certainly not as useful as a folder pane - but perhaps some might find it preferable.

That is the best you can get if you want to hook a common dialog in Vista or 7.

Reasons for this have been speculated on by more qualified individuals than I.  [Over at stackoverflow, David H explains](http://stackoverflow.com/questions/4731218/ofn-enablehook-modifies-the-look-of-getopenfilename):

> The reason for this is that MS completely re-organised the file dialogs for Vista. Hooks are used to extend a file dialog by supplying a resource file. This gives the customiser too much power. They can all too easily modify standard elements of the dialog and indeed many apps did so. The reorganisation of the dialogs would have broken many apps that used hooks. Those would have tried to manipulate elements of the dialog that were not there, or were implemented differently. Legacy versions of the dialogs remain for such apps to "get their hooks into".
> 
> You are correct that it is impossible to get the new look when you use a hook. Instead you need to use the IFileDialogCustomize interface to customise the dialog. This is less powerful but does result in appearance and behaviour that is more consistent with the standard part of the dialog.

(More information is available [here](http://social.msdn.microsoft.com/Forums/en/windowsuidevelopment/thread/78382324-9c23-4619-adfd-3cfd0288914e) for those who are interested.)

Unfortunately, I am not aware of any way to access the [iFileDialogCustomize interface](http://msdn.microsoft.com/en-us/library/ms645818.aspx) in classic VB.  If someone knows how, I'd love to hear it.

The take home message of all this is - if you work in classic VB and you want to hook a common dialog, you need to be content with an XP-style dialog.  There is currently no way to maintain a Vista/7 style dialog while hooking.

For this reason, I'm going to stick with the stock common dialog control in PhotoDemon.  I may look at a dedicated "browse" window in the future, which would allow for full image previewing, but I'm afraid such a feature is not on the roadmap for the next few versions.

All hooking-related screenshots were created using [Carles PV's iBMP project](http://www.planetsourcecode.com/vb/scripts/ShowCode.asp?txtCodeId=42376&lngWId=1), which made it very easy to modify various hooking parameters and test the output.  Thanks, Carles!
