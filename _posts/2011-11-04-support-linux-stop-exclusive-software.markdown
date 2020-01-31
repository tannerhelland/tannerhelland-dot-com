---
author: tanner_h
date: 2011-11-04 23:46:54+00:00
excerpt: I sometimes see Linux users complain because their favorite Linux-only project
  decides to go cross-platform.  Decide to provide a Windows downloader for your project,
  and you can bet the trolls will come calling.  "You're betraying Linux," they'll
  claim.  "I refuse to support you now!"  Please, developers - ignore these people.
layout: post
slug: support-linux-stop-exclusive-software
title: Support Linux by Not Writing Linux-Only Software
redirect_from:
 - /3772/support-linux-stop-exclusive-software
---

[Phoronix ran a story today](http://www.phoronix.com/scan.php?page=news_item&px=MTAxMTU) about the keynote address at this year's [Fedora India Conference](http://fedoraproject.org/wiki/FUDCon:India_2011).  The speech can be viewed in its entirety [here](http://urtalk.kpoint.in/kapsule/gcc-076d796f-9740-4628-8022-3e8811cfa366#tab_Bookmarks), but one quote in particular is drawing attention:

> The number one enemy we have today is ourselves. And I mean that with all seriousness. Too many times we shoot ourselves in our own foot, by the way we act, the way we deal with people, in our narrowminded-ness that we develop.

The quote and ensuing explanation appears around the 44:00 mark.  It's worth a watch.

This is a great quote not just for Linux developers and contributors, but for Linux users as well.  It's especially interesting coming from a Fedora project leader, considering the Fedora project is well-known for its [very myopic rules about included software](https://fedoraproject.org/wiki/Forbidden_items).  (FYI - Fedora does not include any proprietary software, including proprietary drivers, Adobe Flash, Skype, etc.  Is that an example of "shooting yourself in the foot"...?)

In this article, I'm not going talk about the obvious "Linux is its own worst enemy" topics.  Plenty of other people are more qualified to talk about hardware support, FOSS jingoism, obnoxious users, design problems.  No, I'd like to mention something more obscure, but still deserving of attention:

Developing software exclusively for Linux.

**Linux-exclusive software should be the exception, not the rule**

One of the Linux-centric software projects I've followed over the past several years is the [OpenShot Video Editor project](http://www.openshotvideo.com/).  I first discovered OpenShot while researching Linux video editing software in 2009 for a series of Ubuntu articles.  At the time, I considered OpenShot the best choice for default video editor in Ubuntu 10.10.  Canonical eventually went with Pitivi instead, a decision I and many others wondered about.  To quote [one article on the topic](http://everydaylht.com/2010/05/02/ubuntu-makes-another-poor-technology-choice-battle-of-the-movie-editors/):

> In my view, Ubuntu is doing desktop Linux a huge disservice by putting in basic, buggy tools and then advertising its product as having “video editing” capabilities. The short point is that it hasn’t, and users moving to Ubuntu on the basis of this promise will be bitterly disappointed, tainting their overall view of Linux.

Canonical later rethought this decision; in 11.10 [they removed Pitivi from the default install](http://www.omgubuntu.co.uk/2011/05/pitivi-to-be-removed-as-default-app-in-ubuntu-11-10/).  The reasoning behind the decision?  According to the linked article:

> The lack of ‘polish’ and maturity to the application was also highlighted, with one attendee wondering whether its ‘basic’ nature impacted negatively on the perception of the Ubuntu desktop as a whole.

Ironic, eh?

I don't mean to slam Pitivi.  [Collabora](http://www.collabora.com/), the company who funds Pitivi's development, is an incredible contributor to the open-source world and they employ a team of [very talented developers](http://www.collabora.com/about/who-we-are/).  Seriously - they just released a demo of [a video editor built entirely in HTML5](http://mbatle.wordpress.com/2011/11/02/illusions-in-the-web-a-real-time-video-editor-built-in-html5/).  They're incredible.

But writing desktop video editing software is tough, especially video editing software provided for free.  Pitivi continues to grow and improve, but it simply wasn't ready for the big-time in 2009.  That's okay.

Anyway, OpenShot continues to improve at an impressive rate.  In late 2010, OpenShot crossed what I consider the "maturity line" for an open source project - it began work on [a Windows port](http://www.openshotvideo.com/2010/09/openshot-windows-challenge.html).  The response to this was mixed, as always.  Many users realized the benefits of making OpenShot cross-platform.  Some, unfortunately, did not.  As one commenter said:

> When I've seen projects that aim to be multi OS, the Linux version is always the second hand version. More people use Windows so new features are added to the Windows version and no one gives a shit about the Linux users. I have seen it many times, haven't you?
> 
> Why not just use all the time for the Linux version to make it as great as possible. There are already more than enough video editors for Windows anyway.

This is a valid concern.  Take [Songbird](http://en.wikipedia.org/wiki/Songbird_%28software%29), for example.  Songbird started out as a promising cross-platform media player with top-tier Linux support.  This lasted four years, until the team made the hard choice to [completely drop Linux](http://blog.songbirdnest.com/2010/04/02/songbird-singing-a-new-tune/).  It was an unfortunate loss, but it's hard to fault the Songbird developers.  They're a small team and audio support in Linux has never been simple to work with.  (FYI, [untested nightly builds are still available](http://developer.songbirdnest.com/builds/trunk/latest/) for adventurous users.)

But I would argue that projects like Songbird are the exception and not the rule.  While it may seem like Linux-only projects are betraying their loyal base by developing Windows or OSX versions, I would argue that cross-platform development is actually better for Linux as a whole, better for individual software projects and their developers, and ultimately better for Linux users.

**Cross-Platform Software Removes One of Linux's Biggest Barriers of Entry**

It's been said a million times before: one of the hardest things about switching from Windows to Linux is learning new software.  This has gotten easier over time; after all, modern users are probably using the same browser on Windows that they would on Linux, and mature open source projects like LibreOffice, Pidgin, GIMP and Inkscape provide a similar experience regardless of which OS you use.  As we move to a world where more and more software lives within the browser, the switch will get even easier.

But when a new Linux user can't find a Linux version of software that he or she is used to (Adobe products, MS Office, etc), they suddenly have a very good reason to give up on the platform as a whole.  Even if a Linux alternative is better than whatever they were using before, the fact that it _isn't familiar_ is often enough to scare them away.

The typical answer to this is: "everything would be better if Adobe and Apple and Microsoft and everyone else just released Linux versions of their software."  I agree.  That _would_ be better.

But does anyone really think this is going to happen?  Do you really envision a day when you can buy a copy of Microsoft Office for Linux?  I'm afraid I don't.

So if we can't force companies to release their software on Linux, we have to do the next best thing - take the best of Linux software and make it available on other platforms.  In the last five years, projects like Firefox and Chrome have done way more to improve Linux adoption than the Linux-only competitors of Epiphany and Konqueror - not because either of those projects are crap (just the opposite, they're great), but because creating software only for Linux users doesn't help people make the switch.

Now please don't misunderstand.  I am **absolutely not** saying that projects like Epiphany and Konqueror are stupid, or that they don't serve a purpose, or that they are hurting Linux.  Both are mature, well-written, technical accomplishments from talented contributors, and they definitely fill a niche.

But when it comes to making Linux a viable competitor to OSX or Windows, Firefox and Chrome are the ones to thank.

_(Note: yes, I realize that webkit came from KHTML which came from Konqueror.  This doesn't invalidate my point.)_

In the perfect world, Linux users would have access to all the same software as Windows and OSX users.  Releasing a Windows and OSX port of your awesome Linux-only project is a step toward making that happen.

**As a Developer, You Will Get More Donations, Support, and Feedback from a Cross-Platform Release**

Let's return to the Songbird example.  In [the team's blog post about why they dropped Linux](http://blog.songbirdnest.com/2010/04/02/songbird-singing-a-new-tune/), they provide the following chart "for perspective":

![songbird](images/songbird_chart.jpg)

It's hard to argue with those numbers.  Yes, in certain areas (like translations) Linux users contributed more on a per-user basis than Windows or Mac users.  But not that much more.  When you factor in the difficulty of working with audio in Linux, you can see why the Songbird team made the tough decision to drop Linux support entirely.

This same pattern shows up elsewhere.  For gamers, [consider the Humble Indie Bundle](http://www.geek.com/articles/games/linux-users-pay-3x-that-of-windows-users-for-humble-indie-bundle-3-2011082/) - Linux users donated 3x more money, per user, than Windows users.  That's an awesome statistic.  But the sad reality is that there are tons more Windows users, and for the Humble Indie Bundle that meant that revenue from Windows users _as a whole_ was significantly larger than revenue from Linux users.

I point this out only to show that open source developers can receive many benefits - financial and otherwise - from releasing software on as many platforms as possible.  And if you as a developer get more feedback and more money, that will help you produce better software for everyone who uses your products - including your loyal Linux fanbase.

**This Isn't a Major Problem, But It's Something to Consider**

Is Linux-only software the biggest problem facing the open source community?  Hell no.  It's probably not in the top 10 or 100 or 1000 problems.  But I do think it's something to point out, especially for Linux projects that seem perpetually close to becoming "great"... only never quite getting there.  Several examples come to mind.

[Calligra](http://en.wikipedia.org/wiki/Calligra) (formerly KOffice) is a promising open-source office suite developed by KDE.  Personally, I think the project is way ahead of LibreOffice in key areas, particularly the interface.  Consider their word processor, which is one of the few designed with widescreen monitors in mind:

![Calligra Words screenshot.  Note the very nice use of horizontal real estate.](images/KOffice_Words_Screenshot-600x422.jpg)

I'm not a Linux software developer, but I would love to contribute to the Calligra project as a tester.  My problem?  I spend most of my time in Windows, and I need a word processor that works in both OSes.  Calligra's Windows version is in [a perpetual state of disarray](http://userbase.kde.org/KOffice/Download#Windows), and I don't want the hassle of running my word processor in a VM.  How many testers and contributors is this very cool project missing out on because there is no Windows port?  Would a complex piece of software like LibreOffice or Inkscape be half as good if it had remained Linux-only?  I doubt it.

As another example - Linux video editors.  We're finally reaching a world where Linux video editors are stable and usable (kudos to the excellent [Kdenlive](http://www.kdenlive.org/) team and OpenShot, among others), but it has taken far, far too long to get here.  In my opinion, the biggest problem is that most major Linux video projects have remained Linux-only.  Kino and Cinelerra have always been in desperate need of testing and feedback, and by ignoring Windows they aren't doing themselves - or their faithful Linux users - any favors.

**Disclaimers**

Now I realize that you can't just click a magical button that makes your Linux-only project compile under Windows and OSX.  I get that.  If you're an individual developer who doesn't have the time or the resources to test and compile your code for Windows, I totally understand.  Some projects don't make sense multi-platform, and sometimes there are very good technical reasons why a project doesn't make an OSX or Windows version available.

But if you haven't considered cross-platform support, please do.  Look for help on developer forums or IRC.  Talk to Windows packagers of other open source projects.  Follow OpenShot's example and ask your userbase for help.  Just don't fool yourself into thinking that you are helping Linux by _not_ providing Windows and OSX versions of your software.

Because you're probably not.  By releasing your software for as many OSes as possible, you are not betraying Linux or open source.  You are helping it.  If people think Linux represents a small fraction of overall users now, imagine how much worse it would be if _less_ cross-platform software were available.

As for my fellow Linux users: please don't troll developers when they decide to go cross-platform.  FOSS is not just about developing for Linux.  Open source can - and should - work to increase the freedom of all users, everywhere, regardless of what operating system they use.  When your favorite piece of Linux software decides to release a Windows version, don't think of it as betrayal.  Think of it as a way to advertise the benefits of open source to your heathen, Windows-using friends.

As always, I am extremely grateful to the talented individuals that use their time and talents to provide open-source software for free.  Thanks for all your hard work.
