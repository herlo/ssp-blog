---
title: Setting up a FreeIPA Replica
author: herlo
layout: post
date: 2014-10-28T16:58:15+00:00
url: /2014/10/28/setting-up-a-freeipa-replica/
categories:
  - FreeIPA
  - Tech
tags:
  - 389DS
  - bind
  - DNS
  - freeipa
  - ipa
  - replica
  - replication

---
In my last <a title="post" href="{{<siteurl>}}2014/10/09/introducing-freeipa-identity-management-idm-done-right-2/" target="_blank">post</a>, I mentioned that I would show how to configure a client with sudo access. Well, I lied! Hopefully that will be the next post. Instead, I&#8217'm going to cover how to set up FreeIPA replica.

Replicating FreeIPA services is useful in many ways. Managing DNS, LDAP and Kerberos services, for one. Additionally, it makes sense to have replicas in different VLANs or network zones. Opening up only the ports needed for replication between the FreeIPA servers instead of for all hosts makes things more secure.

## All Replicas are Masters

Save for things like running a Certificate Authority or DNS, all of the hosts which run FreeIPA are masters. They replicate using agreements. This means that when a new replica is setup, it will communicate with other FreeIPA servers and replicate to/from only the ones it is allowed to communicate. Further reading is <a href="https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Identity_Management_Guide/Setting_up_IPA_Replicas.html" target="_blank">available here</a>.

## Preparing for the FreeIPA Replica

Preparing the replica requires setting up the agreement documents on one of the IPA master servers.

<pre>$ ssh ipa7.example.com
..snip..

$ su -
Password: <strong>centos
</strong>
# ipa-replica-prepare replica.example.com --ip-address 192.168.122.210
Directory Manager (existing master) password: <strong>manager72

</strong>Preparing replica for replica.example.com from ipa.example.com
Creating SSL certificate for the Directory Server
Creating SSL certificate for the dogtag Directory Server
Creating SSL certificate for the Web Server
Exporting RA certificate
Copying additional files
Finalizing configuration
Packaging replica information into /var/lib/ipa/replica-info-replica.example.com.gpg
Adding DNS records for replica.example.com
Using reverse zone 122.168.192.in-addr.arpa.</pre>

## Copy the Replica gpg Data to the New Replica

The data is now packaged and needs to be put on the replica. The simplest and most secure process is to scp the file directly to the replica. In some cases, this is not possible, and other methods may need to be employed.

<pre># scp /var/lib/ipa/replica-info-replica.example.com.gpg root@192.168.122.210:
..snip..</pre>

## Install the Replica

Once the agreements are created and moved to the new replica, it&#8217's time to perform the install.

<pre>$ ssh root@192.168.122.210
root@192.168.122.210's password:</pre>

Ensure the replica can contact the master server. Additionally, make sure the replica&#8217's ip address resolves locally. Modifying _/etc/hosts_ is the simplest solution.

<pre># cat /etc/hosts
..snip..
192.168.122.210 replica.example.com
192.168.122.200 ipa7.example.com
..snip..</pre>

Set the hostname properly. If it isn&#8217't, correct it by modifying _/etc/sysconfig/network_.

<pre># hostname
replica.example.com</pre>

Once all of the above is correct, it&#8217's time to perform the installation itself. Since a replica is just a clone of another master, installing the same packages makes sense.

<pre># yum install ipa-server bind-dyndb-ldap -y
..snip..</pre>

Next, perform the install. Consider options like --setup-ca_ and --setup-dns_ as optional, though very useful if those processes are going to be needed on the new replica.

<pre># ipa-replica-install --setup-dns /root/replica-info-replica.example.com.gpg \
--no-forwarders --ip-address=192.168.122.210
Directory Manager (existing master) password: <strong>manager72</strong>

Run connection check to master
Check connection from replica to remote master 'ipa7.example.com':
 Directory Service: Unsecure port (389): OK
 Directory Service: Secure port (636): OK
 Kerberos KDC: TCP (88): OK
 Kerberos Kpasswd: TCP (464): OK
 HTTP Server: Unsecure port (80): OK
 HTTP Server: Secure port (443): OK
 PKI-CA: Directory Service port (7389): OK

The following list of ports use UDP protocol and would need to be
checked manually:
 Kerberos KDC: UDP (88): SKIPPED
 Kerberos Kpasswd: UDP (464): SKIPPED

Connection from replica to master is OK.
Start listening on required ports for remote master check
Get credentials to log in to remote master
admin@CODEAURORA.ORG password: <strong>ipaadmin72</strong>

Configuring NTP daemon (ntpd)
..snip..
Configuring directory server for the CA (pkids): Estimated time 30 seconds
..snip..
Done configuring directory server for the CA (pkids).
Configuring certificate server (pki-cad): Estimated time 3 minutes 30 seconds
..snip..
Done configuring certificate server (pki-cad).
Restarting the directory and certificate servers
Configuring directory server (dirsrv): Estimated time 1 minute
..snip..
Starting replication, please wait until this has completed.
Update in progress
..snip..
Update succeeded
..snip..
Done configuring directory server (dirsrv).
Configuring Kerberos KDC (krb5kdc): Estimated time 30 seconds
..snip..
Done configuring Kerberos KDC (krb5kdc).
Configuring kadmin
..snip..
Done configuring kadmin.
Configuring ipa_memcached
..snip..
Done configuring ipa_memcached.
Configuring the web interface (httpd): Estimated time 1 minute
..snip..
Done configuring the web interface (httpd).
Applying LDAP updates
Restarting the directory server
Restarting the KDC
Using reverse zone 122.168.192.in-addr.arpa.
Configuring DNS (named)
..snip..
Done configuring DNS (named).

Global DNS configuration in LDAP server is empty
You can use 'dnsconfig-mod' command to set global DNS options that
would override settings in local named.conf files

Restarting the web server</pre>

At this point, the replica should start functioning. Since this is a FreeIPA server, make sure to allow successful logins. A reboot is a very good idea.

<pre># authconfig --enablemkhomedir --update
..snip..
# chkconfig sssd on
..snip..
# init 6</pre>

Once rebooted, login with an existing user.

<pre>$ ssh replica.example.com
Warning: Permanently added 'replica.example.com' (ECDSA) to the 
list of known hosts.
Creating home directory for herlo.
Last login: Fri Oct 22 12:27:44 2014 from 192.168.122.1
[herlo@replica ~]$ <strong>id</strong>
uid=151600001(herlo) gid=151600001(herlo) groups=151600001(herlo)...</pre>

Assuming all works well, replication should be working.

If all goes well, I&#8217'll show how to install a client and enable sudo access in the next post.

Cheers,

herlo
