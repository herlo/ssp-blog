---
title: 'POW: bash-completion – Bash Auto Completion in Fedora using yum (and more)'
author: herlo
layout: post
date: 2007-10-24T15:29:19+00:00
url: /2007/10/24/pow-bash-completion-bash-auto-completion-in-fedora-using-yum-and-more/
categories:
  - Bash
  - Fedora
  - POW
  - Tech
  - Tools
  - Yum
tags:
  - Bash
  - Fedora
  - POW
  - Yum

---
In an attempt to consistently blog, I am starting a new series here on fedora-tutorials.com. Program of the Week (POW). Hopefully, this will excite and inform all of us about the cool programs available in Fedora. So see you next Wednesday for another program.

Over the past year or so, I've been on the hunt for several things that I find in other Linux distros that I cannot find in Fedora. Its not very common, but on occasion I do run into something that's not there on Fedora. One of them was the ability to automagically complete many of the command lines for many things.

One of them, and probably one of the biggest, was the fact that yum did not have tab completion for available packages. Today is my lucky day! While chatting and helping my students with their labs today, one of them mentioned to me that he could tab complete a particular command on his box. I of course inquired, because it interested me, as to the package name. It turns out my bash tab completion dreams were just about to come true! He told me about this amazing package that would let me use tab completions for things like the **service** command, **man** and of course, **yum**.

I was blown away! So immediately after this discussion, I started searching for this elusive package I've never heard of before. Sure enough, as he informed me, _bash-completion_ does exist and does some amazing things. After hunting around a little on google, here's some of the stuff I found. I'll also include the links at the bottom of this post.

as root try this: (note [Tab] means you should hit the tab key)

> <pre># service ht[Tab]</pre>

What you'll notice is that one of three things happen. If you've got the _bash-completion_ package installed already because you're ahead of the game, it should auto-complete for you. Without bash-completion, this doesn't happen, but its also possible that since bash already has some completion in place, it might auto complete a directory for you, but that's definitely not what you want.

If you've not already installed bash-completion, I'd suggest you do it now. On Fedora 7, run the following command:

> <pre># yum install -y bash-completion
..snip..
Installed: bash-completion.noarch 0:20060301-3.fc7
Complete!</pre>

Now that _bash-completion_ is installed, we need to invoke the tools. Normally, this is not needed, and a reboot/re-login will take care of this as well, but since I wanted to use this right away, I did the following as an unprivileged user:

> <pre>$ source /etc/bash_completion</pre>

This doesn't seem to do much, but its actually quite powerful. The source (or .) will load the environment variables from the _/etc/bash_completion_ script into my current environment. Luckily for us, when we now log into root, _/etc/bashrc_ will accomplish this for us without any intervention. To test that it worked, try running the following command as the same unprivileged user:

> <pre>$ unalias[Tab]
&lt;tab>&lt;tab>.=     ll=     ls=     vi=     which=&lt;/tab>&lt;/tab></pre>

Note that when I pressed <tab> twice, a list of the currently available aliases appeared. Nice ey? Let's complete this:</tab>

> <pre>$ unalias w[Tab]</pre>

Now produces:

> <pre>$ unalias which</pre>

And completes the string as expected. Now we're getting somewhere! But why did I really want to explain this?

<big><big>Oh yeah! <strong>yum</strong></big></big>

With _bash-completion_, yum can now provide us with a list of available packages, similar to the auto completion capability in _apt-get_ or _aptitude_ from Ubuntu or Debian. Say for instance you want to see all of the packages available for install that match what you're looking for, but don't want to run **yum list** or **yum search** because, in truth, it just takes to long! Now you have an alternative:

> <pre># yum -y install bal[Tab]&lt;tab>&lt;/tab></pre>

Produces:

> <pre>ballbuster.i386  ballz.i386       balsa.i386</pre>

Adding another 'lb' to the end of that string (and then the tab key of course) should help us to complete to the package we'd like to install.

> <pre># yum -y install  ballb[Tab]</pre>

Then completes to:

> <pre># yum -y install  ballbuster.i386</pre>

Hitting enter then installs the ballbuster package, and its quite a fun game!

> <pre>.. snip ..
Installed: ballbuster.i386 0:1.0-1.fc6
Dependency Installed: ClanLib.i386 0:0.8.0-4.fc7
Complete!</pre>

Of course, there are hundreds of others tab completions available (and there's a good way to list many of them too, even if its a bit cryptic). Try these on for size:

Are you a developer?

> <pre>$ svn c[Tab]
cat checkout  ci     cleanup   co     commit    copy    cp
$ make [Tab]
all clean dist-clean</pre>

What about a systems administrator?

> <pre># modprobe -r b[Tab]
battery    bay        blkcipher  bluetooth  bridge     button</pre>

> <pre>$ man cron[Tab]
cron     crond    crontab</pre>

> <pre>$ ssh herlo[Tab]
herlo-f7   herlo-lap  herlo.org</pre>
> 
> <pre>$ grep --[Tab][Tab]
 --after-context=  --directories=   --invert-match   --only-matching
 --basic-regexp    --exclude=       --label=         --perl-regexp
.. snip ..</pre>

To help you wade further through, try out the following two commands:

  * <pre>complete -p</pre>

  * <pre>declare -f</pre>

Be aware that these are advanced components and can really be confusing if you're not a developer and just want to use the features. The _complete_ command seems to provides some tools to do additional auto-completion. I also think that its nice to be able to extend this functionality to other applications as well.

As promised, here's a few links to help your completion introduction. **Note**: Some of these links provide more than just the simple tab completion:

  * <a href="http:/http://www.caliban.org/bash/index.shtml#completion" target="_blank">http://www.caliban.org/bash/index.shtml#completion</a> – The GNU page on bash-completion, still needs more.
  * <a href="http://www.keyboardcowboy.co.uk/bash-completion/" target="_blank">http://www.keyboardcowboy.co.uk/bash-completion/</a> – Provides some interesting scripts to improve your bash-competions
  * <a href="http://www.debian-administration.org/articles/316" target="_blank">http://www.debian-administration.org/articles/316</a> – An introduction to bash completion: part 1