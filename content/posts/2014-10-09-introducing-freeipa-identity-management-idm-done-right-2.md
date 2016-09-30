---
title: Introducing FreeIPA – Identity Management (IdM) Done Right!
author: herlo
layout: post
date: 2014-10-10T06:41:31+00:00
url: /2014/10/09/introducing-freeipa-identity-management-idm-done-right-2/
categories:
  - DNS
  - FreeIPA
  - Tech
  - Tools
tags:
  - 389DS
  - apache
  - bind
  - certificate
  - DNS
  - dogtag
  - freeipa
  - identity
  - IdM
  - kerberos
  - ldap
  - management
  - ntp
  - pam
  - ssl
  - sssd

---
It has been a while since I&#8217've posted anything on this blog. It is high time I get something useful up here. Lucky for you, dear reader, I have a series of posts to share. Each of them about a new technical passion of mine, Identity Management.

Many of you probably know of Active Directory. The all encompassing Identity Management solution from Microsoft. It's is the most popular solution out there, and its got a good hold on the market, for sure. But with almost all things Microsoft comes closed source, GUI only management, and resentment among many.

I'm not saying that Active Directory does not do its job as an IdM solution. In fact, I think it's a fine solution, if you want to have a proprietary solution, pay a ton of money yearly and not follow standards. In terms of Identity Management, however, it is a pretty good system overall.

The thing is, closed source systems historically have more issues and delays for fixes long term. Until recently, however, there hasn&#8217't been a reasonable open source solution for IdM. Enter FreeIPA, Identity Management done right.

## What is FreeIPA?

FreeIPA is a solution for managing users, groups, hosts, services, and much, much more. It uses open source solutions with some Python glue to make things work. Identity Management made easy for the Linux administrator.

[<img class="alignleft  wp-image-1218" src="{{<siteurl>}}uploads/2014/10/ipa-components-590x444.png" alt="ipa-components" width="383" height="333" />][1]Inside FreeIPA are some common pieces; The Apache Web Server, BIND, 389DS, and MIT Kerberos. Additionally, Dogtag is used for certificate management, and sssd for client side configurations. Put that all together with some python glue, and you have FreeIPA.

As you can see from the diagram, there is also an API which provides programmatic management via Web and Command Line interfaces. Additionally, many plugins exist. For example, one exists to set up trust agreements for replication to Active Directory. Additional functionality exists for managing Samba shares via users and groups in FreeIPA.

It's probably a good time to setup a FreeIPA server and show its power.

## Installation

Installing FreeIPA is simple on a Linux system. However, there are a few things needed. This installation is being performed on a fully updated CentOS 7.0 system. An entry in the /etc/hosts matching the server ip and hostname is useful. Additionally, make sure to set the hostname properly.

<pre># <strong>echo 192.168.122.200 ipa7.example.com ipa7 &gt;&gt; /etc/hosts</strong>
# <strong>echo ipa7.example.com &gt; /etc/hostname</strong></pre>

We'll be installing the server at this time, but there is a client install, which we'll show in later posts. It's recommended to use RHEL/CentOS >= 6.x or Fedora >= 14. Simply perform a yum install.

<pre>(rhel/centos) # <strong>yum install ipa-server</strong>
(fedora) # <strong>yum install freeipa-server</strong>
..snip..</pre>

Once the {free,}ipa-server package is installed. Run the install itself. Since FreeIPA can manage a dns server, a decision must be made. Here, we are going to choose to manage our internal dns with FreeIPA, which uses ldap via 389DS to store the records.

<pre># <strong>yum install bind-dyndb-ldap</strong>
..snip..
# <strong>ipa-server-install --setup-dns</strong>
The log file for this installation can be found in /var/log/ipaserver-install.log
==============================================================================
This program will set up the IPA Server.

This includes:
 * Configure a stand-alone CA (dogtag) for certificate management
 * Configure the Network Time Daemon (ntpd)
 * Create and configure an instance of Directory Server
 * Create and configure a Kerberos Key Distribution Center (KDC)
 * Configure Apache (httpd)
 * Configure DNS (bind)

To accept the default shown in brackets, press the Enter key.

WARNING: conflicting time&date synchronization service 'chronyd' will be disabled
in favor of ntpd

Existing BIND configuration detected, overwrite? [no]: <strong>yes</strong></pre>

The installation explains the process and services which will be installed. Because we're installing using DNS, some skeleton files exist. It's safe to overwrite them and move forward.

Next, define the server hostname, and the domain name (for DNS).

<pre>Enter the fully qualified domain name of the computer
on which you're setting up server software. Using the form
&lt;hostname&gt;.&lt;domainname&gt;
Example: master.example.com.


Server host name [ipa7.example.com]: <strong>ipa7.example.com</strong>

Warning: skipping DNS resolution of host ipa7.example.com
The domain name has been determined based on the host name.

Please confirm the domain name [example.com]: <strong>example.com</strong></pre>

The next section covers the kerberos realm. This may seem confusing, but kerberos is one of the big powerhouses behind FreeIPA. It makes registering client systems very simple. Kerberos realm names are always in upper case. Usually, they emulate the domain name.

<pre>The kerberos protocol requires a Realm name to be defined.
This is typically the domain name converted to uppercase.

Please provide a realm name [EXAMPLE.COM]: <strong>EXAMPLE.COM</strong></pre>

Next, configure the passwords for the Directory Manager (for ldap administration) and the IPA admin user.

<pre>Certain directory server operations require an administrative user.
This user is referred to as the Directory Manager and has full access
to the Directory for system management tasks and will be added to the
instance of directory server created for IPA.
The password must be at least 8 characters long.

Directory Manager password: <strong>manager72</strong>
Password (confirm): <strong>manager72</strong>

The IPA server requires an administrative user, named 'admin'.
This user is a regular system account used for IPA server administration.

IPA admin password: <strong>ipaadmin72</strong>
Password (confirm): <strong>ipaadmin72</strong></pre>

Finally, the installer follows up with a request for more DNS info.

<pre>Do you want to configure DNS forwarders? [yes]: <strong>yes</strong>
Enter the IP address of DNS forwarder to use, or press Enter to finish.
Enter IP address for a DNS forwarder: <strong>8.8.8.8</strong>
DNS forwarder 8.8.8.8 added
Enter IP address for a DNS forwarder: <strong>8.8.4.4</strong>
DNS forwarder 8.8.4.4 added
Enter IP address for a DNS forwarder: <strong>&lt;enter&gt;</strong>
Do you want to configure the reverse zone? [yes]: <strong>yes</strong>
Please specify the reverse zone name [122.168.192.in-addr.arpa.]: <strong>122.168.192.in-addr.arpa</strong>
Using reverse zone 122.168.192.in-addr.arpa.</pre>

Now that all of the questions have been asked and answered. It's time to let the installer do its thing. A verification step prints out all of the values entered. Make sure to review them carefully.

<pre>The IPA Master Server will be configured with:
Hostname: ipa7.example.com
IP address: 192.168.122.200
Domain name: example.com
Realm name: EXAMPLE.COM

BIND DNS server will be configured to serve IPA domain with:
Forwarders: 8.8.8.8, 8.8.4.4
Reverse zone: 122.168.192.in-addr.arpa.</pre>

Then, when ready, confirm the install and go grab a cup of joe. Installation takes anywhere from 10-30 minutes.

<pre>Continue to configure the system with these values? [no]: <strong>yes</strong>

The following operations may take some minutes to complete.
Please wait until the prompt is returned.

Configuring NTP daemon (ntpd)
 [1/4]: stopping ntpd
 [2/4]: writing configuration
 [3/4]: configuring ntpd to start on boot
 [4/4]: starting ntpd
..snip..</pre>

When complete, the installation gives a bit of useful information. Make sure to open the ports within the firewall. This is beyond the scope here, and is left as an exercise for the reader.

<pre>Setup complete

Next steps:
    1. You must make sure these network ports are open:
        TCP Ports:
          * 80, 443: HTTP/HTTPS
          * 389, 636: LDAP/LDAPS
          * 88, 464: kerberos
          * 53: bind
        UDP Ports:
          * 88, 464: kerberos
          * 53: bind
          * 123: ntp

    2. You can now obtain a kerberos ticket using the command: 'kinit admin'
       This ticket will allow you to use the IPA tools (e.g., ipa user-add)
       and the web user interface.

Be sure to back up the CA certificate stored in /root/cacert.p12
This file is required to create replicas. The password for this
file is the Directory Manager password</pre>

Now that everything is installed. One last simple configuration will help. To ensure users can login correctly, use _authconfig_ to ensure home directories are created. Followed by a quick reboot.

<pre># <strong>authconfig --enablemkhomedir --update</strong>
# <strong>chkconfig sssd on</strong>
Note: Forwarding request to 'systemctl enable sssd.service'.
# <strong>init 6</strong></pre>

Once the system has rebooted, point the browser to the newly installed FreeIPA service. Logging into FreeIPA can be done in two different ways; from the browser, or via kerberos. For now, login via the web browser as the admin user.

[<img class="alignleft wp-image-1220 size-medium" src="{{<siteurl>}}uploads/2014/10/ipa-login1-590x320.png" alt="" width="590" height="320" srcset="{{<siteurl>}}uploads/2014/10/ipa-login1-590x320.png 590w, {{<siteurl>}}uploads/2014/10/ipa-login1.png 800w" sizes="(max-width: 590px) 100vw, 590px" />][2]

&nbsp;

Once logged in, a useful configurations is necessary before adding users. Change the default shell for all users to **/bin/bash**. This is done by choosing _IPA Server_ -> _Configuration_. Once modified, click _Update_.

[<img class="alignnone wp-image-1221" src="{{<siteurl>}}uploads/2014/10/ipa-config-shell.png" alt="ipa-config-shell" width="401" height="309" />][3]

Now it's time to add a user. Choose the _Identity_ tab. Then click _Add_.

[<img class="alignnone wp-image-1222" src="{{<siteurl>}}content/uploads/2014/10/ipa-user-add.png" alt="ipa-user-add" width="400" height="188" />][4]

Clicking _Add and Edit_ presents the user's data. This is useful for adding an ssh key.

[<img class="alignnone wp-image-1223" src="{{<siteurl>}}uploads/2014/10/ipa-user-sshkey-590x256.png" alt="ipa-user-sshkey" width="401" height="174" srcset="{{<siteurl>}}uploads/2014/10/ipa-user-sshkey-590x256.png 590w, {{<siteurl>}}uploads/2014/10/ipa-user-sshkey.png 910w" sizes="(max-width: 401px) 100vw, 401px" />][5]

**NOTE**: Don't forget to click _Update_ after setting the key.

This should now allow ssh into the FreeIPA server as the new user. To make this possible, make sure the new FreeIPA server is configured as a resolver. The simplest way is to update the _/etc/resolv.conf_ file.

<pre># <strong>cat /etc/resolv.conf</strong>
search egavas.org
nameserver 192.168.122.200
..snip..

# <strong>host ipa7.example.com</strong>
ipa7.example.com has address 192.168.122.200</pre>

Once the FreeIPA server is resolvable, ssh should now work.

<pre>[herlo@x220 ~]$ <strong>ssh ipa7.example.com</strong>
The authenticity of host 'ipa7.example.com (192.168.122.200)' can't be established.
ECDSA key fingerprint is 42:96:09:a7:1b:ac:df:dd:1c:de:73:2b:86:51:19:b1.
Are you sure you want to continue connecting (yes/no)? <strong>yes</strong>
Warning: Permanently added 'ipa7.example.com' (ECDSA) to the list of known hosts.
Creating home directory for herlo.
Last login: Fri Oct 10 02:27:44 2014 from 192.168.122.1
[herlo@ipa7 ~]$ <strong>id</strong>
uid=151600001(herlo) gid=151600001(herlo) groups=151600001(herlo) context=unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c102</pre>

Congratulations! The FreeIPA server is now configured. In the next post, I will cover how to configure a client system and setup centralized sudo.

Cheers,

herlo

 [1]: {{<siteurl>}}uploads/2014/10/ipa-components.png
 [2]: {{<siteurl>}}uploads/2014/10/ipa-login1.png
 [3]: {{<siteurl>}}uploads/2014/10/ipa-config-shell.png
 [4]: {{<siteurl>}}uploads/2014/10/ipa-user-add.png
 [5]: {{<siteurl>}}uploads/2014/10/ipa-user-sshkey.png
