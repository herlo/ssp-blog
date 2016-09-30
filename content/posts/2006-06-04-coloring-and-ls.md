---
title: Coloring and ls
author: herlo
layout: post
date: 2006-06-05T04:28:18+00:00
url: /2006/06/04/coloring-and-ls/
categories:
  - Tech
  - Tools

---
So I was recently teaching the RH033 course in Phoenix, Arizona, when one of my students asked me what the colors meant when running ls -l from their prompt. I knew that the command had been aliased, and that it was actually running 'ls -l –color=tty' and I explained this to her, and that's what I showed. Here is what she got when she ran alias:

> [student@station9 ~]$ alias
  
> alias l.='ls -d .* –color=tty'
  
> alias ll='ls -l –color=tty'
  
> alias ls='ls –color=tty'
  
> &#8230;snip&#8230;

As you can plainly see, I found exactly what I expected. When running ls, she had actually been loading colors by default when in a terminal. &#8220;But how do I know what the colors mean?&#8221;, she asked. That's what prompted me to write this blog entry, what do the colors actually mean?

So we did some looking online and discovered that the colors actually derive from the file /etc/DIR_COLORS. This file, all fine and dandy, can be found on most any system (that I have checked, let me know if you don't find it somewhere) and allows ls –color[=WHEN] to display appropriate colors for certain types of files.

Inside this file, the colors themselves consist of three numerically valued parts; attribute, text color, and background color. Attributes are such things as bold or underscore. Text color and background color should be quite clear. I have included a quick list from the config file:

> Attribute codes: 00=none 01=bold 04=underscore 05=blink 07=reverse 08=concealed
  
> Text color codes: 30=black 31=red 32=green 33=yellow 34=blue 35=magenta 36=cyan 37=white
  
> Background color codes: 40=black 41=red 42=green 43=yellow 44=blue 45=magenta 46=cyan 47=white

If we were to make symbolic links bold with blue text and a yellow background, we might do something like so:

> LINK 01;34;43

There you go, now we know how the colors and attributes are represented. Below is a quick breakdown of the default colors and attributes in RHEL4:

> NORMAL 00 – If a format doesn't apply, do this one, black text on white background.
  
> FILE 00 – Normal file, black text on white.
  
> DIR 01;34 – Directory, bold blue text on white.
  
> LINK 01;36 – Symbolic link, bold cyan text on white.
  
> FIFO 40;33 – Pipe, yellow text on black.
  
> SOCK 01;35 – Socket, bold magenta on white.
  
> BLK 40;33;01 – Block device driver, bold yellow on black.
  
> CHR 40;33;01 – Character device driver, bold yellow on black.
  
> ORPHAN/MISSING 01;05;37;41 – Orphaned syminks and the files the orphans point to bold blinking white on red. (No need wasting two lines here)
  
> EXEC 01;32 – Files with executable permissions, bold green on white.

There are many many more file types and extensions which are defined in this file, but most of them follow this general rule. Please go ahead and review them if you are interested in learning more. In fact, I have included my DIR_COLORS file for your perusing pleasure at the bottom of this post.

**Important note**: Order is not important with regard to the attributes and colors as the examples above show. It is also possible to apply multiple attributes to a specific file type, this is important when you want to show a file blinking and bold, for instance.

A couple more details remain unsolved however. One is applying default colors, the other is how to change your personal colors while not affecting the defaults(or if you don't have root access). Lets address these&#8230;

**Loading Default Colors into the Environment**

Just because you changed your /etc/DIR\_COLORS file doesn't mean that the new colors take affect, in fact user interaction is expected. One more step must be taken to make the colors take effect. This step can be done in many ways, however, the quickest is to load them into the environment of your current shell. To do this, make the changes you desire in /etc/DIR\_COLORS, then type the following command:

> [student@station9 ~]$ eval \`dircolors -b /etc/DIR_COLORS\`

This command calls dircolors, which displays the environment variables needed for coloring ls to standard out. By wrapping eval around the outside, the DIR_COLORS variable gets loaded into the current shell environment. You now have a new system color scheme.

Other ways of getting the scheme working do exist, including logging out and back in as well as rebooting, but this scheme appears to be the fastest and most reliable. Also be aware that the next time any user logs in, these new colors will automagically take affect, pretty cool, huh!!

If you run &#8220;echo $LS_COLORS&#8221; from your command line before and after executing the line above, you should be able to see the applied changes.

**Individual User Color Schemes**

As you might wonder, well now I have my defaults set for coloring, but what if users want to change their own color schemes? Well, lucky for your users, their is a simple way. Just copy the /etc/DIR\_COLORS file (its world readable) to .dir\_colors of the users $HOME directory like so:

> [student@station9 ~]$ cp /etc/DIR\_COLORS ~student/.dir\_colors

Once this is done, the user student should now be able to change their colors as described above, using this new .dir_colors file.

**Final Note**

Here is a before and after comparison of the ls coloring I did on my box. I have included several different types of files which should give a good sampling of the changes I have made from the default.

> **_Before_** ([default DIR_COLORS][1])
  
> <span class="imagelink"><img id="image33" alt="lsbefore.png" src="{{<siteurl>}}uploads/2006/06/lsbefore.png" /></span>

> **_After_** ([modified DIR_COLORS][2])
  
> <span class="imagelink"><img id="image34" alt="lsafter.png" src="{{<siteurl>}}uploads/2006/06/lsafter.png" /></span>

 [1]: {{<siteurl>}}uploads/2006/06/DIR_COLORS "DIR_COLORS"
 [2]: {{<siteurl>}}uploads/2006/06/DIR_COLORS.after "DIR_COLORS after"