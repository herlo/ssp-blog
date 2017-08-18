# Content for SexySexyPenguins + Modified Theme

This repository contains the posts, images, configuration, and theme that make
up the static site hosted at http://sexysexypenguins.com

Because the [Hyde Theme](https://github.com/spf13/hyde) was very useful, I've
modified it only slightly to accommodate my needs.

Below is a tree of the current structure.

    ssp-blog
    ├── archetypes
    ├── config.toml # configuration of hugo site (crux of the whole deal)
    ├── content # all of the content lives here
    │   ├── about # simple about herlo page
    │   ├── posts # imported content from the old wordpress site and new posts
    │   └── uploads # images and audio files associated with each post go here
    ├── layouts
    │   └── shortcodes # little code snippes to make rendering a site useful
    ├── README.md # this document. :)
    ├── static
    │   └── images # any overridden images go here.
    └── themes
        └── hyde # as mentioned above, a slightly modified version exists here

# The process

The basic plan is to perform the following cycle for updating the blog with
a new post.

1. Write Article, including media collateral and such
2. Test on local site using 'hugo server --baseURL http://localhost:1313'
3. Once article is publishable, commit to local repository
4. Upload any media collateral larger than 50MB
5. Push updates to live repository `git push stage master`
  * The git post-receive hook on the live server will generate a new
    site with the updated values and display them under the live host
6. Once the site is updated on live, push to origin `git push origin master`.
  * This saves it here on github.

The configurations for the post-receive hook can be found in the
[ssp-packer-templates](https://github.com/herlo/ssp-packer-templates)
repository.

This process is based upon the useful information found at
https://www.digitalocean.com/community/tutorials/how-to-deploy-a-hugo-site-to-production-with-git-hooks-on-ubuntu-14-04
