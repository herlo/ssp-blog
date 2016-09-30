---
title: 'The Mighty Bitlbee – Providing Instant Messaging to the IRC Crowd'
author: herlo
layout: post
date: 2007-01-14T23:14:33+00:00
url: /2007/01/14/the-mighty-bitlbee-providing-instant-messaging-to-the-irc-crowd/
categories:
  - Tech
  - Tools

---
I was recently introduced to <a href="http://www.bitlbee.org/main.php/news.html" target="_blank">Bitlbee</a>. Weird name I know, but I think I hear you asking &#8220;what is bitlbee?&#8221;. Well, I'd say it's a gateway for Instant Messenger (IM) using Internet Relay Chat (IRC).

Bitlbee's job is essentially to allow any individual to provide a simple access to the IM networks using your irc client. I've been up until now using <a href="http://gaim.sourceforge.net/" target="_blank">Gaim</a>. GAIM is a fine tool, but because I travel everyday, I use my laptop for my main computer. Doing so presents me with a unique problem, one which I thing Bitlbee with <a href="http://www.irssi.org/" target="_blank">irssi</a> can resolve for me, I am unable to maintain a constant connection with my IM and IRC clients using Gaim.

A couple reasons why I want this are because I want to be able to be able to keep local logs of my messages. I also want to stay online (although away) even when I am unable to be physically connected. It's something I've seen others do, but couldn't resolve to doing myself because there was only a irc client or only a IM client, but not both. Bitlbee and irssi help me solve that problem.

I'd like to share with my readers how to set up and configure Bitlbee to work with your irc client. It's easy and takes about 3-5 minutes of your time and you'll be managing your own Bitlbee server as well.

First you need to install irssi and Bitlbee:

`# yum install -y irssi bitlbee`

You might notice that <a href="http://www.xinetd.org/" target="_blank">xinetd</a> is required. You need it to run a Bitlbee server.

Once Bitlbee and irssi are installed, you're going to need to setup xinetd to allow connections to the server.

`# chkconfig xinetd on`
  
`# chkconfig bitlbee on`

[Re]start xinetd as well.

`# /etc/init.d/xinetd start`
  
 `Stopping xinetd:         [  OK  ]`
  
 `Starting xinetd:          [  OK  ]`

Once you've got things running similar to what you see above, become a limited user on the system and type:

`$ irssi`

The irssi application will start, hopefully you know enough about irssi or your irc client to get moving, but if you don't, read <a href="http://linuxreviews.org/software/irc/irssi/" target="_blank">this tutorial</a>.
  
Next thing you need to do is connect to the bitlbee server. Because bitlbee should be running on your server, just connect to localhost.

`/connect localhost`

A response similar to this should appear in the top part of the window.

`15:59 -!- Welcome to the BitlBee gateway, herlo<code><br />
<code>15:59 -!- Host herlo-lap.catan is running BitlBee 1.0.3 Linux/i686.`</code></code>

Congratulations, you've successfully set up the Bitlbee server and connected to it. Now we need to connect to our IM servers. To do this next part you should have two irssi windows. The one you are interested in is labeled &bitlbee. In the appropriate irssi window lets add an Aol Instant Messenger account.

`account add oscar herlo-aim mypassword login.oscar.aol.com` – **Note**: use `help account` for details about accounts.

The &bitlbee root user replies

`16:04 <@root> Account successfully added`

Next, save and connect to your account.

`save`
  
`account list`
  
`16:06 <@root>  0. OSCAR, herlo-aim on login.oscar.aol.com`
  
`account on` – to turn on all IM accounts
  
or
  
`account on 0` – to just turn on the AIM account

Does it work? I sure hope so. If it works, as it did for me, you should see a list of all your buddies. There are many other things you can now do. How about chatting with a friend? There's two ways to do that.

`Friend: Hey friend` – Messages Friend in the current window, you must type your Friends name each time.
  
or
  
`/msg Friend Hey friend` – Message Friend in a new window, afterwhich you must switch to the new window to continue the conversation.

For now, that's it. There are many, many good guides on all the switches within Bitlbee and irssi. I'd like to list a few I found while I was on the hunt.

  * <a href="http://www.bitlbee.org/main.php/extdoc.html" target="_blank">Bitlbee External Document Reference</a>
  * <a href="http://f0rked.com/public/bitlbee-user-guide.html" target="_blank">Bitlbee Commands</a>

I want to also mention that if you do not use Fedora or a Red Hat based system, there is another tutorial for Ubuntu <a href="http://ubuntu-tutorials.com/2007/01/14/installing-and-using-bitlbee-irc-gateway-ubuntu-610/" target="_blank">here</a>.

Cheers,

Herlo