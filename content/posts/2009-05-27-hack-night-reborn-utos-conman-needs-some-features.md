---
title: 'Hack Night Reborn: UTOS-ConMan needs some features'
author: herlo
layout: post
date: 2009-05-27T23:20:55+00:00
url: /2009/05/27/hack-night-reborn-utos-conman-needs-some-features/
sociableoff:
  - 'false'
categories:
  - Community
  - Conferences
  - django
  - Fedora
  - HackNights
  - News
  - Tech
tags:
  - conman
  - django
  - hacknight
  - python
  - scalereg
  - utos
  - UTOSC

---
So, you don't know what I am talking about?  Not sure where this is all leading?  Well, if you are interested in learning [Python][1] and [Django][2] or are an artistic hacker, we need you.

Last year, we started a project called [utos-conman][3].  This project in about 3-5 months became the system that ran the speaker approval process, speaker listings, sponsor display, etc. for the [Utah Open Source Conference 2008][4].  In 2009, we're looking to make some improvements that will take us one step further to the ultimate open source [conference management system][5].  Whether that statement is true or not, I want to push forward some goals for utos-conman.

To start off with, I worked this year with the [Southern California Linux Exposition (SCaLE)][6] to get their scale registration system open sourced and available.  It is now available, thanks Lei, and it can be checked out using svn from the google code project site.  This is exciting, and I'm happy to have the SCaLE code available because it provides a very powerful registration system, which includes the ability to create tickets, coupons, promotions, add-ons, reporting, check-in and much, much more.

### Goals

The goals for this year's Hack Night are going to be two fold, because now we have two projects.

First, let's talk about _scalereg_:

  * Porting to Django 1.0 **(completed, patch coming)**
  * Adding back the validation and form management that was removed to get to Django 1.0
  * Adding a new theme for UTOS, we hope to make this generic enough to let anyone add some css and images

Next is _utos-conman_:

  * Working toward reusable app status.  Making it easier to integrate with apps like scalereg
  * Adding volunteer management
  * Adding better room management
  * Adding upload feature to the sponsors admin section
  * Integrating video and audio links

I'd like to take a moment to thank all the folks who've worked on these projects over the years and I look forward to having an awesome code base.  There are many many more features that we'll be looking at in the future, including reporting, auditing and off-line capability.  For now, I'm more interested in making things work and getting it up and running.  In the next month or two, I hope to have a full-fledged registration system in place for the Utah Open Source Conference 2009.

Cheers,

Herlo

 [1]: http://python.org
 [2]: http://djangoproject.com
 [3]: http://code.google.com/p/utos-conman
 [4]: http://2008.utosc.com
 [5]: http://blog.utos.org/2009/05/12/conferences-management-tools/
 [6]: http://www.socallinuxexpo.org/