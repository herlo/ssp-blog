+++
date = "2017-09-12 08:56:43-06:00"
draft = false
title = "My First Flock: Hyannis, Massachussetts"
series = ["fedora"]
tasks = [
]

+++

In the past I've been a big part of the Fedora Project, attending many FUDCons and Activity Days. The last FUDCon, however, was in 2013, in Lawrence, Kansas. In other words, I haven't been to a Fedora-run event in about 4-1/2 years. That changed this weekend when I arrived in Hyannis, Massachussetts for `Flock <https://flocktofedora.org/>`_.

Getting to Flock
================

My trip down from Boston was very comfortabe thanks to Mohan, whom I had not met prior to riding down. I also talked with a nice fellow Robert, who rode along with us. I arrived easily around 6pm, checked in and was able to find dinner in town. I walked around the town for a bit, and headed back for an early evening.

My Purpose at Flock
===================

As part of my charge, I've started investigating where things might be falling down in the future with regard to scaling resources. Considering the amount of builds, repository creation, composes and tools to help build all of those things in an automated way, it's likely things will need a way to scale up.

I believe the scale of the infrastructure needed will not only be increasing by orders of magnitude within Fedora, but will also need to scale on-demand. Because I'm helping to write and maintain a `cloudy provisioner <https://linchpin.readthedocs.io>`_, this is a place were we should start having discussions.

Day One: Factory 2.0, Containers, and Scaling
=============================================

The first part of every FUDCon, was the State of Fedora by the Fedora Project Leader. As a transition to my first Flock, I appreciated that Matthew Miller started it all off in a very similar way. He talked about how releases are always improving, downloads continue to go up, giving a direction.

He discussed a new charge for Ambassadors. A direction for events and such, focusing on specific community objectives. The detail of this is posted on `his blog here <https://communityblog.fedoraproject.org/ambassadors-fedora-strategy/>`_.

Lastly, he talked about what I saw as the biggest goal for the next year or two in Fedora, Modularity. If you've not heard about Modularity, Factory 2.0, or the Fedora.Next initiative, I highly suggest you perform a quick google search and do some reading.

Sessions I Attended
-------------------

I attended two sessions on day one. One of the changes they made for Flock this year is it was to be more of a 'DO' type conference. Most presentations were scheduled for the first day, focusing on workshops the rest of the week.

The first was on Factory 2.0 by Mike Bonnet. He covered all of the new tools that help build the Fedora modular components. It covered new features like Freshmaker, ODCS (On-Demand Compose Service), and WaiverDB. Again, a lot to search on the Googles.

The second session I attended was Become a Container Maintainer workshop. Adam Miller and Josh Berkus guided us through the updates of how to build a container using the Fedora docker registry.

Evening Fun
-----------

The first evening of Flock was Game Night. In addition, Justin Flory organized a candy exchange. I enjoyed trying candy and treats from around the world while playing a game I brought. Later after that, I ended up walking again on Main Street in Hyannis, doing a little bar hopping and making some new friends.


Day Two: Packaging, Tooling in-depth, Testing with dist-git, and more
=====================================================================

Wow, a long heading! I guess that is justified, giving this was probably my busiest day of sessions.

Sessions I Attended
-------------------

As usual, Stef Walter did an excellent job explaining CI tooling in simple terms. His talk focused on how dist-git tests might work using Ansible. This session got me thinking about the difference between provisioning nodes to run all of the tests vs tests doing provisioning as part of the test. In both cases, LinchPin can help. I pulled him aside after lunch to ask about how these tests might scale and this direction became even more clear. essentially, it gave me a lot more to think about with regard to provisioning.

I spend the next few hours in the same room, learning about Freshmaker, Greenwave, and Delorian (DLRN). Freshmaker and Greenwave are Factory 2.0 tools. These tools are used to help build Fedora in a more flexible way.

`Freshmaker <https://fedoraproject.org/wiki/Infrastructure/Factory2/Focus/Freshmaker>`_ tooling helps to ensure that when an RPM, container, module, or something else changes, all of the affected components in the chain are also scheduled to be updated. Freshmaker has some intelligence built-in to determine what components need to be updated, and performs the actions automatically.

`Greenwave <http://readthedocs.org/projects/greenwave/>`_ is a policy engine for allowing builds to commence. The policies help deterimin if the artifact is 'good enough' to continue down the build and compose chain. Essentially, Greenwave allows gating on automated tests with built-in policies. Humans would obviously control the policies, but some automated policies could be in place to start for each artifact, just to ensure that a policy exists. WaiverDB would then look at Greenwave and make decisions on each artifact and how it must proceed down the chain.

I had also intended to spend time in the Future of fedmsg session, but instead I ended up talking for over an hour with the ever intelligent Dennis Gilmore about scaling of Koji. The challenges here are not small. After some initial verbiage clarifications, we got down to the difficult bits of how koji might be able to scale. This will be quite the undertaking for someone for sure. I really appreciated him sitting down and talking through it with me. This was among the best session I had, probably because it was so in-depth.

Evening Fun
-----------

Wednesday evening was a blast, as we attended `Wackenhammers Clockwork Arcade and Carousel <http://www.wackenhammer.com>`_. We were provided with food from a Vietnamese truck, the noodle bowl I had was quite good. I quite enjoyed the arcade, because we basically got unlimited tokens, which led to unlimited tickets. I spent a good amount of time racking up tickets, and ended up with 1425. I started looking at the prizes, but couldn't find anything I really enjoyed. Then, the lady behind the counter showed me a section I hadn't seen previously. 

And there they were, **my new specs**!

.. image:: {{<siteurl>}}uploads/2017/09/herlo_wackenhammer_glasses.jpg
   :target: {{<siteurl>}}uploads/2017/09/herlo_wackenhammer_glasses.jpg
   :height: 250px
   :alt: Click image to see full size

I got a bunch of fun comments on them, from Ozzy to Elton to John Lennon. If you have another look for me, lmk as I might have a plan for Halloween now. :)


At the end of Day Two, I spent another hour talking with my roommate, Adam Williamson. We discussed the day's events, and specifically talked about testing, qa and of course, my koji conversation. This conversation lasted about 2 hours. Then, because my brain was going, I spent the next hour or so thinking, and trying to sleep. It was very late when I finally fell asleep.

Day Three: Better late than never!
==================================

Because I was up so late the night before, I slept in, got a decent breakfast in town, and ran a couple errands. I ended up getting back just in time for lunch. My new friend Maria had promised to corn row my hair at lunch time, but I could not find her. It turns out that she had forgotten and went to lunch at Spanky's with some of her friends.


Sessions I Attended
-------------------

I finally cought up with Maria at the talk by Mo 'Design Pattern Library' just after lunch. It's clearly been a while since I've been around the design folks in Fedora, but it was a refreshing change. I learned about the Atomic structure inside Fedora's design library and how about mustache (or other frameworks, which I forget the names of) to put it together.

After Mo's session, Maria did up my hair in a less-corn-row style, but it was very very well done. I thanked her, and left. They continued on their design hackfest, which I heard later was quite successful. Here's her handiwork.

.. image:: {{<siteurl>}}uploads/2017/09/herlo_braids.jpg
   :target: {{<siteurl>}}uploads/2017/09/herlo_braids.jpg
   :height: 250px
   :alt: Click image to see full size

I then attended Tomas Tomacek's "Let's create a module" workshop. I think this was the most in-depth I've gotten with the modulemd file. The file is a YAML descriptor of both modules and RPMs that this module depends upon. It also contains similar things to a SPEC file for RPMS. Essentially, the goal here was to educate as many packagers as possible on how to build modules. Hopefully, this will jumpstart modules into Fedora for the future.

The next session I attended was Stef's talk on how to deliver CI and CD of Fedora. Because I had spent the better part of an hour at lunch talking to him the day before, a lot of this was already clear. One of those 'aha' moments happened at the lunch chat, and was more solidified at the talk. 

Centered around provisioning, there are really two big points where tests might need to provision. The first would be the more obvious, provision a system to then configure it and run the tests. The second, and less obvious is that tests themselves might want to provision nodes, containers, vms, etc. as part of the tests. This got me to thinking about whether those who write tests would use what they already know, or consider a tool like LinchPin.

The final session I attended this day was the GPG Keysigning Party. Nick Bebout was a little disorganized. In the end, I was able to verify about 20 others IDs and key fingerprints. I expect to be signing these in the days to come. To the many of these folks who have already signed my new key, thank you.

Evening Fun
-----------

Because I hadn't spent any time with the modularity guys since DevConf in January, I found them and joined them for dinner at Tap City Grill. The food and beer was yummy, but the conversations were excellent. I look forward to seeing them again soon. I hope to make DevConf again next year. If not, I am planning to come to Europe next June-August, so hopefully we can have a few beers at that time.

After dinner, I joined my friends, Masha, Amita, Aurelian, Xavier, Jenn, and Maria at Embargo for what ended up being one drink. I ended up playing silly teenage games, like truth or dare (somehow mixed with spin the bottle using a fork). My dare was to go up to a gentleman at the bar, tell him that I thought he was handsome and wanted to dance. A few minutes later, Mike was hanging out with us after a nice little jig. That was very fun and very funny.

I left, headed back to the hotel, and joined some other Fedorans to drink and chat. This ended up moving a couple of times because drinking wasn't allowed there. Eventually, we ended up in our room for a couple of hours until everyone was ready to crash. Long, but fun night. This is the stuff I really enjoy at Fedora conferences.

Day Four: Let's wrap it up!
===============================

I'm not sure I loved the wrap up session on day four. But it did allow me to hear perspective from others on how their Flock experience went. For me, it felt like a long session regurgitating what had happened. From an administrative perpsective, I'm sure it was quite useful. Several folks got up multiple times, and it felt a bit forced at times to get people to come up and talk about their take on the conference.

The one thing I got out of it was that I could spend a bit of time writing the beginnings of this post. So I took advantage and wrote down things that I wanted to remember. So you can thank the wrap up session for my inspiration.

Afternoon/Evening Fun
---------------------

Since the day was short, a few of us headed out to Nauset Beach, the easternmost point on the cape. First, however, we dropped Masha at the Hyannis transport hub, so she could catch her bus to the Airport. After some delay, and a nice goodbye, we headed out.

The beach was gorgous, and they had one of those planes that fly with banners behind them. That was very interesting. We got a little wet in the ocean, talked some, and napped. The sun was soft and the wind was cool, but it wasn't cold until the sun started setting. At that point, we got up and had fun with our long, maybe 50 foot shadows. Afterward, we went north up the cape, got dinner at this amazing place, called Karoo. Unfortunately, I felt a bit ill, so I couldn't finish my lamb shank, but it was very, very good. I asked to stop for ice cream to help with my belly, which was quite yummy as well. Heading back seemed to take less time, as it does. Early to bed for me though.

Day Five: Departure
===================

We had a nice breakfast on Main Street in Hyannis, then headed to the Airport via bus from the same transport hub. As with all good things, they must eventually come to an end. Saturday had come, most of my friends had already left. I will again miss them. I hope they will miss me, our talks, the fun. But of course the memories will remain. I look forward to the next time I will see them.

Flock was a very good conference. Hyannis Conference Center was second rate, but still valuable. The cape will likely still be there for many years to come. I look forward to my contributions, as well as the contributions of others in the Fedora Project. It has been a big part of my life for such a long time now, and I'm glad to be a part of it.


Cheers,

herlo


