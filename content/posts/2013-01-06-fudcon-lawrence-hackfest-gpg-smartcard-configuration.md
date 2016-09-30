---
title: 'FUDCon Lawrence Hackfest: GPG SmartCard Configuration'
author: herlo
layout: post
date: 2013-01-07T03:31:08+00:00
url: /2013/01/06/fudcon-lawrence-hackfest-gpg-smartcard-configuration/
categories:
  - Fedora
  - FUDCon
  - Tech
tags:
  - 2013
  - Fedora
  - fudcon
  - GPG
  - hackfest
  - OpenGPG
  - smartcard
  - SSH

---
As I've been working at my new job at the [Linux Foundation][1], we have been [implementing quite a bit of two-factor authentication][2]. In fact, back in November, [Fedora implemented two-factor authentication for sudo at the Security FAD][3]. I was there and helped setup the clients and did some testing.

While I was there, I had another agenda item, [creating a HOWTO for enabling a GPG SmartCard for use with SSH][4]. Of course, the SmartCard can be used for both encryption and signing as well.

After finishing that HOWTO, I was talking about it with a few people within Fedora, and there seemed to be quite a bit of interest. It turns out there was quite a bit of interest, so I've decided to do a hackfest on [Saturday at FUDCon][5] to help move people over to GPG SmartCards. This is also going to be quite nice in that there will be a [GPG key signing event][6] after this hackfest.

### Come Prepared – Equipment Required

It's important you come prepared! If you have ever had interest in this sort of thing, there's time to get equipment for the hackfest. Here's what you need:

  * SmartCard Reader, any will do. I recommend the [Gemalto USB Shell Token V2 from kernelconcepts.de][7].
  * An OpenPGP SmartCard. Several vendors have them. I recommend the [OpenPGP SmartCard V2 from kernelconcepts.de][8].

Both pieces are required. **Order ASAP,** it takes about 10 days to ship. Consider even shipping to the FUDCon hotel if you are concerned or late. I know Petra will work hard to deliver them as fast as possible.

### Doing a Little Prep Work

If you get your Token and SmartCard before FUDCon Lawrence and have a few spare minutes, feel free to read through my HOWTO. If you get through it, come to the hackfest and help others who might not have had time.

Cheers,

herlo

 [1]: http://www.linuxfoundation.org/
 [2]: https://github.com/mricon/totp-cgi
 [3]: https://fedoraproject.org/wiki/FAD_Infrastructure_Security_2012
 [4]: https://github.com/herlo/ssh-gpg-smartcard-config/blob/master/README.rst
 [5]: http://fedoraproject.org/wiki/FUDCon:Lawrence_2013#Hackfests_.28Saturday_and_Sunday.29
 [6]: http://fedoraproject.org/wiki/FUDCon:Lawrence_2013_GPG_Key_Signing_Event
 [7]: http://shop.kernelconcepts.de/product_info.php?cPath=1_26&products_id=119
 [8]: http://shop.kernelconcepts.de/product_info.php?products_id=42&osCsid=101f6f90ee89ad616d2eca1b31dff757