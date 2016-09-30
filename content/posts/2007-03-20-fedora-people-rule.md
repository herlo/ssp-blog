---
title: Fedora People Rule!
author: herlo
layout: post
date: 2007-03-21T03:35:12+00:00
url: /2007/03/20/fedora-people-rule/
categories:
  - Passion
  - Tech
  - Tools

---
I was visiting the <a href="http://planet.fedoraproject.org/" target="_blank">Fedora People</a> website when I ran across a post by <a href="http://thorstenl.blogspot.com/index.html" target="_blank">Thorsten Leemhuis</a>.

The content of the post was a quick way to set up notifications using _libnotify_ when someone either shouts your name or says your nick in **irssi**. So I thought I'd give it a try. His is an alteration to the original found <a href="http://lewk.org/blog/2006/05/19/irssi-notify" target="_blank">here</a>.

After about 10 minutes of effort and a little bit of tweaking, I now have a script that will notify me every time someone says my name in **irssi**. It was really easy to setup. His had one little bug which I've fixed, so the new script has been posted below.

Essentially, you need two scripts, the <a href="{{<siteurl>}}uploads/2007/03/fnotify" target="_blank">remote <em>fnotify</em></a>, which needs to be loaded into irssi, and the <a href="{{<siteurl>}}uploads/2007/03/irssi-script" target="_blank">local <em>irssi-script</em></a> script, which should be loaded when you login. I recommend the _~/.bashrc_ file. Refer to the original <a href="http://thorstenl.blogspot.com/2007/01/thls-irssi-notification-script.html" target="_blank">article</a> for helpful details.

Once you've got the scripts downloaded. Take the remote _fnotify_ script and rename it to _fnotify.pl_ and place it in your remote _~/.irssi/scripts_ directory

`$ mv fnotify ~/.irssi/scripts/fnotify.pl`

Then, inside **irssi**, go ahead and run the following three commands:

`/unload perl`
  
`/load perl`
  
`/script load fnotify.pl`

If successful, a message similar to this will appear in your irssi control window:

`21:20 -!- Irssi: Loaded script fnotify`

If any other errors appear when running the _/load_ and _/unload_ operations, it should be okay to continue.

Once this is working, its time to go ahead and start the _irssi-script_ obtained previously.

`$ ./irssi-script`

Once this happens, get someone to say your name in **irssi**. Once they have done so, you should get messages that looks similar to this in the bottom right hand corner of your desktop:

[![ping-script-cool.png][1]][2]

This worked pretty well for me. A few things could work better but aren't too bad. I currently have no way of running the local _irssi-script_ as a service or on login without my _~/.bashrc_ hanging. I'll have to look further into it before I have a solution.

I hope this is useful for you as it was for me.

Cheers,

Herlo

PS – As a quick aside; 15 minutes or so into my research, I also noticed another script at the bottom in the comments that was supposed to be able to do it without the extra startup script. When I tried it, I was getting failures within irssi –something about dbus not working properly.

 [1]: {{<siteurl>}}uploads/2007/03/ping-script-cool.thumbnail.png
 [2]: {{<siteurl>}}uploads/2007/03/ping-script-cool.png "ping-script-cool.png"