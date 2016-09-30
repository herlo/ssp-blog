---
title: 'Flying through RPM Builds with Koji: Pass #1 Results'
author: herlo
layout: post
date: 2011-12-09T21:16:33+00:00
url: /2011/12/09/flying-through-rpm-builds-with-koji-pass-1-results/
categories:
  - Fedora
  - GoOSe
  - Koji
  - skein
  - Tech
tags:
  - 2011
  - December
  - koji
  - RPM Building
  - skein
  - statistics

---
Well, it looks like we're just about finished with **Pass #1** to build all of the imported SRPMs we can from upstream. The GoOSe Project results are looking good.

### Build statistics from 2011-11-01 through 2011-12-09

<address>
  Completed Builds: 658<br /> Failed Builds: 296
</address>

It appears that a bit more than 1/3 of the builds failed and notifications are going out to the package owners. This means we can work through each of them and resubmit them. Odds are that most of them are due to dependency issues and only a few for other reasons.

We're preparing for **Pass #2** this weekend. We've discovered some interesting things, however, so here's something we'll be putting in place first (hopefully):

### A repository to track BANNED and EXCLUDED (for now, other names may arise) SRPMs.

At the moment, there are SRPMs we cannot build because we don't support an architecture (s390, for example) There is no reason to build packages that won't work. There are also some packages that contain proprietary content we need to scrub, even though the license states they are free software. These packages will have to wait unless they affect a critical path of getting GoOSe 6.0 composed in coming weeks.

The plan here is to create a repository to track these banned / excluded SRPMs. Skein will query this git repository for the BANNED and EXCLUDED files to make sure any request, grant, or build actions first check to make sure the package is not in either list. If the package is in the list, skein will refuse to act upon the package and the requester will have to resolve the issue before attempting again.

Watch for the updated skein v2.1 with this fix in place in the very near future.

Cheers,

Herlo