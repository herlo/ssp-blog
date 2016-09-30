---
title: Fedora Activity Days 1-3 – A \'Frank (aka Francis) the Fedora pwnie\' report
author: herlo
layout: post
date: 2010-02-02T01:44:03+00:00
url: /2010/02/01/fedora-activity-days-1-3-a-frank-aka-francis-the-fedora-pwnie-report/
categories:
  - Community
  - FAD
  - Fedora
  - Tech
  - Tools
tags:
  - audio
  - events
  - fad
  - Fedora
  - freeseer
  - fudcon
  - planning
  - recording
  - streaming
  - video

---
It appears to me that the weekend in Raleigh went rather well.  Even with the difficult weather conditions on Saturday into Sunday morning, I feel the result was a 'smashing' success!  There were so many things being accomplished that I couldn't keep track of them all.  I will try to make a fairly complete list of the events of the weekend, and what we accomplished overall.

## Friday, January 29 – Day 1

Gathered at Red Hat's main office, we brainstormed in a manual 'tag cloud' kind of way.  Mel had us all take sticky notes, write upon them based upon a few words on the white board and then, stick them to said white board appropriately.  This got our minds going about what a FUDCon or FAD should be, why it was important and the things that could really be improved.  I felt very happy about the amount of ideas that were shared on these sticky notes.  it was quite cathartic to get out the things that always had bugged me or I thought needed improvement in our Events.  I have a few pictures of us doing this process, enjoy them.

After spending about 1.5 hours doing this and discussing it, we broke into separate groups, the FUDCon 2.0 folks (upstairs) and FUDCon Live folks, aka me, Yaakov, and the freeseer folks online (downstairs).  My main target was to get the freeseer application working with completely free software and build the AV Kit from components I had, plus the ones that Mel had purchased for this project.

After getting downstairs with Dennis Gilmore (he was my helper for the first hour), we quickly discovered that one component, the Epiphan vga2usb device, was not working.  After a bit of digging, we also discovered that it had a non-free driver and that it would likely not be easy to find a free driver alternative.  We did, however, attempt to build the binary they provided, but kept getting errors.  More on this later on (or in another post), so stay tuned.

I spent the next few hours trying to get everything else up and running, doing research to find a different alternative for video output from a VGA source to USB input.  _heffer_ joined us on IRC and gave me some good links as to where I might look for a Scan Converter and a easyCAP device.  While a little lower quality, the Linux drivers for it are completely open and free, so I set out with a plan to find one in Raleigh.

At 4pm, Max and I headed out on the town, hunting down several items, including firewire PCMCIA adapters (for our miniDV camera) and the Scan Converter components.  We needed to get a screw driver and some other firewire adapter stuff too, we headed to CompUSA. Though normally I wouldn't go there, but this CompUSA had actually been converted from a Tiger Direct, so I thought we had a chance.  After about 1.5 hours of failure, we ended up with two firewire cards and some audio cables, we headed off to see Avatar in 3D.

## Saturday, January 30 – Day 2

After leaving Avatar, we discovered a nice big blanket of snow had come down in Raleigh.  Just 2-3 inches, and in Utah, we'd think nothing of this, but here it's quite a bit different.  First off, North Carolina doesn't seems to have the infrastructure, no plows or ice melt, to really deal with something like this kind of storm.  There were news reports of it on every station, the Governor called for a state of emergency, and I just thought it was odd.  Because of this, it was determined that we would not leave the hotel for Day 2 of the FAD.  Instead, we reserved a room in the hotel and worked from there.  Luckily, the hotels infrastructure, plus the Days Inn next door provided us with our networking needs, while Max stayed at his apartment and called in using Fedora Talk.

My work was to spend as much time with the [FreeSeeR][1] folks and do tons and tons of testing of their code, plus provide feedback and gstreamer pipelines to get us closer and closer to our eventual goal.  Thanh had spent a lot of time while we were at Avatar to turn FreeSeeR into an API.  He also altered the code to put the gui into a more sensible tool, with both Qt and Gtk implementations.

About half way through the day, I discovered that I had accidentally left my power adapter for my audio mixer in Max's car (he was 15 minutes way with no snow and at least 25 with), essentially eliminating my high quality audio testing.  Luckily Chris Tyler had a headset with a microphone and Dennis Gilmore had a webcam we could use because the firewire cards were a bit flaky and kept crashing my kernel.

By the end of the night, with some tweaking by Dennis and I, we had FreeSeeR working with DV input, USB video input, 1/4&#8243; audio input and were able to output to an ogg file with reasonable quality and consistency.  A lot of testing later, and we were able to determine that we still needed to tweak some of the code to provide for a better way to adjust audio and video settings prior to recording.  All in all, the FreeSeeR software is coming along very nicely.  Andrew Ross and Thanh Ha have been doing an amazing job and I really appreciate their help working on getting this working.  The new version of FUDCon Live thanks you as well, because without this, we won't be able to provide our users with a good quality remote experience.

## Sunday, January 31 – Day 3

The sun is shining, but for some reason, the roads are still not that clear.  Several cars are still having difficulty climbing the incline out of the Best Western to the main road, which is now melting, but still very snow covered.  Today, we discover that we've met one major part of our goals, the [Fedora Pony][2] has been created!!  We must thank Robyn Bergeron for creating, Frank, the Fedora Pwnie.  Now mind you, Francis is really her name, but she's such a tomboy that, well, you just can't call her that, she doesn't enjoy it too much.  So we call her Frank.

In addition to our major goal above of a Pony, the [FUDCon Live][3] team has done some amazing work.  Yaakov has been working on the FUDCon Live document with Mel, while I was working with the FreeSeeR guys to get their git repo moved over to f[edorahosted.org][1], which is awesome!  I've been given commit and sponsor rights to the repo, so we'll start getting more developers involved right away.  Have a look at the screenshots of the GUI if you'd like to see what FreeSeeR can do.

Jon Stanley and I discussed the possibility of moving fedorahosted.org over to [gitolite][4], and discovered that Jesse Keating has been experimenting with it himself, so this might be something we can do in the near future.  While we currently appear to use gitosis, gitolite gives us the ability to set ACLs on a particular branch, which then can help keep the master branch cleaner.  To help illustrate this, there's [a very great article on nvie.com][5] which explains a git branching system which can really make development and commits very clean and easy to track.  Gitolite can help with this, so I'm going to be experimenting with it this coming week.

I spent the rest of the day writing up the [AV Kit][6] wiki page along with Mel.  I stubbed it out, and she added a big section regarding the modules in the AV Kit.  I then rewrote much of that to cover the two styles of AV Kit we'll be building over the next month or two.  In fact, I plan to have one complete in time for the [Marketing FAD][7] in March, where they can use and test it out.  I really hope to get some good feedback on it and improve FreeSeeR some more using these upcoming events as testing grounds.

Currently, I'm on a plane which I didn't think would take off tonight, headed home for Salt Lake City.  I'm excited to see my sweetie and get some much needed sleep.  As much as I enjoy hanging out with my Fedora friends and working on projects like this, it really wears me out.  I'm ecstatic at the amount of work we accomplished though, and am very appreciative to Paul, Jon, Chris, Denis, Dave, Mel and Max, plus all the folks online for their hard work this weekend.

FUDCon 2.0 is alive and kicking, FUDCon Live will make it just that much better.  Watch for upcoming posts in the near future regarding FreeSeeR and the Fedora AV Kit and how everything is going to work.

Cheers,

Herlo

 [1]: https://fedorahosted.org/freeseer/
 [2]: http://img27.imageshack.us/i/ponies.jpg/
 [3]: https://fedoraproject.org/wiki/FUDCon_Live
 [4]: http://github.com/sitaramc/gitolite
 [5]: http://nvie.com/archives/323
 [6]: https://fedoraproject.org/wiki/Audio_Video_Kit
 [7]: http://fedoraproject.org/wiki/Marketing_FAD_2010
