---
title: 'Vim (encryption) Saves the Day – Again'
author: herlo
layout: post
date: 2007-03-02T21:18:34+00:00
url: /2007/03/02/vim-encryption-saves-the-day-again/
categories:
  - Editors
  - Tech
  - Tools

---
Today, while trying to find a solution which still eludes me for storing passwords in a local file. I was informed about a cool feature of **vim**, which has been in there since version 5.7, encryption. 

My main problem was that I wanted to save all of the non-browser passwords and accounts that I've been collecting over the past year or so, having them in one central location. This would make it easy to quickly obtain my usernames and passwords to my accounts on several boxen I maintain. Many of which have several passwords for my login, mysql and other services I regularly use.

**vim** provides this encryption feature in two ways. One is with the `-x` option, the other is within **vim** command mode using ':X'. **vim** does not go out of it's way to make sure protect _.swp_ temporary backup files or text in memory, so this isn't perfect. 

I am still looking for a packaged solution where I can have my passwords stored in an application where I can quickly obtain them by providing a simple pass phrase, either on a usb key, or the physical hard drive in one of my machines. I'd also like to be able to use my gpg and ssh keys as well with this method. A couple of tools that provide similar functionality would be KeePass (for Windows) and Password Safe (for Windows and Linux Source Only). 

Comments are welcome, please tell me about all the cool tools I could use. Tell me how to use gnome-keyring too, and make suggestions with usage if you can.

Cheers,

Herlo