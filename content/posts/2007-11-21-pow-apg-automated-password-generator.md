---
title: 'POW: apg, Automated Password Generator'
author: herlo
layout: post
date: 2007-11-21T17:04:51+00:00
url: /2007/11/21/pow-apg-automated-password-generator/
categories:
  - Fedora
  - Guru
  - POW
  - Tech
  - Tools
tags:
  - apg
  - Fedora
  - POW
  - Tools

---
This week's program may seem like a bit of a cop out, but it really isn't. I've regularly found myself in need of some quick passwords to hand out to users that are both semi-secure and easy to remember. With **apg**, this can become a reality.

First, install **apg**:

<pre># yum install apg
.. snip ..
Install      1 Package(s)
.. snip ..
Total download size: 101 k
Is this ok [y/N]: <strong>y</strong>
.. snip ..
Installed: apg.i386 0:2.3.0b-5.fc8
Complete!</pre>

**apg** does provide several switches which help to provide an easy way to distribute passwords. Recently, I generated random, yet pronounceable passwords for about 30 users of an application I was using. it was quite nice to let the users login and feel safe with my choices of passwords.

To start with **apg** is quite easy to generate a set of passwords:

<pre>$ apg
NatnawmIx
GhisImAv*
Bahiwaihet
adMuhevep
Ombachat
cier]bipt</pre>

These passwords are the default set from apg, providing six pronounceable, 8-10 digit, In my opinion, its better to lose a bit of security to make a password easy to remember, than to have a user have to write the password down, more or less defeating the purpose of the password in the first place.

Because of my opinion, (and no, I'm not a security expert by any means, just using common sense), its probably a good idea to have a look at some of the switches provided by **apg**:

<pre>-a : <em></em> (default) will make the passwords semi-pronounceable, <em>1</em> on the other hand, will be pseudo-random

-n : tell <strong>apg</strong> how many passwords to display

-m/-x : the minimum/maximum length of the generated passwords</pre>

Here's an example of these options in use:

<pre>$ apg -a 1 -n 2 -m 7 -x 10</pre>

**apg** has more to give us though. We can use some standard Linux password checking utilities to help us:

<pre>-r : checks the generated passwords against a particular dictionary file.  /usr/share/dict/words, for example.</pre>

Adding this to our previous example (and removing the -a option) will verify the password doesn't have any dictionary words:

<pre>$ apg -r /usr/share/dict/words -n 2 -m 7 -x 10</pre>

The last component is _-M mode_, which can request/require that a password has a particular set of attributes. Its a bit more complex than the others above. The _mode_ consists of eight letters, _S_, _N_, _C_ and _L_, in both upper and lower case.

<pre>S :  must use special symbol set for every generated password.
s :  should use special symbol set for password generation.

N : must use numeral symbol set for every generated password.
n : should use numeral symbol set for password generation.

C : must use capital symbol set for every generated password.
c : should use capital symbol set for password generation.

L : must use small letters symbol set for every generated password (always present if pronounceable  password generation algorithm is used).
l  : should use small letters symbol set for password generation.</pre>

As you might be able to tell, the list above is almost directly from the _man_ page for **apg**. This is on purpose as it is very well explained (and recommended to read each and every _man_ page for any tool used). Many a good trick has come directly from the _man_ pages.

Let's see these options in use:

<pre>$ apg -n 2 -m 7 -x 10 -M SCnL
Hej=Nio
nefMit/</pre>

What is noted right away during several iterations of these _modes_ is the fact that rarely, if ever, is a number included. It seems the lowercase modes are not strong suggestions except in the case of &#8220;lower case letters&#8221;. However, using the uppercase mode values works every time as expected.

**apg** is a simple, yet effective tool for generating passwords. My hope is that you decide to use more secure passwords in the future with tools like **apg**.

Cheers,

Herlo