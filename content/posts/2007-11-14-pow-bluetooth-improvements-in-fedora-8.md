---
title: 'POW: Bluetooth Improvements in Fedora 8'
author: herlo
layout: post
date: 2007-11-14T16:16:55+00:00
url: /2007/11/14/pow-bluetooth-improvements-in-fedora-8/
categories:
  - Bluetooth
  - Fedora
  - GNOME
  - Guru
  - Install
  - POW
  - Releases
  - Tech
  - Tools
tags:
  - Bluetooth
  - f8
  - Fedora
  - gnome-bluetooth
  - hidd
  - mouse
  - POW

---
The POW is going to be the improvements made in the Bluetooth functionality in Fedora 8. I'm actually quite impressed with it as its been a bit of a challenge to keep my little mouse connected in the past.

Fedora 8 provides a new extended technology with its bluez-gnome package. In fact, the simplicity of it is that I only have to be able to click and approve a new device.

When I first turn on my bluetooth mouse and start to move it around, it doesn't work, but up in the top right hand corner of my GNOME desktop is the bluetooth manager. It has a message for me:

[![bluetooth-authorize.png][1]][2]

The message indicates a click to authorize the device, namely the bluetooth mouse. (One note here, I was originally unable to use my touchpad, so I had to resort to other tactics [not pretty] to enable my mouse. Probably ought to have some other options available instead of clicking.)

Clicking on the notification window above brings me to an authorization window.

[![bluetooth3.png][3]][4]

At this point, authorization is quite simple. Click yes for a one time authorization of the mouse (Note the Bluetooth Travel Mouse indicated in the description), and to authorize it more permanently, choose _Always Grant Access_.

That's it. My Bluetooth mouse is now enabled and working. I'd say this is much friendlier than what I used to have to do, including running hidd –connect <bluetooth id> after pressing the little connect button on the bottom of the mouse. This is sure nice now!

Its possible, that at some point, disconnecting the device might be necessary. To do this, right-click on the nice little Bluetooth logo at the top right of your screen.

[![bluetooth5.png][5]][6]

Choose _Preferences_. Up pops the Bluetooth Preferences window. From this window, three tabs are available. In the first (and also selected) tab, there is a section at the bottom of the window which lists the devices that are currently bonded and/or trusted. Choose the device from the list and then the appropriate action. The choices are Disconnect, Trust or Delete.

[![bluetooth4.png][7]][8]

In addition to just configuring your devices, it appears it might be possible to do things like Bluetooth DUN with a Treo, or enable data synchronization between laptops. One thing I've always wanted to try is to get my bluetooth headset working so I could do Skype or Asterisk phone calls through my headset, to my computer and out through the service.

Cheers,

Herlo

 [1]: {{<siteurl>}}uploads/2007/11/bluetooth-authorize.thumbnail.png
 [2]: {{<siteurl>}}uploads/2007/11/bluetooth-authorize.png "bluetooth-authorize.png"
 [3]: {{<siteurl>}}uploads/2007/11/bluetooth3.thumbnail.png
 [4]: {{<siteurl>}}uploads/2007/11/bluetooth3.png "bluetooth3.png"
 [5]: {{<siteurl>}}uploads/2007/11/bluetooth5.thumbnail.png
 [6]: {{<siteurl>}}uploads/2007/11/bluetooth5.png "bluetooth5.png"
 [7]: {{<siteurl>}}uploads/2007/11/bluetooth4.thumbnail.png
 [8]: {{<siteurl>}}uploads/2007/11/bluetooth4.png "bluetooth4.png"