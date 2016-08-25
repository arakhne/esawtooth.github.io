Title: First Steps
Slug: first-steps
Date: 2013-11-30 14:55
Category: tech general
Tags: tech general
Author: Rohit Jain
Summary: Blog v1


I suppose it was long past time that I started blogging. I love to
write. I also love technology and the ecosystem that surrounds
it. However, despite the presence of both of those two passions, I could
never quite see the charm in creating a blog. A fair bit of that, in
hindsight, had to do with not feeling at home with writing a bunch of
stuff inside a textarea in a browser, however nice. The tools we use to
give effect to our creations are rather important. I prefer writing on
paper, where the smell of the ink, the sounds of the nib hitting the
paper, and the shadings in the colours generate an effect that cannot
easily be communicated. However, now that I begin to write words out on
my vanilla emacs frame, while knowing that I am being much more
efficient a writer and an editor than I ever could manage to be, on my
best day on paper, not to mention the potential of a reader, I think
that it might now, just be worth it.

Let me start out with a brief description of how this blog exists, and
what ideas and requirements influenced its form. When I decided to start
writing stuff online, I felt that the following were important for me to
do a reasonable job:

* __The editor should be emacs et al.:__ I refused to write inside a
  browser window, with few, if any editing controls at my disposal. If I
  need to write a bunch of stuff, the editor just _has_ to get out of my
  way. That was not going to happen without a lot of effort inside a
  browser textarea.

* __The formatting should be minimal:__ I wanted to focus on content,
  and not how it appears. The appearance should be consistent and nice,
  but when creating content, the design really should matter very
  little. Latex makes a lot of sense to me, given that it defines a
  clear focus on describing the document being written, instead of how
  it should appear. Markdown is a lot simpler though for now, not to
  mention faster and more specific.

* __The content should be under versioning:__ Versioning digital content
  of any kind, makes a lot of sense to me. While I doubt I would be
  doing a lot of branching in the git repo holding this stuff, the diffs
  in the content directory are no doubt going to be helpful, if nothing
  else, then for me to be able to see how my writing has changed over
  the months (if this blog lasts that long).

The idea of a static blog generator, with [heroku](https://heroku.com/)
that supports deployments on git push seem to fit the bill quite
nicely. The posts are simply markdown pieces of text, with some yaml
metadata on the top that is very easy to make sense of. The entire setup
seems to nicely get out of the way of creating content. The presence of
a database is mostly unnecessary for my requirements. So this is what I
am doing right now. I am using [Octopress](http://octopress.org/) to
write my posts and am publishing them to heroku. The instructions
[here](http://def.reyssi.net/blog/2012/01/14/get-blogging-with-octopress-on-heroku/)
by Sam are rather good. The only deviation I needed to make them work
for me was to use ruby v1.9.3 instead of v1.9.2, the latter of which
does not play well with the markdown library octopress uses. I also
tried out [hexo](http://zespia.tw/hexo/) for a while. However, I felt
that its not very mature right now. Octopress seems to have a much more
active community and that definitely matters a great deal as well. I
felt that Hexo was considerably simpler to deploy, however, and faster
to get started with as well, particularly on heroku. Perhaps I will take
a look at it again someday. Right now, I am too happy to be writing
stuff to be very concerned about it.
