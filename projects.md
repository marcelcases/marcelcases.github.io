---
layout: other
title: "Projects List"
category: projects
---
<h1> Projects </h1>
<h2> List </h2>

<ul>
  {% for post in site.posts %}
    <li style="list-style-type: square">
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>