---
layout: post
title:  "Project requirements #4: CouchDB database security and delivery"
date:   2017-07-24
categories: requirements
---

Continuing on from our database tables [reveal]({{ "/supporting/databasetables.html" | prepend: site.baseurl }}) and [discussions]({{ site.baseurl }}{% post_url 2017-07-19-requirements-3-tables %}), let's talk a bit about security and how I imagine it will work within the CouchDB world.

First, let's look back at one of our [user stories]({{ site.baseurl }}{% post_url 2017-07-18-requirements-2-proto-personas %}) :

Our owner, Jennifer:
> Wants to have private posts for certain kinds of members

So, we have potentially 3 levels of document security:
1. Draft, not published, only for authors/editors
2. Published for everyone
3. Published for some sub-set of users (members)
	* Potentially more than one type of member, but we won't worry about that now.

Based on my reading of [per document security in CouchDB](https://wiki.apache.org/couchdb/PerDocumentAuthorization), there's no good way to do a private document by user or set of users. The best is a validate on read doc but the impact of that on performance seems seriously deleterious at any kind of scale (and kind of silly). 

The 'accepted' way appears to be a per-user, or in our case, per-audience, database. At the moment I imagine that the general database layout will be:
```
                  Main      <-- Writes
                  /  \
                 /    \
               All    Member    <-- Reads based on audience
```

* `Main` is where writing takes place. Also where core user data lives.
* `All` is where status:published items for audience:all are replicated.
* `Member` is where member items + 'All' items are replicated.

I imagine in the middleware layer we will point to the appropriate database depending on the user's `audienceLevel` flag. 

You will notice in the 'targettable' [tables]({{ "/supporting/databasetables.html" | prepend: site.baseurl }}) that each has an audience flag:
```
audience | String | 'all', 'member', 'patron', 'none'
```

 along with the status flag:
 ```
 status | String | "draft", "published", "removed", "review", "submitted"
 ```

With that, we can then determine what gets pushed out to the replicants. Testing replicants is going to be a bit tricky - we'll table that for now.