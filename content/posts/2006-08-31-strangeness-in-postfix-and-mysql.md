---
title: Strangeness in Postfix and MySQL
author: herlo
layout: post
date: 2006-08-31T22:34:46+00:00
url: /2006/08/31/strangeness-in-postfix-and-mysql/
categories:
  - Tech

---
Okay, so I really don't have any servers that are utterly dependent on having Postfix/MySQL working, but since I moved over to this new server a couple weeks ago, I've had some interesting issues I needed to address.

Postfix:

Not sure how this happens, but every so often, when I restart Postfix, I get a very strange error. Yes, very strange indeed:

\# /etc/init.d/postfix restart

Shutting down postfix: [FAILED]
  
Starting postfix: [FAILED]
  
\# tail /var/log/maillog

..snip..

Aug 31 17:20:19 herlo postfix/postalias[14682]: fatal: open database /etc/aliases.db: Unknown error 4294936318

..snip..

This is the error I get. Strange thing is, no matter what I try, I can't get it to restart. This has happened more than one time too. Each time, I spend several hours trying to get Postfix back up and running, and eventually, after trying a million and one things, it is running again. Though I have no idea why.

This last time was no different. I invoked the 'help' button on #utah and a few other useful resources I had, nobody seemed to be able to identify what the exact problem was. After a while, I put together in my head that it might be related to my failed attempt (so far) to install <a title="Sympa" target="_blank" href="http://www.sympa.org/">Sympa</a>, which requires MySQL to run. However, I've since removed any/all mention of Sympa from my configs, so I am not sure where that is coming from yet.

At this point, at least I have a viable bandaid to my problem, but its not a fix. If anyone out there can point me in the direction of other resources that might help, I'd be greatly appreciative, possibly even convince <a title="Joseph Hall" target="_blank" href="http://blog.josephhall.com">Joseph Hall</a> to bake you a cake or something.

Cheers,

Herlo