---
title: 'GoOSe Project: Progress toward Skein 2.0'
author: herlo
layout: post
date: 2011-11-10T23:34:35+00:00
url: /2011/11/10/goose-project-progress-toward-skein-2-0/
categories:
  - Fedora
  - Geek
  - GoOSe
  - Guru
  - Tech
  - Tools
tags:
  - 2011
  - Community
  - enterprise
  - GoOSe
  - November
  - rebuild
  - skein
  - Tools

---
As some of you may already know, I've been a part of this [enterprise rebuild project][1] for a while now and things have been going pretty well. Recently, though, I've made some good progress on our import and build tool, [skein][2].

Skein's goal is provide easy functionality for rebuilding SRPMS from upstream and import them into github, where they can be built using our [koji instance][3]. The process is actually easier than one might think:

  * skein request – Request a particular repository be setup on our github organization for the specified package. The package itself should be able to be requested from the SRPM, but that feature is not yet available.
  * skein query – To verify the request has been placed, this shows the open queries (by default).
  * skein show – For a particular request, show the detail of who requested and the purpose of such a request.
  * skein grant – Only an admin can grant the repository. Only members of the admin team on our github organization can grant the repository.
  * skein extract – Once granted, the SRPM can be extracted and placed into two basic directories:
  * /path/to/package/lookaside/ – contains the archive from the SRPM, usually a tar, tar.gz or zip file. The contents of this directory can then be pushed to the lookaside cache.
  * /path/to/package/git/ – contains the spec file, any patches and other sources that are not archives. A Makefile and sources file are also generated along with a .gitignore to provide useful functionality during the koji build

Other functionality is currently under development:

  * skein push – Once extracted and committed to the git repository, this pushes the git commits to github.
  * skein upload – Once extracted, this uploads the content of the lookaside directory to the lookaside cache at pkgs.gooselinux.org.
  * skein import – A combination of skein extract, push and upload, since that seems fairly logical.
  * skein build – Albeit mostly complete, it will need to be tested with an SRPM that has been run through this process.

I took a few minutes the other day and created a video of the completed process. I post this here for others to use for their benefit, but also so I can have it in another place besides my laptop.

[Skein video][4]

Cheers,

Herlo

 [1]: http://gooseproject.org
 [2]: https://github.com/gooseproject/skein
 [3]: http://koji.gooselinux.org
 [4]: {{<siteurl>}}misc/skein_qd.webm