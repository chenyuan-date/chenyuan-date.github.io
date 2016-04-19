---
layout: post-index
title: "尘缘"
description: "Dream for future"
tags: [Linux, Python, web, blog, thoughts]
comments: false
share: false
---

{% for post in paginator.posts %}
<article class="hentry">
  <header>
    {% if post.image.feature %}
      <div class="entry-image-index">
        <a href="{{ site.url }}{{ post.url }}" title="{{ post.title }}"><img src="{{ site.url }}/images/{{ post.image.feature }}" alt="{{ post.title }}"></a>
        {% if post.image.credit %}<div class="image-credit">Image source: <a target="_blank" href="{{ post.image.creditlink }}">{{ post.image.credit }}</a></div><!-- /.image-credit -->{% endif %}

      </div><!-- /.entry-image -->
    {% endif %}
    <div class="entry-meta">
      <span class="entry-date date published updated"><time datetime="{{ post.date | date_to_xmlschema }}"><a href="{{ site.url }}{{ post.url }}">{{ post.date | date: "%B %d, %Y" }}</a></time></span><span class="author vcard"><span class="fn"><a href="{{ site.url }}/about/" title="About {{ site.owner.name }}">{{ site.owner.name }}</a></span></span>
      {% if site.reading_time %}
      <span class="entry-reading-time">
        <i class="fa fa-clock-o"></i>
        {% assign readtime = post.content | strip_html | number_of_words | divided_by:site.words_per_minute %}
        Reading time ~{% if readtime <= 1 %}1 minute{% else %}{{ readtime }} minutes{% endif %}
      </span><!-- /.entry-reading-time -->
      {% endif %}
    </div><!-- /.entry-meta -->
    {% if post.link %}
      <h1 class="entry-title"><a href="{{ site.url }}{{ post.url }}" class="permalink" rel="bookmark" title="{{ post.title }}"><i class="fa fa-bookmark"></i></a> <a href="{{ post.link }}">{{ post.title }}</a></h1>
    {% else %}
      <h1 class="entry-title"><a href="{{ site.url }}{{ post.url }}" rel="bookmark" title="{{ post.title }}" itemprop="url">{{ post.title }}</a></h1>
    {% endif %}
  </header>
  <div class="entry-content">
    {% if post.content contains "<!-- more -->" %}
    {{ post.content | split:"<!-- more -->" | first % }}
    {% else %}
      {{ post.content }}
    {% endif %}
  </div><!-- /.entry-content -->
</article><!-- /.hentry -->
{% endfor %}

{% include pagination.html %}