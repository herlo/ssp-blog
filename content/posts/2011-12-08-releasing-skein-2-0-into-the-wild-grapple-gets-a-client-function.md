---
title: 'Releasing skein 2.0 into the wild – Grapple gets a client function'
author: herlo
layout: post
date: 2011-12-09T00:04:50+00:00
url: /2011/12/08/releasing-skein-2-0-into-the-wild-grapple-gets-a-client-function/
categories:
  - Collaboration
  - Community
  - Fedora
  - GoOSe
  - Koji
  - RPM
  - Tech
tags:
  - 2011
  - December
  - github
  - GoOSe
  - koji
  - RPMs
  - skein

---
The [GoOSe Project][1] has [been very busy][2] [over the past][3] [two weeks][4]. This evening, after dinner, I will be releasing [skein 2.0][5]. It's major functionality will be documented and placed in the [RELEASE.rst][6] file on github. Essentially, the request, query, grant, import and build functionality is what makes this **2.0** and ready to use.

The best part about this tool is, while I have been working on it, almost all of the remaining SRPMS have been imported and the majority of them have been built on our koji server. Right now, we're on the [last batch][4] and I expect it to finish sometime late Friday or early Saturday (12/10/2011). This ends our first major hurdle to getting an Alpha release of GoOSe Linux 6.0 out the door.

Another huge tool in this process is [Grapple][7], written by [python master Nafai][8], (aka Travis Hartwell). He spent a good bit of time getting this [github hook][9] in place that will record all git commits and help to process them automatically. I spent a bit of time and added a client script to grab the recorded commits and send them on to koji automatically with the proper dist value and url. No more guessing! This is the 'automagic' corollary to skein build.

Next up, I plan to rebuild the [failed builds][10] and push them through koji again, using skein build. Possibly doing this a few more times until we get things pared down to the packages that don't just have dependency problems. I hope to have most of those fixed up and in place by Monday or Tuesday next week (12/12/2011).I've also noticed a few builds that will never build for our arches, so I will have to figure out what to do with them for now.  I don't want to waste koji resources trying to rebuild them when I know they will never work.

The first Alpha ISO is getting close enough to taste it now! We'll have to make sure to have a grand celebration upon our first Golden GoOSe Release :)

Cheers,

Herlo

&nbsp;

 [1]: http://gooseproject.org
 [2]: http://github.com/gooselinux/
 [3]: http://koji.gooselinux.org/koji/tasks?state=all&view=tree&method=all&order=-id
 [4]: http://koji.gooselinux.org/koji/tasks?start=300&state=all&view=tree&method=all&order=-id
 [5]: https://github.com/gooseproject/skein/tree/master
 [6]: https://github.com/gooseproject/skein/blob/master/RELEASE.rst
 [7]: https://github.com/gooseproject/grapple
 [8]: http://the.softwaretoolsmith.com
 [9]: http://help.github.com/post-receive-hooks/
 [10]: http://koji.gooselinux.org/koji/buildsbystatus