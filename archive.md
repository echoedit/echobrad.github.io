---
layout: page
title: Archive
---

<p class="message">
  Once you eliminate the impossible, whatever remains, no matter how improbable, must be the truth. -- Arthur Conan Doyle
</p>

{% for post in site.posts %}
 * {{post.date | date_to_string}} &mdash; [{{post.title}}]({{post.url}})
{% endfor %}
