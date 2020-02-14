---
layout: default
title: Christopher Cowell, LLC - Blog
---

# Blog

<!-- ## All Posts by Date -->

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title | smartify }}</a>
    </li>
  {% endfor %}
</ul>

---

<!--
## Posts by Category

{% for category in site.categories %}

<h5>{{ category[0] }}</h5>
  <ul>
    {% for post in category[1] %}
      <li>
        <a href="{{ post.url }}">{{ post.title | smartify }}</a>
      </li>
    {% endfor %}
  </ul>
{% endfor %}
-->

<!--
{% comment %}
#
#  Change date order by adding '| reversed'
#  To sort by title or other variables use {% assign sorted_posts = category[1] | sort: 'title' %}
#
{% endcomment %}
{% assign sorted_cats = site.categories | sort %}
{% for category in sorted_cats %}
{% assign sorted_posts = category[1] | reversed %}
<h2 id="{{category[0] | uri_escape | downcase }}">{{category[0] | capitalize}}</H2>
<ul>
  {% for post in sorted_posts %}
 	<li><a href="{{ site.url }}{{ site.baseurl }}{{  post.url }}">{{  post.title }}</a></li>
  {% endfor %}
</ul>
{% endfor %}
-->
