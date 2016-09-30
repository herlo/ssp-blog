---
title: 'Fedora Security FAD: The Results'
author: herlo
layout: post
date: 2012-12-01T17:20:03+00:00
url: /2012/12/01/fedora-security-fad-the-results/
categories:
  - FAD
  - Fedora
  - Tech
tags:
  - 2012
  - authentication
  - fad
  - Fedora
  - GPG
  - November
  - pam_url
  - pgp
  - security
  - smartcard
  - totpcgi
  - Two-Factor

---
Well, I think it was quite successful. Probably the most successful Fedora Activity Day I've attended. Many things were accomplished toward the goal of two-factor authentication within Fedora Infrastructure:

  * Installed and configured [totpcgi][1] authentication on the staging environment. This performs the verification from the clients. There will be several servers doing authentication to prevent a single point of failure.
  * Installed and configured [pam_url][2] on each staging client with the intent of connecting to the authentication servers.
  * Enabled [yubikey][3] as an alternate second factor.
  * Reviewed RPMs for [pam_url][4] and [totpcgi][5] (and a few others to help along the way)
  * Setup the totpcgi provisioning web page for google authenticator
  * Fixed fun bugs in pam_url
  * Wrote [documentation on how to setup authentication][6].

A few things were accomplished that were not part of the goals, but good stuff nonetheless:

  * Enjoyed some awesome [tapas at Buku][7] (a restaurant is at the base of the Red Hat Tower)
  * Found the [open source cow][8]
  * Documented the setup of the [OpenPGP SmartCard with gpg-agent and GNOME 3][9]
  * Watched [Seth Vidal do some Beastie Boys][10]!
  * Enjoyed some [yummy dinner at Gravy][11] (thanks to Ruth Suehle and Red Hat)
  * Discussed some ideas for FUDCon Lawrence and the future of FUDCons

While I didn't participate in all of the above activities, I was definitely involved in many of them. It turns out, everyone there was fairly involved at the FAD. It was fun to watch everyone come together to solve this issue. Everyone seemed to have a good sense of satisfaction accomplishing the goals.

Cheers,

herlo

 [1]: https://github.com/mricon/totp-cgi/
 [2]: https://fedorahosted.org/pam_url/
 [3]: http://www.yubico.com/products/yubikey-hardware/yubikey/
 [4]: https://bugzilla.redhat.com/show_bug.cgi?id=880842
 [5]: https://bugzilla.redhat.com/show_bug.cgi?id=880863
 [6]: http://infrastructure.fedoraproject.org/infra/docs/2-factor.txt
 [7]: http://bukuraleigh.com/buku/
 [8]: http://smoogespace.blogspot.com/2012/11/fedora-activity-day-0.html
 [9]: https://github.com/herlo/ssh-gpg-smartcard-config
 [10]: https://plus.google.com/100952077644304838223/posts/bEWVstsVLtm
 [11]: http://www.gravyraleigh.com/