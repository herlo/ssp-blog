---
title: 'POW: Gobby, the little engine that could! (collaborate)'
author: herlo
layout: post
date: 2008-02-28T07:29:01+00:00
url: /2008/02/28/pow-gobby-the-little-engine-that-could-collaborate/
categories:
  - Collaboration
  - Editors
  - Fedora
  - POW
  - Tech
  - Tools
tags:
  - Collaboration
  - Fedora
  - gobby
  - Tools
  - UTOS
  - wiki

---
_Its been a very long time since I've done the Product of the Week, so I am going to change the name to Product of Whenever. This suits me better._

In July of 2001, I was introduced to a little editing tool many of us now know fondly, the wiki. I was travelling to New Zealand looking for work. During my month's stay, the fellow I traveled with showed me his wiki-wiki. He explained how collaboration could work and the simplicity of the system made it even great for a one person quick web page. Immediately, I was hooked. When I returned from New Zealand and enrolled in school, my mind quickly went back to this funky wiki-editor thing I'd seen. Being a geek even back then, I promptly installed one.

Fast-forward almost 7 years. We've seen the wiki evolve from a little app that could be used to make an entire website of information so grand that even the largest collectors of physical data can't compete. We've seen tools like DocuWiki – the documentation wiki, MediaWiki – which needs no introduction and Tomboy – the little desktop wiki. Many other wiki's emerged to help people collaborate all around the world. How great a time it was&#8230;

This article isn't about wiki's, rather it is about collaboration. This article is about a different type of collaboration, one that's more real-time than a wiki can be. In some ways its more limiting and in others, much less. The feature I'm referring to is real-time collaboration. And the tool that enables this, _**gobby**_, and its closely related cousins, _**sobby**_ and _**obby**_.

**INTRODUCING GOBBY**

[![The Gobby Editor][1]][2]

Gobby is a collaborative text editor, with a bunch of cool features. While gobby is still young and not quite feature-full, its quite amazing what it can do out of the box. The collaboration abilities of gobby come straight out of the box. One can choose to create a session on the local network, or create a server version, with **_sobby_**, where everyone can connect to a centralized server to collaborate. I'd like to also point out this application can also run in Windows according to the authors' website, though I've heard rumors that it doesn't work as I've not personally tried.

To get started with gobby, its easily installed:

`# yum install gobby<br />
.. snip ...`

Once its installed, gobby will easily load from Applications -> Internet -> Gobby Collaborative Editor. Up pops the window we showed you above, albeit a little more bare. The toolbar is the most important piece here.

[![Gobby is disconnected at initial start.  Click create or join a session][3]][4]

There are two distinct features here, plus the ability of a regular text editor. On the left, are the connection buttons, one can join or create a session. On the right hand side, are user and document lists, and a chat button. The left hand side controls how to connect, the right controls once you are connected. Of course, the middle does have tools of a normal editor.

Clicking the _Create session_ button provides this dialog, allowing for a local session to be created and maintained.

[![gobby-create.png][5]][6]

This session can be just one person, but is definitely better with at least two. Notice that you'll need to pick a colour. This feature is what makes it easy to tell who's edited what parts of every document in _**gobby**_.

The other option is to join a session. Joining a session also lists any local sessions currently available.

[![gobby-join.png][7]][8]

Once the session is created and/or joined, its just a matter of using _**gobby**_ like an editor. The fun part about _**gobby**_ though, is when the collaboration begins. When working on a document, others can work on it as well, at the same time. Which can be confusing, and troublesome the first time you play with this tool. Give it some time and you'll be hooked.

In addition to creating an _**obby**_ session with the _**gobby**_ application, its also possible to create a persistent connection with the _**sobby**_ server. Unfortunately, _**sobby**_ doesn't have features that let it run as a SYSV service, but it is possible to get a server up and running quite easily even still. The organization I run, <a href="http://utos.org" target="_blank">UTOSF</a>, has one currently up and running at gobby.utos.org. If you want to join up, please let me know and we'll get you connected.

Take the time to get to know this awesome collaboration tool, and start working with your friends who code, or document or even just for simple brainstorming sessions.  The possibilities are endless.

Cheers,

Herlo

 [1]: {{<siteurl>}}uploads/2008/02/gobby-intro.thumbnail.png
 [2]: {{<siteurl>}}uploads/2008/02/gobby-intro.png "The Gobby Editor"
 [3]: {{<siteurl>}}uploads/2008/02/gobby-disc.png
 [4]: {{<siteurl>}}uploads/2008/02/gobby-disc.png "Gobby is disconnected at initial start.  Click create or join a session"
 [5]: {{<siteurl>}}uploads/2008/02/gobby-create.thumbnail.png
 [6]: {{<siteurl>}}uploads/2008/02/gobby-create.png "gobby-create.png"
 [7]: {{<siteurl>}}uploads/2008/02/gobby-join.thumbnail.png
 [8]: {{<siteurl>}}uploads/2008/02/gobby-join.png "gobby-join.png"