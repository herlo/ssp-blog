---
title: A man/less Trick
author: herlo
layout: post
date: 2007-04-13T16:00:26+00:00
url: /2007/04/13/a-manless-trick/
categories:
  - Tech
  - Tools

---
I regularly use man pages. I also regularly use **less** to view files I wanna read.

$ man vsftpd.conf

$ man named.conf

$ man less

$ less README

$ less CHANGES

and so on and so forth. But one of the most annoying things about the default setting to **less**. The one that I wonder what the devs were thinking when they created this application, is the way that it works by default. When I exit from one of my man pages, or when I finish reading a document using **less**, I discover that the page has disappeared. Gone!

No text! Zip, nada, buh-bye!

_**Annoying!!**_

So today in class, one of my students asked me if there was a way to fix this problem. I said that I thought there was, but couldn't remember the option. I found that switch and thought that others might like to know as well.

The option is -X. If you run _man less_ you will find it in the **OPTIONS** section. The only trick is, I didn't want to create an alias for it, but rather wanted it to be the default. Luckily for me, there is an environment variable called **LESS** that I can set, so that's what I did.

I added the following to the bottom of my ~/.bashrc file:

export LESS=&#8221;-isXf&#8221;

and I modified my /etc/man.config file to match:

PAGER /usr/bin/less -isXf

Now, when I hit the **q** button either in a man page or when I less a text document, the content stays on the screen. Very nice!

Cheers,

Herlo