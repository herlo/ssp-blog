---
title: 'Packaging Update: pydf now in Fedora'
author: herlo
layout: post
date: 2011-07-22T16:52:01+00:00
url: /2011/07/22/packaging-update-pydf-now-in-fedora/
categories:
  - Fedora
  - Filesystems
  - Guru
  - Tech
  - Tools
tags:
  - 2011
  - Fedora
  - july
  - pydf
  - Tools

---
Recently, my friend [beandog][1] introduced me to [**pydf**][2]. After playing with it for a couple of days, I decided I liked it enough that I packaged and included into Fedora. _(If you are interested in other packages I maintain, you can check them out [here][3].)_

## What is pydf?

$ yum info pydf

<address>
  Name             : pydf<br /> Arch               : noarch<br /> Version          : 9<br /> Release         : 3.fc15<br /> Size                : 14 k<br /> Repo              : updates<br /> Summary       : Fully colorized df clone written in python<br /> URL                : <a href="http://kassiopeia.juls.savba.sk/~garabik/software/pydf/">http://kassiopeia.juls.savba.sk/~garabik/software/pydf/</a><br /> License          : Public Domain<br /> Description   : pydf displays the amount of used and available space on your file systems,<br /> : just like df, but in colors. The output format is completely customizable.
</address>

I was also able to send in a patch for the python 2.4 version to the upstream author. He was very happy to receive and apply the fix. The patch is also available in the [source rpm][4].

A nice looking screenshot of the output from pydf is below:

[<img class="alignnone" title="pydf in action" src="{{<siteurl>}}misc/pydf.png" alt="" width="512" height="225" />][5]

Cheers,

herlo

 [1]: http://wonkabar.org/
 [2]: http://kassiopeia.juls.savba.sk/%7Egarabik/software/pydf/
 [3]: https://admin.fedoraproject.org/pkgdb/users/packages/herlo
 [4]: http://kojipkgs.fedoraproject.org/packages/pydf/9/3.fc15/src/pydf-9-3.fc15.src.rpm
 [5]: {{<siteurl>}}misc/pydf.png