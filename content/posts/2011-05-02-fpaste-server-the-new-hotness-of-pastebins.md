---
title: 'Fpaste-Server: The new hotness of pastebins'
author: herlo
layout: post
date: 2011-05-02T17:51:07+00:00
url: /2011/05/02/fpaste-server-the-new-hotness-of-pastebins/
categories:
  - Collaboration
  - Community
  - django
  - Fedora
  - Releases
  - Tech
  - Tools
tags:
  - django
  - epel
  - Fedora
  - fpaste-server
  - packaging
  - rpm
  - Yum

---
If you have been on the internet for a while, you probably have seen or been told to use a [pastebin][1] when submitting large amounts of text or code in IRC. If not, you may have used a [pastebin][1] to show your buddy the code you are working through and getting advice.

My point&#8230;

# PASTEBINS ARE EVERYWHERE

One of the pastebins that has been in use for a very long time is <http://fpaste.org> and the focus of my post today. Essentially, the Fedora community tends to use fpaste.org over other pastebins as it [has a bunch of nice features][2] and it's Fedora branded. About 2 months ago, I was asked by [Jonathan Steffan (aka daMaestro)][3] if I would be interested in packaging fpaste.org's code and get it into Fedora infrastructure (FI). I accepted that challenge.

As Jonathan will tell you, the code was hacked together over a weekend at a coffee shop. Thus, it needed a bit of clean-up to make things work without including libs from other projects (a big no-no when packaging a Fedora rpm). After a few weeks of clean-up and back-and-forth with Jonathan, fpaste-server was born. That was the first big step to get fpaste-server into FI.

Fpaste-Server is comprised of many other packages. Since I wasn't the maintainer on many of them, I worked with the amazingly awesome [Dave Riches (dcr226)][4] to get [django-mptt][5], [django-tracking][6], [django-simple-captcha][7] and [django-dpaste][8] into the [EPEL repositories][9] for both EL5 and EL6. Dave was not only helpful, but went above and beyond to complete these builds. Thank you, sir!

Over the past month, I've been really busy, prepping for my wedding and what not, but found some time recently to finish the package builds of fpaste-server. The packages are all approved, save for el5 which was submitted this morning. This was the second big step to get fpaste-server into FI.

This week, and after my honeymoon, I plan to finish up the work to get fpaste-server into FI. All that's really left is to get django-tracking into EPEL6.

If you haven't tried fpaste-server yet, you should. It's a pretty cool and stable pastebin, it's also very hackable. Changing out the background to fit your own logos and such is very simple. Please comment here if you find any bugs or issues, have questions or comments.

Cheers,

Herlo

&nbsp;

 [1]: http://en.wikipedia.org/wiki/Pastebin
 [2]: http://fpaste.org/about/
 [3]: http://damaestro.us/
 [4]: http://fedoraunity.org/Members/dcr226
 [5]: http://koji.fedoraproject.org/koji/packageinfo?packageID=11856
 [6]: http://koji.fedoraproject.org/koji/packageinfo?packageID=11095
 [7]: http://koji.fedoraproject.org/koji/packageinfo?packageID=11075
 [8]: http://koji.fedoraproject.org/koji/packageinfo?packageID=11855
 [9]: http://fedoraproject.org/wiki/EPEL