---
title: Talks
permalink: /library/talks/
---

# Talks

Conference presentations and invited talks from Manulife AI teams.

{% assign talks = site.library | where: "type", "talk" | sort: "year" | reverse %}
<ul class="library-list">
{% for item in talks %}
  <li class="library-item">
    <span class="library-year">{{ item.year }}</span>
    <a href="{{ item.external_url }}" target="_blank" rel="noopener">{{ item.title }}</a>
    {% if item.venue %}<span class="library-venue">{{ item.venue }}</span>{% endif %}
  </li>
{% endfor %}
</ul>

{% if talks.size == 0 %}
No talks yet.
{% endif %}
