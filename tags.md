---
layout: page
title: குறிச்சொற்கள்
permalink: tags/
---

<!-- Get the tag name for every tag on the site and set them
to the `site_tags` variable. -->
{% capture site_tags %}{% for tag in site.tags %}{{ tag | first }}{% unless forloop.last %},{% endunless %}{% endfor %}{% endcapture %}

<!-- `tag_words` is a sorted array of the tag names. -->
{% assign tag_words = site_tags | split:',' | sort %}

<!-- List of all tags -->
<div id="post-list">
  <ul class="tags">
    {% for item in (0..site.tags.size) %}{% unless forloop.last %}
      {% capture this_word %}{{ tag_words[item] }}{% endcapture %}
      <li>
        <a href="#{{ this_word | cgi_escape }}" class="tag">{{ this_word }}
          <span>( {{ site.tags[this_word].size }} )</span>
        </a>
      </li>
    {% endunless %}{% endfor %}
  </ul>
</div>

<!-- Posts by Tag -->
<div>
  {% for item in (0..site.tags.size) %}{% unless forloop.last %}
    {% capture this_word %}{{ tag_words[item] }}{% endcapture %}
    <h2 id="{{ this_word | cgi_escape }}">{{ this_word }}</h2>
    {% for post in site.tags[this_word] %}{% if post.title != null %}
      <div>
        <span style="float: left;">
          <a href="{{ post.url }}">{{ post.title }}</a>
        </span>
        <span style="float: right;">
        <span class="fa fa-calendar"></span>
        {% assign m = post.date | date: "%-m" %}
        {{ post.date | date: "%-d" }}
        {% case m %}
            {% when '1' %}சனவரி
            {% when '2' %}பிப்ரவரி
            {% when '3' %}மார்ச்
            {% when '4' %}ஏப்ரல்
            {% when '5' %}மே
            {% when '6' %}சூன்
            {% when '7' %}சூலை
            {% when '8' %}ஆகசுட்
            {% when '9' %}செப்டம்பர்
            {% when '10' %}அக்டோபர்
            {% when '11' %}நவம்பர்
            {% when '12' %}டிசம்பர்
        {% endcase %}
        {{ post.date | date: "%Y" }}
        </span>
      </div>
      <div style="clear: both;"></div>
    {% endif %}{% endfor %}
  {% endunless %}{% endfor %}
</div>
