---
title: Succumbing to the pressure
author: herlo
layout: post
date: 2008-04-13T01:31:01+00:00
url: /2008/04/12/succumbing-to-the-pressure/
categories:
  - Bash
  - Community
  - Guru
  - Tech
  - Tools
tags:
  - banana
  - Bash
  - git
  - make
  - svn

---
My T60p.

[clints@herlo-lap ~]$ history|awk '{a[$2]++ } END{for(i in a){print a[i] &#8221; &#8221; i}}'|sort -rn|head
  
144 svn
  
144 cd
  
108 ls
  
104 ./manage.py
  
101 ssh
  
69 su
  
43 screen
  
26 vim
  
25 rm
  
15 ping

[clints@thor ~]$ history|awk '{a[$2]++ } END{for(i in a){print a[i] &#8221; &#8221; i}}'|sort -rn|head
  
266 git
  
260 make
  
71 cd
  
57 ls
  
55 vim
  
55 rt
  
26 rm
  
19 bin/send-patch
  
18 grep
  
16 bin/validate

I guess I love RCS'.

Cheers,

Herlo