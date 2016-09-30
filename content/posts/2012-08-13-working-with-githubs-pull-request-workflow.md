---
title: Working with github's pull request workflow
author: herlo
layout: post
date: 2012-08-13T16:25:16+00:00
url: /2012/08/13/working-with-githubs-pull-request-workflow/
categories:
  - Fedora
  - git
  - GoOSe
  - Tech
tags:
  - 2012
  - august
  - fork
  - git
  - github
  - pull
  - pull request
  - push
  - salt
  - saltstack
  - workflow

---
Recently, I have given a response similar to this at least a half-dozen times and thought it could be useful here.  I work with many github repositories and manage them each and every day.  Below is the workflow I use to make things simple, easy and efficient.

First off, whoever you are pulling from is the 'upstream' repo. My example uses the the [saltstack repository][1] (git://github.com/saltstack/salt.git). Make sure it's set to the **read only** git url so as to not accidentally push to upstream directly. To set this, you can do the following operation in your repository:

<pre>git remote add upstream git://github.com/saltstack/salt.git</pre>

Next, adjust the origin repository to point to your fork of the saltstack repository. In my case, my username is 'herlo' so my ssh-based read-write git url would be 'git@github.com:herlo/salt.git'. To adjust the values, do the following:

<pre>git remote set-url origin git@github.com:herlo/salt.git</pre>

It's possible that 'origin' isn't set, but if you cloned originally from the saltstack repo, it will need to be adjusted.

Finally, it's good to verify this, run 'git config –list' and look for lines similar to what I show below. If you have yours configured this way, you are ready to work with the github pull request structure simply and efficiently.

<pre>git config --list
..snip..
remote.origin.fetch=+refs/heads/*:refs/remotes/origin/*
remote.origin.url=git@github.com:herlo/salt.git
branch.master.remote=origin
branch.master.merge=refs/heads/master
remote.upstream.url=git://github.com/saltstack/salt.git
remote.upstream.fetch=+refs/heads/*:refs/remotes/upstream/*</pre>

Last step, and this is more of a workflow piece than anything. Simply perform tasks in this fashion and you'll be able to handle most anything with github's pull requests.

  1. git pull upstream master/develop –  (the develop branch is likely the one you want)
  2. do some work, make commits to your changes, etc.
  3. git push origin master
  4. submit a pull request at your fork – (for example, https://github.com/herlo/salt/pull/new/master)
  5. once your merged changes are accepted, go back to step one – rinse and repeat.

I hope this helps clarify how the workflow in github could work. It's simple, easy and effective.

Please let me know of any tweaks as you go through this process. I'd like to hear of any way to improve my process as well.

Cheers,

herlo

 [1]: https://github.com/saltstack/salt
