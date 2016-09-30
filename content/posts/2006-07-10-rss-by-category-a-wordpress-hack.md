---
title: 'RSS by Category – A WordPress Hack'
author: herlo
layout: post
date: 2006-07-11T05:59:59+00:00
url: /2006/07/10/rss-by-category-a-wordpress-hack/
categories:
  - Tech

---
So recently, I had several conversations with others about having RSS feeds by category in WordPress. You can do this in other blog software, why not WordPress?

I found this nice little ditty that will easily display all of your different feeds. For those of us who blog on different subjects, like family or on non-FOSS-related subjects, this is really nice and easy to do. What I found was this page:

<a target="_blank" title="Creating RSS Feeds by Category" href="http://wordpress.org/support/topic/18679">http://wordpress.org/support/topic/18679</a>

Thing is, WordPress already has this functionality built-in, but I didn't actually know how to get the information. I started digging around and found the lovely post above. After adding one line to my _wp-content/**my-theme**/index.php_, it was working.

Here is the line I added:
  
`<br />
<?php wp_list_cats('sort_column=name&optioncount=1&feed=RSS'); ?>`

Here's one of the feeds WordPress creates for me:

<a title="WordPress Tech Feed" target="_blank" href="{{<siteurl>}}category/passion/feed/">{{<siteurl>}}category/passion/feed/</a>

This one is with pretty permalinks, if you don't have mod_rewrite with Apache or are using something else, this won't work for you.

Pretty simple really. Now I have a list of all of my feeds right underneath my blogroll on my site. I view this as a good improvement, and already have it working with <a target="_blank" title="Utah Open Source Planet" href="http://openclue.org/ut/">Utah Open Source Planet</a>.  Maybe we all should give this a try, it is really easy!!

Cheers,

Herlo