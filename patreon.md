---
layout: default
title: Patreon Posts
nav_order: 9
---

This is an archive of posts from the [SpiritWiki Patreon](https://www.patreon.com/c/TheSpiritWiki) provided here for easy AI and research access. Please support the SpiritWiki by joining our Patreon. 

## Archive

{% comment %} Gather pages whose path contains 'patreon/' {% endcomment %}
{% assign patreon_pages = site.pages | where_exp: "item", "item.path contains 'patreon/'" %}

{% comment %} Exclude directory indexes and build a clean array {% endcomment %}
{% assign sorted_pages = "" | split: "" %}
{% for pg in patreon_pages %}
  {% unless pg.name == 'index.md' or pg.name == 'README.md' or pg.name == 'readme.md' %}
    {% assign sorted_pages = sorted_pages | push: pg %}
  {% endunless %}
{% endfor %}

{% comment %} Sort by the 'order' front matter variable {% endcomment %}
{% assign sorted_pages = sorted_pages | sort: 'order' %}

{% if sorted_pages.size > 0 %}
<div class="patreon-list">
{% for pg in sorted_pages %}
  <div class="patreon-item" style="margin-bottom: 1.5em;">
    <h3 style="margin-bottom: 0.2em;">
      <a href="{{ pg.url | relative_url }}">
        {{ pg.title | default: pg.name | replace: '.md', '' | replace: '-', ' ' | capitalize }}
      </a>
    </h3>
    {% if pg.description %}
      <p class="description" style="margin: 0.3em 0; color: #555;">
        {{ pg.description }}
      </p>
    {% endif %}
  </div>
{% endfor %}
</div>
{% else %}
<p>No pages found in the <code>patreon</code> directory.</p>
{% endif %}
