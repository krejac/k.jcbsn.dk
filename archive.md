—
layout: page
title: Copenhagen Marathon 2012
—

<p class=“message”>
  Dette er en samling af alle mine indlæg vedr. træningen op til Copenhagen Marathon 2012.
</p>

{% for post in site.posts %}
  <a href=“{{ post.url }}”>
    <h2>{{ post.title }}</h2>
    <p>{{ post.date | date_to_string }}
  </a>
{% endfor %}
