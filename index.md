---
title: Home
layout: page
description: "Here I share the programming stuff that I learn. Many times, it's for my own reference. It might help people stuck with similar problems. I have seen a lot of professional growth due to the efforts of various opensource communities. This is my small way of giving back."
tags: [Manu, Ganji, technology, programming, blog,]
group: navigation
---
<div class="hero-unit">
    <h1>Hello, world!</h1>
    <p>Here I share the programming stuff that I learn. Many times, it's for my own reference. It might help people stuck with similar problems. I have seen a lot of professional growth due to the efforts of various opensource communities. This is my small way of giving back.</p>
</div>
<h4>Recent Articles</h4>
<hr/>
<ul class="post-list">
{% for post in site.posts limit:10 %} 
  <li><article><a href="{{ post.url }}">{{ post.title }} <span class="entry-date"><time datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: "%B %d, %Y" }}</time></span></a></article></li>
{% endfor %}
</ul>
{% comment %}
<center style="margin-top:30px;">
    <iframe style="min-width:325px;" src="https://docs.google.com/forms/d/1OL07Y_5TqQdef2EoGwNMRCaY7yy5yD9rT5kGsAkgk1I/viewform?embedded=true" width="35%" height="800" frameborder="0" marginheight="0" marginwidth="0">Loading...</iframe>
</center>
{% endcomment %}
