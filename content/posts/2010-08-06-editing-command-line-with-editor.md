---
title: Editing command line with $EDITOR
author: herlo
layout: post
date: 2010-08-06T20:17:02+00:00
url: /2010/08/06/editing-command-line-with-editor/
categories:
  - Bash
  - Fedora
  - Tech
tags:
  - Bash
  - edit
  - emacs
  - vim

---
Recently, I've been working on a huge command line that I wanted to edit over and over.  However, the problem was that I didn't want to use the prompt to edit the command.  It took me a while to realize what I wanted, but finally, I realized that **most**ï»¿ of the Emacs bindings are very useful in bash, so I went to work.

I use VIM for all of my editing when I can.  I don't much care for Emacs, but since bash uses the bindings, it's good to know a few of the commands.  Like Ctrl+k, Ctrl+u, Ctrl+e, Ctrl+a (try them out with text on the bash command if you don't know what they do&#8230;).  The thing is, the default editor in many of my CentOS systems at work is Emacs.  I clearly didn't want that, so I had to change two variables in my ~/.bashrc file.  It now looks better:

`$ cat ~/.bashrc<br />
.. snip ..<br />
EDITOR=/usr/bin/vim<br />
VISUAL=/usr/bin/vim<br />
export EDITOR VISUAL<br />
.. snip ..`

After setting these variables up, it's very easy to edit the command line with vim.  First, source the ~/.bashrc file.

`$ source ~/.bashrc`

Then bring up the command to edit:

`$ yum remove -y NetworkManager.i?86 NetworkManager-glib.i?86 alsa-lib.i?86 apr.i?86 aspell.i?86 audit-libs.i?86 coolkey.i?86 cracklib.i?86 cryptsetup-luks.i?86 cyrus-sasl-lib.i?86 cyrus-sasl-plain.i?86 db4.i?86 dbus-glib.i?86 dbus-libs.i?86 device-mapper.i?86 e2fsprogs-libs.i?86 ecryptfs-utils.i?86 expat.i?86 fipscheck.i?86 freetype.i?86 giflib.i?86 glib2.i?86 gpm.i?86 hal.i?86 java-1.6.0-openjdk.i?86 keyutils-libs.i?86 krb5-libs.i?86 libICE.i?86 libSM.i?86 libX11.i?86 libXau.i?86 libXdmcp.i?86 libXext.i?86 libXi.i?86 libXt.i?86 libXtst.i?86 libXxf86vm.i?86 libaio.i?86 libcap.i?86 libdaemon.i?86 libdrm.i?86 libgcc.i?86 libgcrypt.i?86 libgpg-error.i?86 libhugetlbfs.i?86 libjpeg.i?86 libpng.i?86 libselinux.i?86 libsepol.i?86 libstdc++.i?86 libtermcap.i?86 libusb.i?86 libutempter.i?86 libvolume_id.i?86 mesa-libGL.i?86 mkinitrd.i?86 ncurses.i?86 neon.i?86 nspr.i?86 nss.i?86 nss_db.i?86 nss_ldap.i?86 numactl.i?86 openldap.i?86 openssl.i?86 openssl-devel.i?86 pam.i?86 pam_ccreds.i?86 pam_krb5.i?86 pam_passwdqc.i?86 pam_pkcs11.i?86 pam_smb.i?86 parted.i?86 readline.i?86 redhat-lsb.i?86 sqlite.i?86 tcp_wrappers.i?86 wireless-tools.i?86 zlib.i?86`

As can be seen, this is pretty long and cumbersome.  It'd be nice to be able to edit the line without having to use bash, plus, if I accidentally mistype and hit 'Enter', it could be executed before the command is ready.  To edit the command, hit the following:

`Ctrl+x, Ctrl+e`

The command will then be opened in your $EDITOR (probably /usr/bin/vim if you followed the instructions above).  Edit away, when you save and quit (:wq in VIM), the command will be executed.  If you don't want to execute the command after all, just quit without saving (:q in VIM).

Enjoy,

Herlo