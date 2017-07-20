---
layout: post
title:  "Project requirements #3: Database layout"
date:   2017-07-18
categories: requirements
---

This is part three on requirements for our blogging engine. See [part 1 - the press release]({{ site.baseurl }}{% post_url 2017-07-18-requirements-1-press-release %}) and [part 2 - Personas]({{ site.baseurl }}{% post_url 2017-07-18-requirements-2-proto-personas %})

### A diversion/pause

At this point in our set, we should be working through our wipeboards or other design options. But, I'm going to tell you a secret. I've been thinking about this project for ... years. As such, some of our decisions have already been made. For instance, you might have noticed in the press release that we mentioned CouchDB. That's what we're going to use as a backend for the following reasons:
1. I want to learn how to hook up Couch through Node.
2. I eventually want to build a Pouch/React version of the website (that's not our first version though).
3. I eventually want to build a iOS version to test CouchbaseLite and Couch syncing.

I've spent time thinking about the database layer -- the 'tables' or document types. It tends to be how I start my thought process (1. general idea of the functionality. 2. What are the objects that need to be there to express that functionality.) 

I'm going to lay that on you now because I want to make sure we're expressing all of the documents and their contents as part of a design (and, conversely, push design needs back into the document types).

See here: [Database tables]({{ "/supporting/databasetables.html" | prepend: site.baseurl }})