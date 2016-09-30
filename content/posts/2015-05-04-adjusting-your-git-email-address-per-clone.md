---
title: Adjusting your git email address per clone
author: herlo
layout: post
date: 2015-05-04T23:40:11+00:00
url: /2015/05/04/adjusting-your-git-email-address-per-clone/
categories:
  - Bash
  - git
  - Passion
  - Tech
  - Tools

---
I've been working a lot with git over the years. To that end, I commonly use my personal email address for projects I post on [my github][1]. Additionally, I have a project or two in which I participate. The email address I use there is just an alias to my personal email, but I want to use it instead of the email above.

Today, I came [across an article][2] that makes changing this value much, much simpler.  Try this:

<pre><code class="language-text" data-lang="text">$ git config --global alias.personal 'config user.email "herlo@personal"'
$ git personal
$ git config user.email
herlo@personal
$ git config --global alias.work 'config user.email "herlo@work"'
$ git work
$ git config user.email
herlo@work</code></pre>

As you can see, it's now trivial to switch between certain email addresses. Man, git aliases are very nice!

Cheers,

herlo

 [1]: https://github.com/herlo
 [2]: http://www.codeography.com/2011/08/05/project-specific-git-author.html
