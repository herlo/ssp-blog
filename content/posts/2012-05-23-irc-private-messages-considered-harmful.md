---
title: 'IRC: Private messages considered harmful – or Be considerate to others on IRC'
author: herlo
layout: post
date: 2012-05-23T22:41:50+00:00
url: /2012/05/23/irc-private-messages-considered-harmful/
categories:
  - Community
  - Fedora
  - Geek
  - IRC
  - Tech
tags:
  - 2012
  - Community
  - irc
  - may
  - PM
  - Private Message

---
<div>
  <p>
    I use IRC a LOT. IRC Clients allow users to send what are called &#8220;private messages&#8221; (or PMs). Today, I sent a private message to my friend <a href="http://fedoraproject.org/wiki/User:Kevin">Kevin Fenzi</a>. I received the following reply:
  </p>
  
  <p>
    '(Autoreply) Please consider if what you are sending me needs to be in a Private message. See: <a href="http://tinyurl.com/64vdbql">http://tinyurl.com/64vdbql</a>' (sic)
  </p>
  
  <p>
    So I clicked&#8230;. and what I read pretty much fit my thought process. I think it's pretty great, so I thought I would share with all of you.
  </p>
  
  <p>
    –<br /> There are a few cases where PM's could possibly be acceptable:
  </p>
  
  <ul>
    <li>
      You have something that NEEDS to be private (account info, phone number, etc). You should ask yourself however if a unencrypted IRC session is the right place to send that info. Perhaps a phone call, a scp to a secure server, or a gpg encrypted email would be better?
    </li>
    <li>
      It's something you need to impart to JUST that one person. A friendly jibe or conversation with someone you know well perhaps, or a quick note from someone that they are running late or are going to do something for you.
    </li>
  </ul>
  
  <p>
    That said, there are a number of cases where they are NOT a good idea (especially in support channels):
  </p>
  
  <ul>
    <li>
      The person you are PMing might be busy, so you get no answer, but many others in a common channel may know the answer to your question.
    </li>
    <li>
      The person you are PMing might give you a incorrect or incomplete answer, which other people in a common channel could correct or expand on.
    </li>
    <li>
      Other people in a common channel cannot learn from your question or any answers you get. Perhaps they too were interested in doing that? Perhaps they have a related question that comes from that one? It's good for everyone to ask questions in a common channel.
    </li>
    <li>
      It doesn't scale. You can't always ask a person your questions directly. Sometimes people are on vacation or busy and you will not get answers. If 100 people try and ask one person privately each question most IRC clients would go crazy with tabs and trying to keep track of those separate conversations.
    </li>
    <li>
      Some people provide support for things for a living. If you are directly PMing them shouldn't you pay for private support?
    </li>
    <li>
      IRC is somewhat transitory. Unless someone has setup a bouncer (znc, bip, dircproxy) and set it to record private messages, they can easily be lost (just reboot without checking all of them and many clients won't show them on restart of the app). So, if you PM someone the message may well not get through anyhow.
    </li>
  </ul>
  
  <p>
    Finally there are some modes of interest (on freenode at least):
  </p>
  
  <ul>
    <li>
      /umode +R – This will prevent people who are unidentified with freenode services from sending you private messages.
    </li>
    <li>
      /umode +g – This will prevent you from receiving private messages from anyone not on a session-defined whitelist. The content of the whitelist can be controlled using the /accept command. When a user not on the whitelist attempts to contact you, you will receive a notice informing you of the fact and you can then use /accept user to speak to them. Users can be removed from the whitelist using /accept -user. Finally, /accept * will print the whitelist.
    </li>
    <li>
      Other clients or IRC bouncers may have ways to log/ignore/etc private messages. See your clients docs.
    </li>
  </ul>
  
  <p>
    In some channels/areas it's polite to ask before PMing: 'Hey, foo, mind if I PM you my phone number?' or 'Hey foo, can I PM'.
  </p>
  
  <p>
    So, next time you are in a community channel and want to PM someone, do consider the above before doing so, odds are it would be much better to just ask in the main community channel than PM some particular person.<br /> –
  </p>
  
  <p>
    Cheers,
  </p>
  
  <p>
    herlo
  </p>
</div>