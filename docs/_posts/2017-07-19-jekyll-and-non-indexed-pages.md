---
layout: post
title:  "Jekyll - how to add pages and have them not automatically included in navigation"
date:   2017-07-19
categories: jekyll
---

_We take a break from our regular coverage of the requirements of our new blogging engine to talk about the blogging engine we are using to blog about the development of the blogging engine (sooo meta)._

We use [Jekyll](https://jekyllrb.com) to write about our development and for the most part it's awesome. However, today I wanted to create a document that wasn't a blog post. Jekyll has the concept of [pages](https://jekyllrb.com/docs/pages/), which are units of non-blog magic, but I found out they are always included in [site.pages variable](https://jekyllrb.com/docs/variables/). 

For this site we're using the totally capable, and [included](https://jekyllrb.com/docs/themes/), Minima theme. In this theme, the site.pages items are included in the site navigation at the top (see links to 'About' page and probably 'Supporting Files') - in the header.html include file. I wanted a set of pages that I could include in blog posts that were not either blog posts nor 'navigationally aware' pages. 

**Jekyll doesn't do that.**

Luckily, Jekyll is a pretty easy engine to customize, or at least hack around a bit. After reading through the docs, I decided to use tags in a way that they weren't designed for but works with minimal customization.

I call these pages 'supporting' pages and I tagged them 'x-sup' (full disclosure: they were initially 'supporting' but I realized I was going to forget and use that later in a tag and be sad). To keep them from showing up in the header, I used the `unless` function in [Liquid](https://shopify.github.io/liquid/) like so:

```liquid
{% raw %}
{% for my_page in site.pages %}
  {% if my_page.title %}
  {% unless my_page.tags contains 'x-sup' %}
  <a class="page-link" href="{{ my_page.url | relative_url }}">{{ my_page.title | escape }}</a>
  {% endunless %}
  {% endif %}
{% endfor %}
{% endraw %}
```
So, if the page has a title *and* the tags array does not contain the string 'x-sup', the header shows the title and url.

Then, I created another `_layouts` template and called it `supporting.html`. It does the opposite:

```liquid
{% raw %}
<ul class="post-list">
{% for a_page in site.pages %}
{% if a_page.title and a_page.tags contains 'x-sup'%}
  <li>
    <span class="post-meta">{{ a_page.date | date: "%b %-d, %Y" }}</span>
    <h2><a class="post-link" href="{{ a_page.url | relative_url }}">{{ a_page.title | escape }}</a></h2>
  </li>
{% endif %}
{% endfor %}
</ul>
{% endraw %}
```
Finally, I created another page that will be included in the navigation that calls this new layout:
```
---
layout: supporting
---
```

It works locally, it works on Github pages. All good.

_Back to our program._