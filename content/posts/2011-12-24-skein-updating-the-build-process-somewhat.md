---
title: 'Skein: Updating the build process (somewhat)'
author: herlo
layout: post
date: 2011-12-25T01:24:44+00:00
url: /2011/12/24/skein-updating-the-build-process-somewhat/
categories:
  - Fedora
  - GoOSe
  - Tech
tags:
  - 2011
  - build
  - December
  - GoOSe
  - process
  - skein

---
<div>
  <address>
    The <a href="https://groups.google.com/group/goose-linux/browse_thread/thread/7f068af8b978ab52">original post is in the GoOSe mailing list</a>. I am reprinting here for a wider audience.
  </address>
  
  <p>
    Last night, Mike (shalkie) and I had a nice discussion about the process we are now using to build / import packages. This is in preparation for now and the future. A lot of this discussion is thanks to Mathieu Bridon (bochecha).
  </p>
  
  <p>
    I have inserted a few notes in the process below for clarification.
  </p>
  
  <p>
    02:03 < herlo> k, so you should know that you first 'skein request' a package<br /> 02:03 < herlo> it can be done with either the –path or –name option, but one must be provided<br /> 02:04 < herlo> normally, one shouldn't grant their own package. I should be around some tomorrow to grant packages in bulk for you as needed<br /> 02:04 < herlo> but<br /> 02:04 < herlo> if you do need to grant a package<br /> 02:04 < herlo> it should be something like<br /> 02:05 < herlo> skein grant -k <koji owner> -g <github owner> issue_number name
  </p>
  
  <p>
    Package repos and koji tags are what get created with skein grant. However *only* an admin can grant a new package into our build environment. This is to make sure we are not putting packages into the process that are not part of the upstream and/or for a good review<br /> process. In the future, I suspect quite a few people will be admins and this will be less problematic.
  </p>
  
  <p>
    02:05 < herlo> once granted, the package can be imported with<br /> 02:05 < herlo> skein import /path/to/srpm<br /> 02:06 < herlo> usually though, I do take one extra manual step.<br /> 02:06 < herlo> I visit the repo page on github and add a service hook<br /> 02:06 < herlo> if you look at this page: <a href="http://www.google.com/url?sa=D&q=https://github.com/gooselinux/libgnomecanvasmm26/admin/hooks&usg=AFQjCNG6KIv_Ic3KgYsKXQzFJx07YpJqXQ" rel="nofollow" target="_blank">https://github.com/gooselinux/libgnomecanvasmm26/admin/hooks</a><br /> 02:07 < herlo> you can see the 'Post-Receive URLs (1)'<br /> 02:07 < herlo> if you click on it, you'll see the url you should add for any new repo<br /> 02:07 < herlo> this post receive hook will automatically launch builds upon a commit
  </p>
  
  <p>
    If you have admin access to a repository (and if a package has been 'granted' to you, then you do), add the following in the Post-Receive<br /> URLs if it's not already there:
  </p>
  
  <p>
    <a href="http://www.google.com/url?sa=D&q=http://roman.gooselinux.org:8080/add&usg=AFQjCNEx42wY7S0qjsd8GMv39mKiAQ7NtA" rel="nofollow" target="_blank">http://roman.gooselinux.org:8080/add</a>
  </p>
  
  <p>
    02:08 < herlo> once you have that in place, run the import command described above<br /> 02:08 < herlo> at that point, everything should be pretty automatic.<br /> 02:08 < shalkie> k<br /> 02:08 < herlo> within 10 minutes, the build should automatically launch<br /> 02:08 < herlo> shalkie: seem pretty straightforward?<br /> 02:09 < shalkie> Yeah it does.<br /> 02:09 < herlo> k, so now it should also be clear that you may (and probably already do) have failed builds<br /> 02:09 < shalkie> The stack of email certainly suggests that.<br /> 02:09 < herlo> lol<br /> 02:10 < herlo> shalkie: a good portion of those can be run through again, though I have been working on fixing a few of mine<br /> 02:10 < herlo> shalkie: as you look through the failed builds, you may just need to run them again<br /> 02:11 < herlo> to do that, you can use<br /> 02:11 < herlo> skein build<br /> 02:11 < herlo> the way I usually do that is 'skein build –nowait dist-gl6 <pkg_name>'<br /> 02:11 < herlo> only an admin can perform this task (you are an admin)<br /> 02:12 < herlo> you can watch the tasks at <a href="http://www.google.com/url?sa=D&q=http://koji.gooselinux.org/koji&usg=AFQjCNEQ6JLQcbMJv5RSM8aVacSil6xUVg" rel="nofollow" target="_blank">http://koji.gooselinux.org/koji</a> as you always have, or go out for a<br /> few hours and check the build statuses when you return
  </p>
  
  <p>
    02:13 < herlo> BUT WAIT! There's more!<br /> 02:13 < herlo> If for some reason, you determine something has to change in the spec file, like another dependency or something<br /> 02:13 < herlo> you'll need to do two things<br /> 02:14 < herlo> first, clone the branch if not already there and then create a vanilla branch<br /> 02:16 < herlo> git checkout –track -b  <local branch> <remote>/<tracked branch><br /> 02:16 < herlo> eg git checkout –track -b vanilla origin/vanilla<br /> 02:16 < herlo> then push that vanilla branch<br /> 02:16 < herlo> git push origin vanilla<br /> 02:17 < herlo> this is so we can keep the original state of the package before we make any changes. I'll be working on  automating this later<br /> 02:17 < herlo> when vanilla is pushed, we'll go back to master and make our changes<br /> 02:17 < herlo> git checkout master<br /> 02:17 < herlo> <make changes><br /> 02:17 < herlo> git add <files changed><br /> 02:17 < herlo> git commit -m &#8220;message regarding changes&#8221;<br /> 02:18 < herlo> git push origin master<br /> 02:18 < herlo> again, when you push to master, a build will be launched within 10 minutes<br /> 02:18 < herlo> sit back, enjoy coffee and wait for the build to return
  </p>
  
  <p>
    At the moment, the 'master' branch is currently what is getting built. Vanilla never gets built, but serves as a reference point to what the upstream did at certain points along the way. The vanilla branch also provides a way to merge in upstream changes with our changes. Git will<br /> make this easy for us, because merge conflicts will be much easier to resolve across branches.
  </p>
  
  <p>
    I hope this little conversation is a bit clearer on the process we're trying to use. Look for further improvements coming to skein 2.1 (I already have quite the feature list) in the next few months.
  </p>
  
  <p>
    Cheers,
  </p>
  
  <p>
    Clint
  </p>
  
  <p>
    PS – I likely won't be online when this post is published as I'll literally be enjoying some GoOSe, prepared by my lovely wife. She is an amazing cook / chef and is attempting this for the first time ever!
  </p>
</div>