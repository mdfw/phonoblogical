---
layout: post
title:  "Configuring Jekyll and Github Pages"
date:   2017-04-20
categories: jekyll
---
Our first step in setting up a blogging engine is to decide which one. Since I knew I wanted to host the source on Github, it seems a natural fit to host the blog on [Github pages](https://pages.github.com/). Luckily, Github Pages uses [Jekyll](http://jekyllrb.org), which is relatively straitforward to set up locally.

I'm not going to go through all of the setup as there are great posts out there on that, but I will point out a couple of decisions you have to make that I wish I'd made earlier:
1. Where you want to host your Github pages content. Initially I chose a separate branch (the gh-pages branch) to store the data but quickly realized it was not going to be easy to code and write at the same time, which is part of the goal here. So, I moved everything to the `/docs` directory and pointed Github pages to that.
2. If you want to style the blog. For this situation, it's not important, so I'm using the builtin Minima theme.

Also, one tutorial I read started coding on Github. I don't recommend that. Start locally and push up. Just use Jekyll.

That's it. 