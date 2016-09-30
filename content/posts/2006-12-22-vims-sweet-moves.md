---
title: vim's sweet moves
author: herlo
layout: post
date: 2006-12-22T17:00:43+00:00
url: /2006/12/22/vims-sweet-moves/
categories:
  - Editors
  - Tech

---
Lately, I've been spending a lot of time editing books for my company, <a target="_blank" href="http://www.gurulabs.com">Guru Labs</a>. Because of this, I've come to really appreciate the power of **vim**, and some of it's very intuitive functionality. Many of you probably have much more experience with **vim** than I do, but I'd like to share some of the cool things I've recently learned while using vim.

Most of these commands involve command mode. If you are unclear what command mode is, you can find the documentation at <a target="_blank" href="http://www.vim.org/">http://www.vim.org/</a>. Anyway, here's the command I like to use:

  * **_:cd /path/to/where/my/files/reside_** – the :cd command allows you to change directory to somewhere more useful than where you currently are in the file tree. I find this useful when I am working on one project, then need to move away from that project to another one. I simply _:cd /to/the/new/project/dir_ and then open the file from there.
  * **_:e filename_** – this command will simply open the requested file (if it exists) right into **vim**. If you need to abandon unsaved changes on the previous file, use _:e!._
  * _**:pwd**_ – this one may seem obvious to some, but did you know you can print your current **vim** working directory? Pretty neat I say.

These are some simple command to help you move about in **vim**. I am sure there are plenty more that you use, why not share them?

Cheers,

Clint
