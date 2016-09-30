---
title: 'Git Hooks: Making the awesomest RCS ever even better!'
author: herlo
layout: post
date: 2009-10-01T01:35:39+00:00
url: /2009/09/30/git-hooks-making-the-awesomest-rcs-evar-even-bettar/
sociableoff:
  - 'false'
categories:
  - Fedora
  - git
  - Guru
  - puppet
  - Tech
tags:
  - git
  - hooks
  - puppet

---
Over the past month or so, I've been really digging into git.  It's quite the revision control system (RCS) and has some seriously awesome tools to do just about anything with your data.  My latest project has been around my semi-new job at [Backcountry.com][1] as a Senior Linux Administrator.  Essentially, my entire job right now is to automate and make our infrastructure idempotent.  I am tasked with setting up cobbler, puppet, koji and other tools that will make our infrastructure more agile and scalable.

To do this, I've been using a centralized git repository using gitosis and gitweb.  Because it's behind the Backcountry firewalls, there is no easy way to share our repository data.  However, there are some great git repos at [github][2], which I highly recommend.

Anyway, we do the hub-and-spoke model with our git repositories.  Meaning that we have a central repository where much of the data is stored so everyone can get access.  Of course, though, most people clone these repositories and work on the code where they choose.  Because we have several people pushing puppet data to our repository, which has been on subversion until 2 weeks ago, I am keen on making sure the puppet code we push to the central repo is at least syntactically valid.

### Git Hooks: The skinny

Essentially, the key here is to understand is that git, like many other popular revision control systems is distributed.  This means that many people keep repos locally and push to the central repository after many many commits (or just one or two).  Git keeps the history in a clean way and all of the commits are pushed and tracked.  Essentially, we need some way to validate the data coming in from an outside source.  Enter [git hooks][3].

There are several git hooks, but three that are quite critical to this scenario; _pre-commit_, _pre-receive_ and _post-receive_.

The first, pre-commit is specific to the repository where the commit is taking place, such that a validation of the puppet syntax here is useful to help the person writing the puppet rules.

Next is post-receive which is generally useful for sending out emails after a successful push.  It would list the files and the diff of each in an email to those who wish to know about the commit.

And finally, the least documented of the bunch; the one with the least amount of examples, pre-receive.  The pre-receive hook has some really awesome power, but without knowing the git commands backward and forward, it can be very frustrating to get working.

### The value of the pre-receive hook

Whenever a push is made to the centralized repository, you don't just want to let any willy nilly commit crawl in there.  You can't trust that the author of the commits did his part to validate the code.  So you need to at least do some basic checks.  That is what the pre-receive hook does.  In the following example, I am parsing files that end in '.pp' with puppet syntax validation as you would do from the command line.

<pre><pre>#!/bin/bash

while read old_sha1 new_sha1 refname anothervalue ; do
    list=$(git show --pretty="format:" --name-only $new_sha1 | grep -e ".pp$")
    for tmpfile in ${list}; do
        git show ${new_sha1}:${tmpfile} | puppet --color=false --confdir=/tmp --vardir=/tmp --parseonly --ignoreimport
        if [ "$?" -ne "0" ]; then exit 1; fi
    done
done

exit $?</pre>


<p>
  The above script, placed in a bare repository at hooks/pre-receive with the execute (+x) bit turned on, will get a list of files that end in '.pp' and run the puppet validator for the newest commit in the push.  Essentially, I can validate someone else's puppet code in just a few seconds and return a failure if it doesn't succeed.  With git hooks, a failure means no commit/push/etc will actually happen.
</p>


<p>
  I sure hope this helps someone else to understand pre-receive hooks as well as git hooks in general.  If you have any helpful suggestions or comments, those are most welcome as well.
</p>


<p>
  Cheers,
</p>


<p>
  Herlo
</p>

 [1]: http://Backcountry.com
 [2]: http://github.com
 [3]: http://www.kernel.org/pub/software/scm/git/docs/githooks.html