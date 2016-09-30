---
title: 'GoOSe and Skein: The road to 2.0'
author: herlo
layout: post
date: 2011-11-20T23:32:14+00:00
url: /2011/11/20/goose-and-skein-the-road-to-2-0/
categories:
  - Fedora
  - GoOSe
  - Python
  - Tech
tags:
  - 2.0
  - 2011
  - features
  - GoOSe
  - November
  - python
  - skein

---
<address>
  As some of you may already know, I've been a part of this <a href="http://gooseproject.org/">enterprise rebuild project</a> for a while now and things have been going pretty well.
</address>

As I have been working on getting the import functionality into [skein pre2.0][1], there are a few features that have come to mind as I go along. It's very interesting to see these features appear once the tool is out in the wild. Some of them have come from other users/contributors and some from my brain, but here's a dump of what I have been considering adding to skein:

  * [skein revoke][2] – (this one is from imak, and quite a good idea) It's possible to accidentally request a repo that you didn't mean to request. skein revoke will allow you to specify that you erred and will allow you to close the request with a nice message you provide.
  * [skein request from an SRPM][3] – the above request brought forth something I'd been thinking about doing, but hadn't really formalized. I suspect this feature will be a good bit of our automation in our second push to finish GoOSe 6.0 by year's end.
  * skein update – providing this feature will probably happen **after** 2.0. The plan would be to allow an already existing repo to be updated to a new release or version of an SRPM. In addition, it's possible the update will be to a new branch, which update should be able to handle.

As for the rest of the features, the code for export was just finished today. I expect to be able to finish push, upload and import by the end of this coming week. Then it will be on to importing the rest of the upstream tree and building GoOSe 6.0

Cheers,

Herlo

 [1]: https://github.com/gooseproject/skein/tree/new_workflow
 [2]: https://github.com/gooseproject/skein/issues/7
 [3]: https://github.com/gooseproject/skein/issues/8