---
layout: post
title: "A Blog Makeover"
date: 2015-12-01 11:44:51 +0530
comments: true
categories: blog tech
---

This one is just a quick update on my latest blog makeover. So this
business started when I discovered that a domain name that I've been
looking for a while just popped back up on the grid. They have a
tendency to do that, so it pays to keep looking once in a while. As an
aside, this has given me an idea for a sort of notification service for
when domains you care (or might care for) for become available. I think
I'll try to spare a weekend for this.

Anyways, once I bought this domain, I simply had to move my blog
over. Also, I wanted an email address linked to it as well. And of
course, my vpn server and other machines in the cloud had to be moved
onto subdomains of this one as well. Sigh. Given how I had previously
been using octopress for the blog, and that it had lately become
deprecated, I thought I might as well move over to Github Pages and
Jekyll while I was at it. Fortunately, the entire thing above proved to
be less of a pain than it usually is.

Trawling through the Github documentation got me to a simple jekyll
template site that I was able to link to my custom domain. For now I
have kept the apex domain pointed the blog since I've been too lazy to
maintain some seperate placeholder website. Hopefully I won't have to
either anytime soon. The good thing about the Jekyll move was that I was
simply able to copy over the old markdown files from the source/_posts
directory to the _posts directory of the jekyll tree. The only thing
that required some work was that the default markdown parser used by
jekyll used a different way of quoting code.

The email was a simple matter of creating a new Zoho Mail account and
aliasing that to my current Gmail account. So now, all mail from my
current Gmail account would be routed through the new email, and all
mail received at the new account would lie waiting for me in the Gmail
account. Piece of cake. One discovery was that I couldn't find the
account settings in Google's Inbox app. Had to do all the work from the
old Gmail interface with the clunky popups. Hopefully they will fix that
soon. Particularly if they ever decide to shutdown the old interface as
they are in the habit of usually doing.

Overall I am positive about the move now. Things feel neater, though
I've still got to figure out how to add commenting in Jekyll. I'll
update this post once that's done.
