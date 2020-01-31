---
author: tanner_h
date: 2013-02-13 01:24:44+00:00
excerpt: The next PhotoDemon release (5.4) will include support for multiple languages, with French, German, and Dutch (Vlaams) officially supported at release.  I would love to include official support for additional languages.  If you are fluent in a language other than English, please consider contributing a new translation!
layout: post
slug: official-photodemon-language-support
title: 'Coming to PhotoDemon 5.4: Language Support.  Translators welcome!'
redirect_from:
 - /4793/official-photodemon-language-support
---

**Note: this is an old article!  [PhotoDemon now has its own website at photodemon.org](https://photodemon.org).**

Today I made an interesting discovery: my PhotoDemon release dates are slipping further and further apart.

  * PhotoDemon 4.3 - 10 August 2012
  * PhotoDemon 4.4 - 21 August 2012 (11 days later)
  * PhotoDemon 5.0 - 21 September 2012 (31 days later)
  * PhotoDemon 5.2 - 28 November 2012 (68 days later)
  * PhotoDemon 5.4 - ...? (76 days and counting)

If I throw together a quick chart for the delay between releases, a clear trend emerges:

![Not my favorite correlation...](images/release_delays-600x285.png)

According to the chart, I still have a good for or five months available to work on the next release...

Actually, PhotoDemon 5.4 is rapidly nearing completion!  My excuse for this latest delay is a good one, and I imagine you already inferred it from the title of the article... but in case you didn't:

**The next PhotoDemon release will include support for multiple languages, with French, German, and Dutch (Vlaams) officially supported at release.**

Language support has been a monster to implement on account of the large amount of text in the project, not to mention classic VB's utter lack of usable translation libraries.  As a result, an entirely novel language engine was written from scratch, with (quite lovely) XML files being used to supply the actual translation data.

To give you an idea of the scope: as part of the translation process, I wrote a separate program whose sole purpose was to extract all necessary text from the PhotoDemon source code so that a "master" language file could be assembled.  According to it, PhotoDemon contains almost 1400 unique phrases, with a total of more than 7800 words.  Every one of those phrase occurrences needed code added to handle the actual text substitution, and then there's the obvious challenge of the translation itself.

Fortunately, I didn't tackle this project alone.  An absolutely amazing contributor by the name of Frank Donckers contacted me with the initial prototype of the translation engine, and it is Frank who is supplying the French, German, and Dutch translation text.  I could not have built this feature without him - so thank you, Frank!

At present, the translation engine is pretty much complete in terms of base functionality - all program text is translated on the fly, and the user is free to change languages at run-time at their leisure (no restart required!).  The [coding solution behind this](https://github.com/tannerhelland/PhotoDemon/blob/master/Classes/pdTranslate.cls) is quite elegant, if I might say so, and users shouldn't experience any noticeable performance hit while a translation is active.  The only noticeable delay might be an additional second or two of start-up time on older machines, on account of the translation XML file being loaded and parsed.  I've got some ideas for speeding up this process, however, so even that delay may disappear by release time.

**I would love to include official support for additional languages.  If you are fluent in a language other than English, please consider contributing a new translation!**

No programming experience or specialized software is required to translate.  I've got a master translation file ready to go - all that's needed is to plug in the translated text in whatever language you might speak.

![Here is how the French language file looks.  All a translator needs to do is place a translation between the translation XML tags - easy peasy!](images/translation_notepadpp_sample-600x433.png)]

Here is how the French language file looks in the free Notepad++ editor.  All a translator needs to do is place a translation between the translation XML tags - easy peasy!

If you're familiar with XML or HTML, you can see how simple the translation document is.  Each phrase consists of original text and translated text, and that's all there is to it.  The lines in green are just comments added for convenience, in this case comments written by the language extraction tool.  Translators can safely ignore these.

Before wrapping up, I should mention one rather large caveat with multiple language support - at present, only "ANSI" ([Windows-1252](http://en.wikipedia.org/wiki/Windows-1252)) languages are supported.  I apologize for this, but one of the problems with classic VB is its inability to handle unicode characters without major hacking - and by major hacking, I mean replacing every user interface aspect of the project, as well as every string library.  If I ever port PhotoDemon to another programming language (something I often consider), Unicode support would be much more feasible, but I'm afraid it's not on the present roadmap.

I need at least a couple more weeks to hammer out a few remaining issues with version 5.4, which leaves plenty of time for any ambitious translators out there to pitch in and contribute a new translation before release day.  If it helps, note that your name will be visibly displayed as the translator in not only the language source file, but I'll also add you to the special thanks section of the program, the PhotoDemon website, and the README file.

I can always be reached via [this contact form](contact) - so that's the place to go if you're willing to help.  Thank you in advance!
