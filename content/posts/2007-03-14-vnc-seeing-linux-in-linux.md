---
title: 'VNC – Seeing Linux in Linux'
author: herlo
layout: post
date: 2007-03-14T22:48:38+00:00
url: /2007/03/14/vnc-seeing-linux-in-linux/
categories:
  - Tech
  - Tools

---
What does that mean? Seeing Linux in Linux? Huh?

Well let me tell you a little about **vnc** – Virtual Network Computing.

**vnc** has been around quite some time, and in Fedora, its easy to setup. **vnc** supports communication over **ssh** too, which will help us securely perform over the network. There are two parts to **vnc**, the client **vncviewer**; and the server; **vncserver**. The easiest way to configure **vnc** is to set up **vncserver** first.

**vncserver** runs as a system V service in Fedora 6. We need to do some configuration to allow connections from different users. Modify the _/etc/sysconfig/vncservers_ configuration file to set the connections up:

`# vi /etc/sysconfig/vncservers`

Find the lines that look like this:

`VNCSERVERS="1:root"`
  
`VNCSERVERARGS[1]="-geometry 800x600"`

And add your configurations however you'd like. Many options are detailed in this configuration file. Here's a few good ones:

`-nolisten tcp` – Prevents X connections to the VNC Server over TCP
  
`-localhost` – Prevents remote VNC clients from connecting, except when they do a **ssh** tunnel.

Here is my _/etc/sysconfig/vncservers_ file on a system I recently configured:

`# cat /etc/sysconfig/vncservers`
  
`..snip..`
  
`VNCSERVERS="1:root 2:student"`
  
`VNCSERVERARGS[1]="-geometry 800x600"`
  
`VNCSERVERARGS[2]="-geometry 640x480 -localhost"`

Of course, we should make a password for each of our users as well. This password should probably not be the same as the user's login, but nothing prevents the password from being the same. To change the users password, login as that user and run **vncpasswd**:

`# vncpasswd`
  
`Password: <em>mypassword</em>`
  
`Verify: <em>mypassword</em>`

Finally, we need to make sure **vncserver** starts correctly:

`# /etc/init.d/vncserver restart`
  
`..snip..`
  
`Starting VNC server: 1:root`
  
`New 'station5.example.com:1 (root)' desktop is station5.example.com:1`

`Starting applications specified in /root/.vnc/xstartup`
  
`Log file is /root/.vnc/station5.example.com:1.log`

`2:student`
  
`New 'station5.example.com:2 (student)' desktop is station5.example.com:2`

`Starting applications specified in /home/student/.vnc/xstartup`
  
`Log file is /home/student/.vnc/station5.example.com:2.log`

Once started, test out the connections. These two connections have been configured differently.

Connection _**1**_ will let me connect as root with a screen size of 800&#215;600 over an insecure vnc connection. Connection _**2**_ will let me connect as student but only via an **ssh** tunnel. Let's have a look at how we'd connect:

Connecting as **root** to _station5_:

`$ vncviewer station5:1`

or

`$ vncviewer via root@station5 localhost:2`

``[![VNC - Login Prompt][1]][2]

This prompt appears.   Enter the password you created earlier with **vncpasswd**.

And voila!! You should have access to that user's desktop.

Cheers,

Herlo

 [1]: {{<siteurl>}}uploads/2007/03/vnc-login.thumbnail.png
 [2]: {{<siteurl>}}uploads/2007/03/vnc-login.png "VNC - Login Prompt"